# Lab 4 - Query

In this lab, we're going to take data from a Google Cloud Storage bucket and import it into Neo4j.  There are a few different ways to do this.  We'll start with a very naive LOAD CSV statement and then improve it.  

The Neo4j Data Importer is another option.  It's a great graphical way to import data.

The dataset is from the SEC's EDGAR database.  These are public filings of something called Form 13.  Asset managers with over 100m AUM are required to submit Form 13 quarterly.  That's then made available to the public over http.  We don't have time to download those in the lab today as they take a few hours.  But, if you're curious, they're all available [here](https://github.com/neo4j-partners/neo4j-sec-edgar).  We've filtered the data to only include filings over 10m in value.

## Simple Load Statement

For this portion of the lab, we're going to work with a subset of the data.  Our full dataset is a year of data.  However, we'll just be playing around with a a subset of a day's worth.  The data is [here](https://storage.googleapis.com/neo4j-datasets/hands-on-lab/form13-2023-05-11.csv).

You may want to download the data and load it into your favorite tool for exploring CSV files.  Pandas, Excel or anything else should be able to make short work of it.  Once you understand what's in the data, the next step would be to load it into Neo4j.

To load it in Neo4j, let's continue on with Neo4j Query.

We're going to run a Cypher statement to load the data.  Cypher is Neo4j's query language.  `LOAD CSV` is part of that and allows us to easily load CSV data.  Copy this command into the query field.

    LOAD CSV WITH HEADERS FROM "https://storage.googleapis.com/neo4j-datasets/hands-on-lab/form13-2023-05-11.csv" AS row
    MERGE (m:Manager {managerName:row.managerName})
    MERGE (c:Company {companyName:row.companyName, cusip:row.cusip})
    MERGE (m)-[r:OWNS {value:toFloat(row.value), shares:toInteger(row.shares), reportCalendarOrQuarter:date(row.reportCalendarOrQuarter)}]->(c);

![](images/01.png)

It should look like the following.  You can then press the triangle with a circle around it to run the job.

![](images/02.png)

That will load the nodes and relationships from the file.

You'll now see the nodes, relationships and properties we loaded.  We have two kinds of nodes, manager and company.  Manager nodes are asset managers.  Company nodes are the companies that those asset manages buy shares of.  Managers are related to companies by the owns relationship.  Manager, company and owns all have properties that we can inspect as well.

Click on "Manager" under "Nodes" to automatically generate a new cypher query and run it.

![](images/03.png)

You'll now see a subset of the managers we have in the database.  The query returns 25 of them.  It's limited because returning to many nodes in this visualization mode can make it hard to navigate.

Now, let's click on one of the managers.  Don't worry, it doesn't particularly matter which one.  

![](images/04.png)

Once we've clicked on it, we can see its details.  This particular manager has a property "managerName" with value "Second Half Financial Partners, LLC."

Right click on that manager to open a context menu.

![](images/05.png)

Select "Expand selected."

![](images/06.png)

When it expands, we can see what companies this manager owns shares in.  In this case, "Smithfield Trust Co" seems to only have five holdings.  Note that this data set only has holdings over 10m.  Smaller holdings were filtered out in pre-processing.

Try selecting a company that is connected to our manager.

![](images/07.png)

