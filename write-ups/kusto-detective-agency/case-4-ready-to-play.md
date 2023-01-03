# Case 4 - Ready to play?

### Intro

Kusto Detective Agency - Case 4 - Ready to play? In a twist turn of events, we're not even given an ingestion script this time, there's also a bit more sleuthing with this one and the next one.

### Walthrough

Start by ingesting the data we're given:

```
.execute database script <|
.create-merge table Prime_Numbers (Prime:int)
.ingest async into table Prime_Numbers (@'https://kustodetectiveagency.blob.core.windows.net/prime-numbers/prime-numbers.csv.gz')
```

To start off, we've ingested the data, now we've got a table of prime numbers and we need to find the highest special prime number under 100 million.

A prime number is a whole number, greater than 1 that cannot be divided by any other number than itself and 1.

A special prime number is a prime that is considered special if it's prime and can also be represented by the sum of two neighbouring prime numbers or 1.

#### Special Prime Examples

7 + 11 + 1 = 19. So 19 is considered a special prim number

#### Find our special prime number

So I started by serializing the prime numbers. Next we create a column called **Special\_Prime** and add the current prime in the row with the prime number on the previous row, then adding 1 onto it. This creates a list of potential special primes. To find out which are the actual special primes though we need to join them back to the original table. We're going to use an inner join which will only match data in both columns, so if our potential prime isn't in the actual prime numbers list it'll be discarded, leaving us with just a list of special primes.

Now we just filter for less than or equal to 100 million and project 1 column just to clean up our output a bit:

```
Prime_Numbers
| serialize Prime
| project Special_Prime = prev(Prime) + Prime + 1
| join kind=inner (Prime_Numbers) on $left.Special_Prime == $right.Prime
| where Special_Prime <= 100000000
| top 1 by Prime desc
| project Special_Prime
```

#### The clue

We can now go to [https://aka.ms/99999517](https://aka.ms/99999517).

We're basically given another ingestion script that we need to take a look at along with a riddle:

**Across the Big Apple city, there is a special place with Turkish Hazelnut and four Schubert Chokecherries within 66-meters radius area. Go 'out' and look for me there, near the smallest American Linden tree (within the same area). Find me and the bottom line: my key message to you.**

Once you've run the new ingestion script we've basically got a new table of NYC trees and two functions, **Decrypt** and **VirtualTourLink.**

We can start by looking at the nyc\_tree table that we've ingested:

```
nyc_trees
| limit 1
```

There are so many columns that I'm not going to write them out. So we need to write a query that's going to find the one Turkish Hazlenut tree and foute Schubert Chokebcherries within a 66-metre radius.

Our second hint is:

**Geo-hashing fun fact: H3 cell with size of 10 is about 66m in radius.**

With the second hint in mind the below query finds all instance of 4 Schubert and 1 Turkish trees within a 66m radius,

```
nyc_trees
| extend h3cell = geo_point_to_h3cell(longitude, latitude, 10)
| summarize Count_Schubert=countif(spc_common contains "Schubert"), Count_Turkish=countif(spc_common == "Turkish hazelnut") by h3cell
| where Count_Schubert == 4 and Count_Turkish == 1
```

We can then do the below to grab the co-ordinates of the trees:

```
print h3cell = geo_h3cell_to_central_point("8a2a100dec9ffff")
```

Then we can use the **VirtualTourLink** function to get a Google Maps link.

```
VirtualTourLink(40.71222313,-73.96452201)
```

We see in the Google street view that there's a mural "ASHES to ASHES" is painted on it. We know this is the hint we’re looking for because in the Kusto email intro for the task we see it’s from El Puente.

No we need to decrypt the message given in the task then pass in ASHES to ASHES as the key which will give us the output we’re after:

```
print Decrypt(@"20INznpGzmkmK2NlZ0JILtO4OoYhOoYUB0OrOoTl5mJ3KgXrB0[8LTSSXUYhzUY8vmkyKUYevUYrDgYNK07yaf7soC3kKgMlOtHkLt[kZEclBtkyOoYwvtJGK2YevUY[v65iLtkeLEOhvtNlBtpizoY[v65yLdOkLEOhvtNlDn5lB07lOtJIDmllzmJ4vf7soCpiLdYIK0[eK27soleqO6keDpYp2CeH5d\F\fN6aQT6aQL[aQcUaQc[aQ57aQ5[aQDG","ASHES to ASHES")
```

And we're given the following, which is our final answer for this one:

```json
wytaPUJM!PS:2,7,17,29,42,49,58,59,63
```
