---
title: 'Google Search Operators - 2022'
date: 2022-01-11 16:00:00
description: 'In this blog post, the 2022 Google Search Operators are listed and explained in detail. These are all working in 2022.'
featured_image: '/images/negative-space-aerial-pacific-ocean.jpeg'
accent_color: '#08877d'
---

# Google Search Operators \- 2022

<br />

As motivation, a reminder of what the goal is with the list of hits returned by any search engine:


> The goal with Information retrieval is the efficient
>	recall of information that satisfies a user’s
>	information need.


**In other words:** Return hits to the user, that give him the information he was looking for with his query.

This is an up to date list of the 'basic' google **search operators**, that are *working* in 2022.
Since these make up most of the **search operators** or even all, that one *should* know in order to make their
*google searches* more efficient and more relevant, these operators will be simply be called **search operators**
in the following.
There have been quite big changes to the names of a number of operators in this list over the last year.
That is part of why I decided to write this post.


Here are the google **search operators** that can be used in the search field of [google.com](http://google.com) and
any country specific extension of google search as well. The **search operators** always have to be written in English in order to be invoked. One can specify their value in another language though.


**Disclaimer:** In some examples the timeframe for how old results are allowed to be is set to 1 year. This can be seen in the examples with images showing the result list. This is chosen, as oftentimes results older than one year are irrelevant by now. The exception to this are queries that specify something that is not of a timely manner. This can be for example *stack overflow* questions and answers or topics that have relevant matches further back in the past, newspaper articles for example. This is relevant for reproducibility of results.



## Google Search Operators List


### Exact Match \" \"

**"\<search term>"** Forces google to only return hits, that contain the exact match \<search term>. The syntax is:

`"<search_term>"` or equivalent `'<search_term>'`

The quotation marks have to be immediately before and after the end of the search term or immediately before the first word and immediately after the last word in a multi word search term.
Spaces between words are allowed, as long as they are supposed to be matched exactly as well. The following examples show the effect that various uses of  the quotation marks have on how restrictive the query is for the web search algorithm:

```text

```

This is probably the single most powerful operator. Takes some practice to find the line between narrowing down the hits google returns too much and the returned hits not being specific enough.

There is no difference between single and double quotes for anything one writes in the search bar or in an **HTML** environment for that matter, as quoted from *Stack Overflow*:

![Single vs Double Quotes](/blog/images/single-vs-double-quotes.png)

### Logical *OR*

Acts as a logical OR and therefore will allow google to return all hits, where \<search term 1> or \<search term 2> have a match and as such, where both search terms are matched as well.

This operator will force one to quickly having to use parenthesis around the alternative search terms and so can become cumbersome, when used in longer queries.

#### Example *OR*

 - Information to gain with the search query about different generations of BMW 3 Series.
 - Precisely for chassis codes *E36*, *E46*, *E90*
   - E36: 3 Series, 1992–1999 (third generation)
   - E46: 3 Series, 1999–2006 (fourth generation)
   - E90: 3 Series, 2005–2011 (fifth Generation)
 - We want to know which generation is the most reliable in general.

We run this query in the [google.com](https://google.com) search field:

```text
most reliable generation "E36" OR "E46" OR "E90" "3 series"
```

We do get [relevant hits with it, that look promising.](https://www.google.com/search?q=most+reliable+generation+%22E36%22+OR+%22E46%22+OR+%22E90%22+%223+series%22&client=firefox-b-d&biw=1413&bih=1080&tbs=qdr%3Ay&ei=ydveYaHlDZHTkgXmx4SgAg&ved=0ahUKEwjh7azprKz1AhWRqaQKHeYjASQQ4dUDCA0&uact=5&oq=most+reliable+generation+%22E36%22+OR+%22E46%22+OR+%22E90%22+%223+series%22&gs_lcp=Cgdnd3Mtd2l6EAMyBQghEKABOgcIABBHELADOgcIIRAKEKABOgQIIRAVSgQIQRgASgQIRhgAUMUNWNcwYJkzaAFwAngAgAGpAYgByQmSAQMzLjiYAQCgAQHIAQjAAQE&sclient=gws-wiz)

![Article about which 3 Series is/was the most reliable historically](/blog/images/article-about-which-3-series-is-was-the-most-reliable-historically.png)

[Link to Search Result in image above.](https://www.vehiclehistory.com/articles/which-bmw-3-series-is-the-most-reliable)

### Logical *AND*

**AND** is the logical *AND*. It forces google to only include results where the search term or what is written inside parenthesis `()` before **AND** and the search term or what is written inside parenthesis after **AND** are both matched.

#### Example *AND*
In the following, the goal is to find information about the Chassis Code of BMW Series 3 cars, produced in 1992. Which tells what generation these cars belong to.

```text
BMW 3 Series Chassis code AND 1992
```
First [result](https://www.google.com/search?q=BMW+3+Series+Chassis+code+AND+1992&client=firefox-b-d&ei=nureYYaHC5Hg7_UPjNyHIA&ved=0ahUKEwiGzvD7uqz1AhUR8LsIHQzuAQQQ4dUDCA0&uact=5&oq=BMW+3+Series+Chassis+code+AND+1992&gs_lcp=Cgdnd3Mtd2l6EAM6BwgAEEcQsAM6BAghEApKBAhBGABKBAhGGABQmkdYjllg5lpoA3ACeACAAV-IAekGkgECMTCYAQCgAQHIAQjAAQE&sclient=gws-wiz) delivers the information.

![E36 is the Chassis Code for 3 Series produced in 1992.](/blog/images/e36-is-the-chassis-code-for-3-series-produced-in-1992.png)

[E36 is the Chassis Code for 3 Series produced in 1992](https://www.turnermotorsport.com/t-BMW-Chassis-Codes)


### Exclude *\-*


The **-** (dash) excludes whatever comes immediately after it. It can be used to exclude a word like so:

```text
microsoft 10 backup built in -"cloud"
```

`-``"`cloud`"` was added to exclude cloud backup solutions, such as OneDrive which is a Microsoft owned service and so can be a valid return to the `built in` keyword in the query.

I would advise against not putting the excluded word or phrase inside quotation marks, as it will let the algorithm exclude other related terms and not the one you wrote for example. It might do other things as well...
With exclusions, actually telling the algorithm what to exclude (and nothing else) from the search results seems to give reliable and foreseeable results.

![Built in local backup solution Windows 10](/blog/images/built-in-local-backup-solution-windows-10.png)

Excluding phrases or anything that has white space in it, makes using  around what is to be excluded non optional.


### Fill *\**


The \* acts as a wildcard, that will match any word or phrase.


#### Example \*


Let's say, that one remembers hearing something about U.S. Census, but never really understood what it is. One could send a query like this:

```text
Census *
```

Which would show this as the top hit. Out of over **4 Billion** results, that top hit gives the right information.

![U.S. Census Bureau - Search Results](/blog/images/u-s-census-bureau-search-results.png)


### Price Operator *\$*

This operator will look for prices in the results it will show. The user has to supply exact numerical values for the price they are looking for. '.' and ',' are allowed as decimal separators in the price statement. E.g.

```text
$9 # Will match anything that costs $9.
$99.99 # Will match any price of 99 Dollars and 99 Cents.
€1,99 # Will match anything that costs 1 Euro and 99 Cent.
```

The sign before the actual price value, will be interpreted as the currency the price is in.
The use of quotation marks around the price term, can help keep results relevant. Quotation marks do not escape the operators special meaning in the search, as I tested. The following all gave the exact same results. I tried it with a few other *price terms* to add some more qualitative evidence to my observation. There were no results found, that suggest that this search operator can be escaped by use of quotation marks either.

```text
"$" "1.99"
\"$\" "1.99"
\"$\" \"1.99\"
"$1.99"
\"$1.99\"
"\$1.99"
"$ 1.99"
"\$ 1.99"
```

#### Example Price Operator *\$*


Practical uses include, but are not limited to:

```text
"$9.99" "haircut" -coupon # This was necessary in this case.
$5 lunch manhattan
```

With the haircuts, there were a lot of unrelated results, that already were missing 'haircut' after a few results down the list. Many coupon matches for haircuts meant I had to exclude coupons like this `-`coupon.
There were also matches with 9.99 Pounds, which had to be excluded by means of using the **exact match** operator around the price term by adding quotation marks around the price term `"`$9.99`"`.


![Cheap haircuts](/blog/images/cheap-haircuts.png)

A guide on how to eat for less than \$5 in Manhattan is the Number one Result.

![Cheap Eats in Manhattan](/blog/images/cheap-eats-in-manhatten.png)

### *define*

Syntax is `define:<search term>` or, if \<search term> has whitespace in it, the syntax is `define:"<search term>"`.

**define** will priorities results that contain factual information about whatever was specified in \<search term> over other information about it.

This can be useful, if one wants to learn more about a product and not get mostly results with buying options for that item.

The **define** operator was used like that in the following example. A NAS from brand QNAP was passed along as \<search term> and the first query made use of the **define** operator, while the second one did not.


#### Example *define*


```text
define:TVS-872XT
```

Which resulted in the very accurate result that takes one directly to the technical specifications section on QNAP's website.

![define operator used with TVS872XT](/blog/images/define-operator-used-with-tvs872xt.png)


Without the **define** operator, the results focus on the prices of various sellers.

```text
TVS-872XT
```
![without define operator TVS872XT](/blog/images/without-define-operator-tvs872xt.png)


One can see the stark difference between the top results for each of the two methods.

### *Cache*

**Cache** will return the most recent cached version of a web page, if it is indexed by google.

This can be useful, if a web page is down for some reason or if there has been recent changes to the content of that web page, that one wants to be able to ignore when viewing the page. Things like the deletion of media or articles, that one wants to visit again, after they have been deleted from the web page.


#### Example *Cache*

```text
cache:https://www.backblaze.com/blog/how-long-do-disk-drives-last/
```

Nothing much has changed on the web page in the example, so the cached and the current version of this article will be the same.


### *filetype*

This operator is very powerful, if one is looking for content, that can be downloaded and searched prior to downloading it by means of the search query written.
Below is a, as of today, [complete list of supported file types, directly from google.](https://support.google.com/webmasters/answer/35287?hl=en)



|                       File types indexable by Google - Search Console Help                        |
|:-------------------------------------------------------------------------------------------------:|
|                               Adobe Portable Document Format (.pdf)                               |
|                                      Adobe PostScript (.ps)                                       |
|                                 Autodesk Design Web Format (.dwf)                                 |
|                                     Google Earth (.kml, .kmz)                                     |
|                                    GPS eXchange Format (.gpx)                                     |
|                                       Hancom Hanword (.hwp)                                       |
|                             HTML (.htm, .html, other file extensions)                             |
|                                   Microsoft Excel (.xls, .xlsx)                                   |
|                                Microsoft PowerPoint (.ppt, .pptx)                                 |
|                                   Microsoft Word (.doc, .docx)                                    |
|                                  OpenOffice presentation (.odp)                                   |
|                                   OpenOffice spreadsheet (.ods)                                   |
|                                      OpenOffice text (.odt)                                       |
|                                      Rich Text Format (.rtf)                                      |
|                                  Scalable Vector Graphics (.svg)                                  |
|                                         TeX/LaTeX (.tex)                                          |
| Text (.txt, .text, other file extensions), including source code in common programming languages: |
|                                     Basic source code (.bas)                                      |
|                         C/C++ source code (.c, .cc, .cpp, .cxx, .h, .hpp)                         |
|                                       C# source code (.cs)                                        |
|                                     Java source code (.java)                                      |
|                                      Perl source code (.pl)                                       |
|                                     Python source code (.py)                                      |
|                               Wireless Markup Language (.wml, .wap)                               |
|                                            XML (.xml)                                             |


The syntax of **filetype** with pdf as example, is:

`filetype:pdf`.

Whenever one is looking for an actual file and not content on a web page, that can not be downloaded this operator comes in handy.

#### Example *filetype*

To give ideas of how this operator can be used, a few examples follow:

- One is looking for the manual of a device one owns:


```text
"iphone 13" "manual" filetype:pdf
"algorithms" "cs" "princeton" filetype:pdf
"hard drive" AND "failure" AND ( filetype:csv OR filetype:zip OR filetype:json )
```


These are some examples of how the **filetype** operator can be used.

### *site*

The syntax is `site:'someurl' <search term> ...`

One can basically to an in-site search for 'someurl' using the powerful google web search algorithm and all the operators available.


### *related*

The **related** operator has the syntax:

`related:<keyword> ...` or `related:"<search term>" ...`

The latter in the case of a \<search term> with spaces in between.

It is a proprietary google operator in the sense, that it is unknown what is related in the eyes of the algorithm.
Use it, if the results are good is what I would suggest.


### *intitle*

**intitle** will look for matches in titles of articles, blog posts and basically anything that has a title for that matter.

#### Example *intitle*

```text
intitle:Häkkinen
intitle:Häkkinen schumacher
```

The first one returns the [*Mikka Häkkinen* Wikipedia article](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwi86oPuiq31AhVtkIsKHY3UAIoQFnoECAgQAQ&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FMika_H%25C3%25A4kkinen&usg=AOvVaw3NAWR8N-4LVieJGGz9YQUT) as the first result.


![haekkinen wikipedia article first result](/blog/images/haekkinen-wikipedia-article-first-result.png)


The second line gives this as the top result, which shows nicely what the operator does:

![haekkinen schumacher in title](/blog/images/haekkinen-schumacher-in-title.png)


### *allintitle*

This operator is simply the **intitle** operator where quotation marks are used on every instance, where it is called. Syntax is:

`allintitle:<search term 1> <search term 2> ...`

One does not need to add quotation marks around any of the search terms following the **allintitle** operator. The algorithm will assume, that they all have to be part of the title.

#### Example *allintitle*

Running the following query only resulted in one result. This goes to show, that the operator only accepts exact matches.


```text
allintitle:formula 1 cornering
```


![allintitle formula 1 cornering](/blog/images/allintitle-formula-1-cornering.png)


### *inurl*

The **inurl** operator has the syntax:

`inurl:<some URL or fragment of a URL> ...`

This operator will search for matching substrings in indexed URL strings.

It could come in handy, if one is looking for a sub part of a URL, that describes something like a forum or support site.

#### Example *inurl*



### *allinurl*
### *intext*
### *allintext*
### *AROUND\(X)*
### *weather*
### *stocks*
### *map*
### *movie*
### *in*
### *source*