In this case, we see the company "JOHNSON & JOHNSON" has CUSIP 478160104.  A [CUSIP](https://en.wikipedia.org/wiki/CUSIP) is a unique identifier in the financial services industry.

We can also click on the relationship, that is the line between the nodes to see detail on the transaction.

![](images/08.png)

In this case, it appears we have a report from 2023-03-31 that 3008 shares were purchased with a value of 310,715,000.  That number of shares is almost certainly missing some zeroes.  Sometimes these regulatory filings have significant quality challenges.  It seems we've just uncovered one!

At this point, take some time to poke around the graph.  You can expand it by clicking the icon with two arrows pointing away from each other in the upper right.  

![](images/09.png)

Click the different views in the upper right to adjust the display.

![](images/10.png)

We can click on some more nodes and expand them.

![](images/11.png)

As you play around, you may start to see some of the structure in the graph with recurrent connections and interesting communities of managers who have similar holdings.

Let's shrink the graph view back by clicking the icon in the upper right.

![](images/12.png)

Now that we have some understanding of this portion of the dataset, we're going to delete it.  Then we'll load the full data set.  To delete all the nodes and relationships enter this command:

    MATCH (n) DETACH DELETE n;

![](images/13.png)

Then press the run button.

![](images/14.png)

Now, all your data should be deleted.  Note that Workspace is still caching some property keys.

![](images/15.png)

In the next section, we'll load more data.

## More Performant Load

The LOAD CSV statement we used before was pretty naive.  It didn't create any indices.  It also loaded the nodes and relationships simultaneously.  Both of those are inefficient approaches.  It wasn't a big deal as that single day was a small amount of data.  However, we'd now like to load a full year of data.  That has a million rows, so we have to be a bit more efficient.  That new dataset is [here](https://storage.googleapis.com/neo4j-datasets/hands-on-lab/form13-2023.csv).

If you're curious, you can read a bit about the intracties of optimizing those loads here:

* https://neo4j.com/developer/guide-import-csv/#_optimizing_load_csv_for_performance
* https://graphacademy.neo4j.com/courses/importing-cypher/

First, let's create constraints, essentially a primary key, for the company and manager node types.  Company keys should be CUSIPs.  We know a CUSIP is unique because that is the whole point of one.  They are identifiers for securities designed to be unique.  You can read more about them [here](https://www.cusip.com).  This is a much better field to use than nameOfIssuer (called companyName here) because it avoids the problem where some companies (like Apple or Apple, Inc.) are referred to by slightly different names.

The manager is a little more difficult.  But, we're going to assume that the manager name field is both unique and correct.

    CREATE CONSTRAINT unique_company_id IF NOT EXISTS FOR (p:Company) REQUIRE (p.cusip) IS NODE KEY;
    CREATE CONSTRAINT unique_manager IF NOT EXISTS FOR (p:Manager) REQUIRE (p.managerName) IS NODE KEY;

That should give this:

![](images/16.png)

Now that we have all the constraints, let's load our nodes.  We're going to do that first and grab the relationships in a second pass.  While we could do it in a single Cypher statement, as we did above, it's more efficient to run them in series.

Let's load the companies first.  We're going to have a lot of duplication, since our key is CUSIP and many different rows in our csv, each representing a filing, have the same cusip.  So, we need to enhance our LOAD CSV statement a little bit to deal with those duplicates.

    LOAD CSV WITH HEADERS FROM 'https://storage.googleapis.com/neo4j-datasets/hands-on-lab/form13-2023.csv' AS row
    MERGE (c:Company {cusip:row.cusip})
    ON CREATE SET c.companyName=row.companyName;

That should give this:

![](images/17.png)

Now let's load the Managers:

    LOAD CSV WITH HEADERS FROM 'https://storage.googleapis.com/neo4j-datasets/hands-on-lab/form13-2023.csv' AS row
    MERGE (m:Manager {managerName:row.managerName});

That should give this:

![](images/18.png)

Well, this is cool.  We've got all our nodes loaded in.  Now we need to tie them together with relationships.  In this case we only need one kind of relationship.  A manager "OWNS" a company.

So, let's add the relationships.

    LOAD CSV WITH HEADERS FROM 'https://storage.googleapis.com/neo4j-datasets/hands-on-lab/form13-2023.csv' AS row
    MATCH (m:Manager {managerName:row.managerName})
    MATCH (c:Company {cusip:row.cusip})
    MERGE (m)-[r:OWNS {reportCalendarOrQuarter:date(row.reportCalendarOrQuarter)}]->(c)
    SET r.value = toFloat(row.value), r.shares = toInteger(row.shares);

This will run for about 2-5 minutes.  When complete, you should see this:

![](images/19.png)

You've done it!  We've loaded our data set up.  We'll explore it in the next lab.  But, feel free to poke around a bit as well.
