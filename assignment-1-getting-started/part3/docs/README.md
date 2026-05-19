# Lab 2 - Deploy Neo4j

There are a number of options for deploying Neo4j on Google Cloud Marketplace (GCMP):

* [Neo4j Community Edition](https://console.cloud.google.com/marketplace/product/neo4j-mp-public/neo4j-community-edition)
* [Neo4j Enterprise Edition](https://console.cloud.google.com/marketplace/product/neo4j-mp-public/neo4j-enterprise-edition)
* [Neo4j Aura](https://console.cloud.google.com/marketplace/product/neo4j-mp-public/neo4j-aura)

CE and EE are self managed versions of the product.  The marketplace listing deploys infrastructure in your account, including virtual machines.  Scripts then install and configure Neo4j.

Aura is a SaaS version of Neo4j.  That is managed entirely by Neo4j so no infrastructure administration is required.  We're going to use that version.

So, let's get started deploying...  Be sure your [Google Cloud Console](https://console.cloud.google.com/) is open from the last lab.  In the search bar, type "Neo4j Aura."

![](images/01.png)

Select the "Neo4j Aura" product.  That is the top result in this screenshot.

![](images/02.png)

This will take you to the Neo4j Aura marketplace listing.  The Vocareum organization we're part of has already subscribed to this listing.  If you were in an organization that had not subscribed you would see a "Subscribe" button.

Since we already have an active subscription, we can click "Manage on Provider."

![](images/03.png)

You'll see a dialog stating that we're leaving Google Cloud.  That is because we're punching out of the marketplace into the Neo4j Aura Console.  Click "OK."

![](images/04.png)

We're now on the auth page for Neo4j Aura.  Click "Accept Cookies" to dismiss the dialog.

![](images/05.png)

Neo4j supports a number of different auth providers, including Google, GitHub and Microsoft.  We've already authenticated with Google for the console.  So, click on the "Continue with Google" button to carry those credentials through to Neo4j Aura.

![](images/06.png)

Click on your Vocareum account name to continue.

![](images/07.png)

Click "Continue."

![](images/08.png)

Now we are in the Aura Console.  Click on "GCP marketplace project."

![](images/09.png)

You'll then be presented with a dialog to gather information about your use case.  For "Company / Institution" you can enter "Vocareum" and click "Next."

Note that we're starting to build a labeled property graph describing our use case.

![](images/10.png)

Click "Build a graph-powered application."  After all, we're going to be building some agent powered applications on top of Neo4j!

![](images/11.png)

Click "Data Scientist."  Even if that's not your job title, you are today.  We'll be using Graph Analytics!

![](images/12.png)

Now click "Generative AI."  We're going to be using Google Gemini Enterprise to build agents.

![](images/13.png)

We're now presented with a choice of product tiers within Neo4j:

* Free
* Business Critical
* Professional

The Free tier is a great way to get started experimenting.  Business Critical offers a 3 node fault tolerant and highly available cluster.  We don't really need that for this lab.  The Professional tier has similar functionality with a single node.  Select "Professional."

![](images/14.png)

Vocareum and Neo4j Aura are currently interacting in a somewhat undesirable manner.  The Neo4j Aura Organizations and Projects are viewable to everyone within this Vocareum course.  While each user has their own username and project, they all share a single billing account.  We're working on improving this.

In the meantime, please name you instance using your Vocareum username.  That will allow you to distinguish your Neo4j Aura instances from those belonging to your classmates.

In my case, I set my instance name to user1684365460481394.

![](images/15.png)

Now, let's inspect the other options.


![](images/16.png)

We're going to load a fair about of data, so need to bump the amount of RAM from 4GB to 8GB.  Do that.

![](images/17.png)

We can deploy in different regions.

There are two options for Graph Analytics.  This feature provides access to 60+ graph alogrithms.  These run across your graph, computing things like centrality and node importance.  We'll keep the default.  That spins up computations on demand.  Another option is to collocate it in the database.

Finally, there's an option to optimize the database for vector search.  We'll be using vector functionality but our workloads will be comparatively light so we don't need this optimization.

We've reached the bottom!  Click "Create Instance."

![](images/18.png)

You'll be presented with the credentials for your database.  Click "Download and continue."  That will download the credentials to a text file on your local machine.  

![](images/19.png)

A save dialog should pop up.  Be sure to save that file as you won't be able to get those credentials later.

![](images/20.png)

You'll see a dialog that your database is being created. This should only take a few minutes.

![](images/21.png)

When deployment is complete you'll see the instance details in the management console.  

![](images/22.png)

You can poke around the menus here a bit and see more on database status and connection information.

You now have a deployment of Neo4j AuraDB Professional running!  In the next lab, we'll connect to it.
