
**It is more important to follow one style consistently than trying to find the best style.**


[What is correct Java naming convention for id? - Stack Overflow](https://stackoverflow.com/questions/1699944/what-is-correct-java-naming-convention-for-id)

```
I think I read somewhere that the best guideline is to always capitalize _only_ the first letter of an acronym (i.e., if you have a user TTL where TTL is some random acronym in your project, then it's best to write userTtl).

This makes sense, since it solves some problems. For example, say you want a user id counter. Readability of userIDCounter is worse than userIdCounter. For a longer acronym, it gets even worse.
```

Abbreviations in camelCase   : 

Try to be consistent or else a good coding standard is 👇

```
Whatever you do, be consistent. Consistency is the important part.
Seeing `UserID` and `ProductId` in the same codebase is strange.
```

[Capital Offense: How to Handle Abbreviations in CamelCase - Approxion](https://www.approxion.com/capital-offenses-how-to-handle-abbreviations-in-camelcase/)
In some cases, an abbreviation is written all uppercase, in other cases only the initial character is capitalized. To avoid such mixes, some coding conventions, like Python's PEP-8,  try to cure this by giving explicit advice.

*When using abbreviations in CapWords, capitalize all the letters of the abbreviation. Thus HTTPServerError is better than HttpServerError.*

But this is incorrect 👆, It works in simple cases, it leads to abominations when one abbreviation follows another: 

```
HTTPURLConnection
XMLIDREF
```

The only convention that works is, "Treat abbreviations just like ordinary words". That is don't use capital letters at all,

```
HttpException
HttpUrlConnection
XmlFormatter
XmlId
XmlIdRef
```

This works also if identifiers have to start with a small letter (e.g. names of local variables)

```
httpException
httpUrlConnection
xmlFormatter
xmlId
xmlIdRef
```



* This is the best option -- initialisms should only have their first letter capitalised. `HtmlDocument` is much more readable than `HTMLDocument` because it is more clear where the second word begins.

* What if the abbreviation is IPP, then IPPProvider doesn't make sense, but IppProvider does

Issues with Capital:
1. Multiple abbreviations in the same word create confusion
2. HtmlDocument is more readable than HTMLDocument, IppProvider is more readable than IPPProvider
3. can use it with local variable names also
4. MS has a nuance 
5. Microsoft says all capital letters if it's 2 letters or less. If it's 3 letters or more then it's only the first letter capital and rest lowercase.
