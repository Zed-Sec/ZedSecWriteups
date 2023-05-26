# Case 1 - The rarest book is missing!

### Video Walkthrough

{% embed url="https://youtu.be/H4tnbqKWmCY" %}
Kusto Detective Agency - Case 1 Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Case 1 - The rarest book is missing! For this one we're given a bit more of a challenge for the first official case. A book has gone missing, and we have to find it. Start by running the ingestion script to bring in the data we need for this case.

### Key Information

* There's 325,000 rare books.
* They can’t locate the book **De Revolutionibus Magnis Data**, published **1613**, by **Gustav Kustov.**
* Each book has its parameters recorded:
  * Number of pages
  * Weight
* Each book has an RFID tag attached to it.
* Each shelf some data back, which RFID tags appear on its shelf and it measures the total weight of books on the shelf.
* The RFID for the book we're looking for has been found on the floor.
* We need to locate which shelf the book is on.

### Tables

There's two tables that have been ingested by the ingestion script, **Books** and **Shelves**. We can check the columns in a table using the **getschema** operator:

```
Books
| getschema

```

We can do the same for the **Shelves** table too. This gives us the columns for each of the tables:

* Books
  * rf\_id
  * book\_title
  * publish\_date
  * author
  * language
  * number\_of\_pages
  * weight\_gram
* Shelves
  * shelf
  * rf\_id
  * total\_weight

### Walkthrough

We can get an idea of the sample data using the **take** function, this will give us one row from the specified table, you can change the number to grab multiple rows if you want a larger dataset:

```kusto
Books
| take 1
```

If we have the weight of each book, and each shelf adds up to the weight of all the books on the shelf, we should be looking for the shelf that doesn't add up to the right weight. It's just a case of how do we actually go about doing that?

We can find the weight of the missing book by doing:

```
Books
| where book_title == "De Revolutionibus Magnis Data"
```

This gives us the weight of **1764**. So we need to find a shelf with an expected weight that is 1764 different than what is expected.

The below query expands the **rf\_ids** column to break it up into multiple rows instead of all being concatenated in the one entry. Then there’s a **join** on the ID fields to combine the two tables, then the expected weight is calculated based on the individual weight of each book on the shelf. The **actual\_weight** variable is then taken from any of the column since they’re all the same and grouped by the **shelf**. At this point we have the shelf, the weight that is expected on that shelf based on the books we know are on it and then what the real weight is.

An **extend** is then done to create a new column called “difference” which is calculated by subtracting **expected\_weight** from the **actual\_weight** where the difference is more than **1764**, the weight of the missing book:

```
Shelves
| mv-expand rf_ids to typeof(string)
| join Books on $left.rf_ids == $right.rf_id
| summarize 
    expected_weight = sum(weight_gram),
    actual_weight = take_any(total_weight) by shelf
| extend difference = actual_weight - expected_weight
| where difference >= 1764
```

The shelf we're left with is the shelf the book is on and the answer to the case.
