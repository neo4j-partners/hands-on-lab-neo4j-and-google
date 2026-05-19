# Lab 8 - User Neo4j Agent

We deployed Neo4j Agent into our Gemini Enterprise instance.  Now let's use it.

Continuuing where we left off, click on "Overview" on the left.

![](images/01.png)

We're now back at the main Gemini Enterprise screen.  Click "Open preview" in the upper right.

![](images/02.png)

This gives us a chat window where we can interact.  Click "Get started."

![](images/03.png)

Click "Agents."

![](images/04.png)

Click the three dots above the Neo4j Agent.

![](images/05.png)

Click "Pin."  This will pin the Neo4j Agent to the menu, making it easier to find.

![](images/06.png)

Click on the Neo4j Agent.

![](images/07.png)

We're finally there!  Let's pause for a moment and think about what we have...

We've got a chat window to Gemini Enterprise.  That is using [Agent2Agent (A2A)](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/) to speak with the [Neo4j MCP Server](https://github.com/neo4j/mcp) running in a SaaS wraper.  The SaaS wrapper is essentially a Google Cloud Function with auth syntax and such on top.

The agent is connected to a Neo4j Aura instance.  That instance has the SEC data from the earlier query loaded into it.  Note that all your classmates are connected to this same Aura isntance.  So any writes you make will change their reads.

I'm going to do something rather simple to start.  I'll enter this prompt.

    Make a node called Bob.

![](images/08.png)

Then hit enter.

![](images/09.png)

Click "Authorize."

![](images/10.png)

Select the Vocareum user that you have been using.

![](images/11.png)

Scroll down.

![](images/12.png)

Click "Continue."

![](images/13.png)

Alright.  Now we're authorized.  Gemini Enterprise does a lazy authorization for agents.  So, it only attempted it once we submitted a prompt.

Now it's thinking...

![](images/14.png)

And there!  We have a brand new node.  Note that if someone else also made Bob, it'll just overwrite the existing node.

Now let's make sure it's there.  Type:

    List nodes with name "Bob"

![](images/15.png)

Hit enter.

![](images/16.png)

Eureka!  We found a node named Bob.

This being a graph database, with rather a lot of data from the SEC in it, we can probably do some more interesting things.  Here's one idea:

    What companies are owned by three or more managers?

![](images/17.png)

Hit enter.

![](images/18.png)

We see a bunch of companies.

![](images/19.png)

Some other ideas for queries include:

* What manager owns the most companies?
* What manager owns the least companies?
* Which managers own Exxon?

Feel free to play around, though please don't nuke the database as everyone else is using it to.