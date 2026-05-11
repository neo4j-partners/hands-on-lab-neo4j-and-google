# Lab 9 - Aura Agent

In the Neo4j Aura console select "Agents."

![](images/01.png)

Click "Create with AI."

![](images/02.png)

Enter this prompt:

    This database contains asset manager nodes.  Those are connected to company nodes by the owns relationship.  I'd like the understand what managers are picking uncommon companies.  I'd also like to understand what managers share these relatively uncommon companies.

![](images/03.png)

Click "Create."

![](images/04.png)

Wait for the agent configuration to complete.

![](images/05.png)

Type in:

    List managers investing in uncommon companies.

![](images/06.png)

Press return.

![](images/07.png)

Review the output.  In this case, I'll answer the question with:

    Let's try 3.

![](images/08.png)

We see a list of such companies.

![](images/09.png)

This is just scratching the surface of what is possible with these agents.  The UI we've used in the Neo4j Aura Console is a great way to get started.  Agents can be incorporated into larger agentic flows through APIs.

Experiment and have fun!
