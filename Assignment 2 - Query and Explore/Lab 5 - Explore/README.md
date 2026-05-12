# Lab 5 - Explore

In this lab, we'll use Explore, Neo4j's business intelligence (BI) tool, to explore our data.

Click on the 'Explore' option in the left menu under Tools.

![](images/01.png)

Now click on "Show me a graph."

![](images/02.png)

In this case, we got a view with a manager and a company node in the middle and then some surrounding nodes.

We can mouse over the company to see its name.

![](images/03.png)

Now let's try finding a new graph.  Click in the search bar.

![](images/04.png)

Select "Manager."

![](images/05.png)

Now select "OWNS."

![](images/06.png)

Now select "Company"

![](images/07.png)

Now hit press return.

![](images/08.png)

That gives us search results for paths that go from Manager to Company.  We hit a limit of 1000, so it's not visualizing everything.

Next, we will apply some point-and-click data science to our graph.  Click on the atom icon to open the data science menu.

![](images/09.png)

Click "+ Add" to add an algorithm.

![](images/10.png)

Click on "Select" to open the algorithm drop down.

![](images/11.png)

Select "Degree Centrality."

![](images/12.png)

Click "Apply."

![](images/13.png)

This spins up an additional ephemeral instance running Neo4j Graph Analytics.  That takes a few minutes.

![](images/14.png)

Once it is running, we see this view.  We can choose how we want to visualize the results in the graph.  

Choose "Size scaling."

![](images/15.png)

That gives us this.  The more central nodes in our graph are now shown as larger.

We can close the data science panel to get a better view.  Do that by clicking the icon above "Analytics Session Running."

![](images/16.png)

That gives us a better view of the differently sized nodes.

![](images/17.png)

These are just a few examples of what you can do with Bloom.  Feel free to explore!
