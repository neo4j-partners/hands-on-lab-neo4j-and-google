# Lab 7 - Deploy Neo4j Agent

In this lab we're going to use the Neo4j Agent in Google Cloud Marketplace with Gemini Enterprise.

The agent is an MCP server that can interact with a Neo4j Aura instance.  It can perform CRUD operations available through the Cypher language.  The agent takes natural language as input and converts that to the appropriate Cypher before passing the query to Neo4j Aura.

The Agent is available in the Google Cloud Marketplace.  It's wrapped in the Agent to Agent (A2A) protocol.  This means we can deploy it within a Gemini Enterprise environment.

So, let's get started.  You can open the Neo4j Agent listing [here](https://console.cloud.google.com/marketplace/product/neo4j-mp-public/neo4j-agent).  

![](images/01.png)

Our adminsitrator has already subscribed to this listing for us.  So, let's go set it up in Gemini Enterprise.  Navigate to the cloud console [here](https://console.cloud.google.com/).

Type "Gemini Enterprise" in the search bar.

![](images/02.png)

Click on the "Gemini Enterprise" product result.

![](images/03.png)

Click "Start 30-day free trial."

![](images/04.png)

Click "Continue and activate the API."

![](images/05.png)

That will run for a minute...

![](images/06.png)

Dismiss the "You have successfully onboarded to Gemini Enterprise" dialog.

![](images/07.png)

Click "Create."

![](images/08.png)

Dismiss "App created successfully."

![](images/09.png)

Click on "Agents" in the menu on the left.

![](images/10.png)

Click "+ Add Agent."

![](images/11.png)

On the "Agents via Marketplace" tile click "Add."

![](images/12.png)

Select "Neo4j Agent by Neo4j" and click "Next."

![](images/13.png)

Click "Next."

![](images/14.png)

Click "Finish."

![](images/15.png)

When complete, you should be redirected.  Dismiss the "Your agent was completed successfully" dialog.

![](images/16.png)

Great!  Our agent is now installed in our Gemini Enterprise instance.

![](images/17.png)

The next step is to configure the agent.  We can do that at the setup page [here](https://graphrag-gcp.neo4j.agency/setup).

![](images/18.png)
