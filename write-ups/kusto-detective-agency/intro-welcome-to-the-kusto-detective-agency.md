# Intro - Welcome to the Kusto Detective Agency

### What is Kusto Detective Agency?

So, Kusto Detective Agency is a set of challenges and puzzles that need to be solved using Kusto Query Language (KQL). It's basically a language for querying sets of data. The main area that I use this is when querying Microsoft Sentinel logs. But we won't be using Sentinel or a Log Analytics Workspace for these challenges, we'll be using Azure Data Explorer.

### Getting Started

To start, you're going to want to head over to [https://detective.kusto.io/](https://detective.kusto.io/) and you'll be met with some basic instructions for getting started. Follow the instructions to:

* Create a free Kusto cluster which will be used throughout the tasks.
* Copy the Cluster URI, this will be needed later in this task.
* Paste the ingestion script into the query editor and run it to ingest the data.

### Enter the sum of the "Score" column

Once you've created an account and ingested the data, the first challenge we're met with is to find the sum of the score column. We're going to use the **sum** operator to add up all of the rows in the score column. This can be done with the below query:

```
Onboarding
| summarize sum(Score)
```

The output for the above query is the answer. That's us for the intro case, case 1 is up next, where things get a bit more complicated.
