# Lab 6 - Document Intelligence

Document Intelligence is a new tool within Neo4j Aura.  It's currently in a private preview.  We've enabled your account for this lab with it.

Document Intelligence transforms documents into knowledge graphs stored in Neo4j.  It's an evolution of an approach Neo4j has been pioneering with AI since 2022.  Early integrations focused on using [Langchain to build these architectures](https://cloud.google.com/blog/topics/partners/build-intelligent-apps-with-neo4j-and-google-generative-ai).  Many of our customers using AI to create knowledge graph continue to use this approach.  It's code heavy and deeply customizable.

More recently Neo4j Labs, our experimental department, built a [LLM Graph Builder application](https://neo4j.com/labs/genai-ecosystem/llm-graph-builder/) that packaged this approach in a nice UI.

Document Intelligence is the next evolution of this, built into our Neo4j Aura product.

First off, download [this pdf](https://storage.googleapis.com/neo4j-datasets/hands-on-lab/Apple_10-K_2025_2_pages.pdf) and take a peek at it.  It's 2 pages of the 2025 10-K filed by Apple.  We're going to generate a knowledge graph from it.

![](images/01.png)

Now, let's go to our Neo4j Aura Console.  In the left menu, click on "Document Intelligence."

![](images/02.png)

Click "Create graph model."

![](images/03.png)

Click "Add data source."

![](images/04.png)

Click "Local files."

![](images/05.png)

Select the file "hands-on-lab_Apple_10-K_2025_2_pages.pdf"

![](images/06.png)

Now click "Generate model."

![](images/07.png)

For the promp enter:

    Extract products, services, segments and competition.

![](images/08.png)

Click "Save."

![](images/09.png)

The generator will run for a bit.

![](images/10.png)

When complete, you'll see a neat graph model.  You can zoom in and around, inspecting it.

When you're done, click "Graph preview."

![](images/11.png)

We can explore the model a bit, zooming in and inspecting.  

![](images/12.png)

Click the icon in the upper right of the graph to expand the view.

![](images/13.png)

Explore a bit more...

![](images/14.png)

We can see the node for the home category includes streaming and wireless devices such as the HomePod, HomePod mini and Apple TV.

![](images/15.png)

For the full graph query functionality, we would need to import this into a Neo4j instance.  Support for that feature went live on Aura Pro and BC 5/14.  So, we haven't had a chance to work it into the lab material yet.  Feel free to experiment though!

We really hope you enjoyed this preview of Document Intelligence.  Please stay tuned for the full release and updates!
