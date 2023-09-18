# Case 6 - Hack this rank!

### Video Walkthrough



{% embed url="https://youtu.be/A98vZaYLGkw" %}
Kusto Detective Agency - Season 2 - Case 6 - Hack this rank! - Video Walkthrough
{% endembed %}

### Intro

Kusto Detective Agency - Season 2 - Case 6 - Hack this rank!

This is another week where I'm going to say this was the toughest one yet. I had to look some hints up myself to nudge me in the right direction, just when I was getting more confident in KQL this week came along. Thanks to the following people for posting their guides online, wouldn't have been able to solve it without them:

* **Aviv Yaniv** - [https://medium.com/courisity-is-a-drug/walk-through-guide-for-kusto-detective-agency-season-2-case-6-solution-ce91f338b8de](https://medium.com/courisity-is-a-drug/walk-through-guide-for-kusto-detective-agency-season-2-case-6-solution-ce91f338b8de)
* **Th3Tul1p3** - [https://github.com/Th3Tul1p3/Kusto\_detective\_agency\_season2\_writeup/blob/main/Case\_5.kql](https://github.com/Th3Tul1p3/Kusto\_detective\_agency\_season2\_writeup/blob/main/Case\_5.kql)

### Walkthrough

The main points for this case:

* We've got a list of art gallery paintings and an encoded string. We need to find the key to decode the string and decode the message.
* The message will be a riddle which will give us some hints on which key-words we're looking for.
* Once you've got the words this will allow us to find an image which will help us find the passcode to log into [https://kuanda.org/](https://kuanda.org/).

### Decoding the string:

We've been given the following text string:

```
12204/497 62295/24 50883/678 47108/107 193867/3,
45534/141 hidden 100922/183 143461/1 1181/505 46187/380.
41526/155 66447/199 30241/114, 33745/154 12145/387 46437/398 177191/131:
293/64 41629/1506 210038/432, 41612/803 216839/1.

404/258 rules 40/186 1472/222 122894/2 46081/105:
41594/650 32579/439 44625/141 184121/19 33254/348 357/273 32589/821,
46171/687 punctuations 62420/10 50509/48 1447/128,
176565/82'56721/591 561/225 insensitive, 30744/129 76197/32.

1319/42 41599/216 68/457 136016/146, 42420/126'46198/389 42429/158 40091/108 41667/252,
1515/555 177593/223 176924/73 45889/65 159836/96 35080/384 32578/199.
1607/167 124996/9 71/56, 1303/187 45640/1114 72328/247 75802/11,
1168/146 163380/12 57541/116 206122/738 365/267 46026/211 46127/19.

119295/425 45062/128 12198/133 163917/238 45092/8 54183/4 42453/82:
561/433 9/387 37004/287 1493/118 41676/38 163917/238 3159/118 63264/687
1/905 1493/109 43723/252, 136355/1 1159/134 40062/172 32588/604,
158574/1 45411/8 10/892 127587/175 - 633/9 72328/247 1514/615 42940/138.

164958/84 221014/479 151526/7 111124/138, 41668/206 34109/46 1514/555,
147789/2 3228/152 993/323 166477/167 178042/167, 50753/91'207786/8 12/372.
1108/158'42423/150 12/309 66154/9 213566/11 44981/158 1197/300
40184/149 92994/63-71071/179 75093/7 211718/18 74211/5 46144/399.
```

The key for this string when looking at the **NationalGalleryArt** table is in the form of **ObjectID:Index** where **ObjectID** == **ObjectID** and **Index** == The number of character you need to extract from the field **ProvenanceText**.

Taking the first encoded string **12204/497**. If you filter by **ObjectID** **12204** we can pull out the **497th** character which would be **The**.

So let's make this a little easier to decode.

````kusto
// Set encoded string
let encodedMessage =
```12204/497 62295/24 50883/678 47108/107 193867/3,
45534/141 hidden 100922/183 143461/1 1181/505 46187/380.
41526/155 66447/199 30241/114, 33745/154 12145/387 46437/398 177191/131:
293/64 41629/1506 210038/432, 41612/803 216839/1.

404/258 rules 40/186 1472/222 122894/2 46081/105:
41594/650 32579/439 44625/141 184121/19 33254/348 357/273 32589/821,
46171/687 punctuations 62420/10 50509/48 1447/128,
176565/82'56721/591 561/225 insensitive, 30744/129 76197/32.

1319/42 41599/216 68/457 136016/146, 42420/126'46198/389 42429/158 40091/108 41667/252,
1515/555 177593/223 176924/73 45889/65 159836/96 35080/384 32578/199.
1607/167 124996/9 71/56, 1303/187 45640/1114 72328/247 75802/11,
1168/146 163380/12 57541/116 206122/738 365/267 46026/211 46127/19.

119295/425 45062/128 12198/133 163917/238 45092/8 54183/4 42453/82:
561/433 9/387 37004/287 1493/118 41676/38 163917/238 3159/118 63264/687
1/905 1493/109 43723/252, 136355/1 1159/134 40062/172 32588/604,
158574/1 45411/8 10/892 127587/175 - 633/9 72328/247 1514/615 42940/138.

164958/84 221014/479 151526/7 111124/138, 41668/206 34109/46 1514/555,
147789/2 3228/152 993/323 166477/167 178042/167, 50753/91'207786/8 12/372.
1108/158'42423/150 12/309 66154/9 213566/11 44981/158 1197/300
40184/149 92994/63-71071/179 75093/7 211718/18 74211/5 46144/399.
```;

// Split objectID and index
let rawKey =
NationalGalleryArt
| extend extractWords = extract_all(@"(\w+)/(\w+)", encodedMessage)
| mv-expand with_itemindex=Order extractWords
| extend objectID = tolong(extractWords[0]), index = tolong(extractWords[1])
| summarize by objectID, index;

// Translate the encoded value to the extracted word
NationalGalleryArt
| join kind=inner (rawKey) on $left.ObjectId == $right.objectID
| project ObjectId, Title, ProvenanceText, index
| extend ExtractedWords = extract_all(@'(\w+)', ProvenanceText)
| extend ExtractedWords = ExtractedWords[index]
| project ObjectId, index, ExtractedWords
| project ExtractedWords, EncodedValue = strcat(tostring(ObjectId), "/", tostring(index))
```
````

The above query will set the **encodedMessage** variable. The next block will split each word of the encoded message into two separate columns, the **ObjectID** and **Index**.

The third block in the example will map each part of the encoded message to the corresponding word. From here we're meant to write some regex to switch each word in the original text with the right words. By this point I was over 10 hours over the weekend into playing about with this and just assembled it myself. My regex for initial extracting is slightly flawed so a few of the words aren't entirely accurate, but it's enough to get the key parts of the riddle. Here is the assembled version:

```
in catalogue of titles Grand
three words Demand your Hand
when found all they form Aline
A clear timeline simply Fine

words are simple to Review
at least three Letters have in view
all Mark the End
theyre case my friend
to find all words youll need some skill
seeking the popular will guide you still
below The King the first word mounts
the Second shares with Third their counts
reveal the last word with Wise thought
take first two letters from most sought
into marked dozen and change just one
and with those two the is done
so search the titles high and low
and when you find it youll know
youve picked the Image that revealed
the pass code to the World concealed
```

It's a nasty riddle that had me down a bunch of different paths. I thought that the line about the King mounting was a reference to chess, maybe the knight piece that uses a horse? But, not quite. Here's the key things we're looking for from the riddle:

* Three words.
* Each word has at least three letters.
* Search by the most popular words.
* Look for the next most popular word after **King**
* The words are case-insensitive.
* The second and third shares their counts.

The first word is **Day.**

```kusto
NationalGalleryArt
// Case insensitive
| extend formatTitle = tolower(Title)
| extend titleWord = extract_all(@'(\w+)', formatTitle)
| mv-expand titleWord
| extend length = strlen(titleWord)
// Filter out words shorter than 3 letters
| where length >= 3
// Count the words and sort by the count
| summarize countWord = count() by tostring(titleWord)
| sort by countWord
```

The second word is shares the same count as **third.** The following query finds the counts for the word **third** which turns out to be **161**:

```kusto
// Find the count for the word third
NationalGalleryArt
// Case insensitive
| extend formatTitle = tolower(Title)
| extend titleWord = extract_all(@'(\w+)', formatTitle)
| mv-expand titleWord
| extend length = strlen(titleWord)
// Filter out words shorter than 3 letters
| where length >= 3
| where titleWord == "third"
// Count the words and sort by the count
| summarize countWord = count() by tostring(titleWord)
| sort by countWord
```

Then we find all words with **161** counts. Out of the returned results our answer is **year** because the words share a common theme:

```kusto
// Find words with the same count
NationalGalleryArt
// Case insensitive
| extend formatTitle = tolower(Title)
| extend titleWord = extract_all(@'(\w+)', formatTitle)
| mv-expand titleWord
| extend length = strlen(titleWord)
// Filter out words shorter than 3 letters
| where length >= 3
// Count the words and sort by the count
| summarize countWord = count() by tostring(titleWord)
| sort by countWord
| where countWord == 161
```

Finally the most common word is **The** so the first two letters are **Th**. The 12th most common word is **man,** apparently this makes out word **month**, though I'm not sure why. I got a bit lost in the sauce trying to find the meaning for the last word, but let's put them all together to find the image URL.

The following will output the image URL:

```kusto
NationalGalleryArt
| where Title has_all ("day", "month", "year")
```

That gives us a link which provides the following image:

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption><p>Image hint</p></figcaption></figure>

Head on over to - [https://kuanda.org/login](https://kuanda.org/login) and paste the image URL into the second box:

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

You need to start at the Octopus eye and follow the tentacles counter-clockwise, this spells **STOPKUSTO** which is the passcode. When you sign in you'll find an email signed off by the big leader **Krypto**.

That's it for this case!
