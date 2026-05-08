# hands-on-lab-neo4j-and-google

Neo4j is the [leading graph database](https://db-engines.com/en/ranking/graph+dbms) vendor.  We’ve worked closely with Google Cloud engineering for years.  Our SaaS database, Neo4j Aura, is offered as a managed service on Google Cloud.  [This is available through the Google Cloud Marketplace](https://console.cloud.google.com/marketplace/product/neo4j-mp-public/neo4j-aura).

In this hands on workshop, you’ll get to learn about [Neo4j](https://neo4j.com/) and [Google Cloud Gemini Enterprise](https://cloud.google.com/gemini-enterprise).  The lab is intended for data scientists and data engineers.  We’ll walk through deploying Neo4j and Gemini Enterprise in a Google Cloud account.  Then we’ll get hands on with a real world dataset.  We'll use both traditional and AI approaches to parse and load data.  Then we'll show how to build AI agents that leverage the knowledge graph.  You’ll come out of this lab with enough knowledge to apply graph AI to your own datasets.

We’re going to analyze the quarterly filings of asset managers with $100m+ assets under management (AUM).  These are regulatory filings made to the Securities and Exchange Commission’s (SEC) EDGAR system.  We’re going to show how to load that data from a Google Cloud Storage bucket into Neo4j.  We’ll then explore the relationships of different asset managers and their holdings using the Neo4j Query and Explore.

If you’re in the capital markets space, we think you’ll be interested in potential applications of this approach to creating new features for algorithmic trading, understanding tail risk, securities master data management and so on.  If you’re not in the capital markets space, this session will still be useful to learn about building agentic AI pipelines with Neo4j and Gemini Enterprise.

## Venue

These workshops are organized onsite in a Google office.

## Duration

3 hours.

## Prerequisites

You'll need a laptop with a web browser.  Your browser will need to be able to access the Google Cloud Console and port 7474 on a Neo4j deployment running on Google Cloud.  If your laptop has a firewall you can't control, you may want to bring your personal laptop.

## Agenda

### Part 1

* Introductions
* Lecture - [Introduction to Neo4j](https://docs.google.com/presentation/d/1WvPzs_JEh8uuKEAQGecH1rUd1NoRzqZIKc-hQkuBdXQ/edit?usp=sharing) (10 min)
  * What is Neo4j?
  * How is it deployed and managed on Google Cloud?
* [Lab 0 - Sign In](Lab%200%20-%20Sign%20In) (5 min)
  * Improving the Labs
  * Sign into Google Cloud
* [Lab 1 - Deploy Neo4j](Lab%201%20-%20Deploy%20Neo4j) (15 min)
  * Deploying Neo4j Aura Professional
* [Lab 2 - Connect to Neo4j](Lab%202%20-%20Connect%20to%20Neo4j/README.md) (10 min)
* Break (5 min)

### Part 2

* Lecture - [Moving Data](https://docs.google.com/presentation/d/1O6Oy_GbDYYCvQanUyUCl30hQdSsy9kKL53Jgl23Nnsk/edit?usp=sharing) (10 min)
  * LOAD CSV
  * Neo4j Aura Importer
  * Apache Beam and Google Dataflow
  * Apache Spark and Google Dataproc
  * Apache Kafka and Cloud Cloud
* [Lab 3 - Moving Data](Lab%203%20-%20Moving%20Data/README.md) (15 min)
  * Simple Load Statement
  * More Performant Load
* [Lab 4 - Exploration](Lab%204%20-%20Exploration/README.md) 10 min)
  * Exploration with Neo4j Explore
* Break (5 min)

### Part 3

* Lecture - [Gemini Enterprise](https://docs.google.com/presentation/d/1BowFoowrk0pTVqdScC4weBFZJ-xMTdHbvMUCW4ZyP68/edit?usp=sharing) (15 min)
  * What is Gemini Enterprise?
* Lecture - [Neo4j and AI](https://docs.google.com/presentation/d/1vVII1F9RgcFiQ8Pxd2RQUursZiqqbkpIG798sn-HWgU/edit?usp=sharing) (15 min)
  * Generating Knowledge Graphs
  * Retrieval Augmented Generation
  * Using Gemini Enterprise with Neo4j
* Lab 5 - Document Intelligence (20 min)
* Lab 6 - Neo4j Agent (20 min)
* Lab 7 - XXX (20 min)
* [Questions and Next Steps](Questions%20and%20Next%20Steps.md) (5 min)
