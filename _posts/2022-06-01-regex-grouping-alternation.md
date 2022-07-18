---
title: 'Regex Series<br>Grouping And Alternation'
date: 2022-06-01 16:00:00
description: 'This article shows my solutions to problems, that regular
expressions are commonly used for. The main topics are Grouping & Alternation.'
featured_image: '/images/negative-space-aerial-pacific-ocean.jpeg'
accent_color: '#08877d'
---

# Regex Series: Alternation & Grouping

Grouping and alternation are two basic concepts, that should be understood and
made use of in a variety of regular expression patterns. This article shows my
solutions to problems from these two areas using practical examples.

## 21.

### a.)

Check if the given string starts with `be`.

---



```python
import re


line1 = 'be nice'
line2 = '"best!"'
line3 = 'better?'
line4 = 'oh no\n bear spotted'

pat = re.compile('^be.*')

print(f'{line1}: {bool(pat.search(line1))}')

print(f'{line2}: {bool(pat.search(line2))}')

print(f'{line3}:{bool(pat.search(line3))}')

print(f'{line4}:{bool(pat.search(line4))}')
```

    be nice: True
    "best!": False
    better?:True
    oh no
     bear spotted:False


### b.) 

For the given input string, change only whole word `red` to `brown`.

---


```python
import re


words = 'bred red spread credible'
re.sub(r'\bred\b', 'brown', words)
```




    'bred brown spread credible'



### c.)

For given list with strings, filter out the ones that contain `42`.

---

Surrounded by word characters problem.



```python
import re


words = ['hi42bye', 'nice1423', 'bad42', 'cool_42a', 'fake4b']

f = [w for w in words if re.search(r'\w42\w', w)]

print(f)
```

    ['hi42bye', 'nice1423', 'cool_42a']


### d.) 

For given input list, filter all elements that start with `den` or end with `ly`.

---


```python
import re


items = ['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\n', 'dent']

f = [print(so) for so in items if re.search(r'\A^den|ly$\Z', so)]
print(f)
```

    lovely
    2 lonely
    dent
    [None, None, None]


### e.)

For the given input string, change the whole word `mall` to `1234`, only if it
is at the start of a line.

---


```python
import re


para = '''\
ball fall wall tall
mall call ball pall
wall mall ball fall
mallet wallet malls'''

print(re.sub(r'^(mall)\b','1234' ,para, flags=re.M))
```

    ball fall wall tall
    1234 call ball pall
    wall mall ball fall
    mallet wallet malls


### f.)

For the given list, filter all elements having a line starting with `den` or
ending with `ly`.

---


```python
import re


print('We are at f')
items = ['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\nfar', 'dent']

[print(bing) for bing in items if re.search(r'^den|ly$', bing, flags=re.M)]
```

    We are at f
    lovely
    1
    dentist
    2 lonely
    fly
    far
    dent





    [None, None, None, None, None]



### g.)

For the given input list, filter all whole elements '12\nthree' irrespective of case.

---


```python
import re


items = ['12\nthree\n', '12\nThree','12\nthree\n4','12\nthree']

[print(bang) for bang in items if re.search(r'\A12\nthree\Z', bang, flags=re.I)]
```

    12
    Three
    12
    three





    [None, None]



### h.)

For the given input list, replace `hand` with `X` for all elements that start
with `hand` followed by at least one word character.

---


```python
items = ['handed', 'hand', 'handy', 'unhanded', 'handle', 'hand-2']

[print(re.sub(r'\Ahand\B', 'X', bing)) for bing in items]
print('\ntest\n')
[print(re.sub(r'^hand\B', 'X', bing)) for bing in items]
```

    Xed
    hand
    Xy
    unhanded
    Xle
    hand-2
    
    test
    
    Xed
    hand
    Xy
    unhanded
    Xle
    hand-2





    [None, None, None, None, None, None]



### i.) 

For the given input list, filter all elements starting with `h` Additionally,
replace `e` with `X` for these filtered elements.

---


```python
import re


items = ['handed', 'hand', 'handy', 'unhanded', 'handle', 'hand-2']

[print(str(re.fullmatch(r'\Ah[a-z-\d]+', proc)).replace('e', 'X')) for proc in items]
```

    <rX.Match objXct; span=(0, 6), match='handXd'>
    <rX.Match objXct; span=(0, 4), match='hand'>
    <rX.Match objXct; span=(0, 5), match='handy'>
    NonX
    <rX.Match objXct; span=(0, 6), match='handlX'>
    <rX.Match objXct; span=(0, 6), match='hand-2'>





    [None, None, None, None, None, None]



**Notes**

Without any word boundaries, any matching part will be replaced.


```python
import re


words=['cat','par']

'|'.join(words)

re.sub('|'.join(words), 'X', 'cater cat concatenate par spare')
```




    'Xer X conXenate X sXe'



**expected:** Xer X conXenate X sXe
Correct!

**Note** how raw string is used on either side of concatenation. Avoid f-strings
unless you know how to compensate for RE *He means something like this: f'we got
f, we just need {delta} now.'*



```python
import re


alt = re.compile(r'\b(' + '|'.join(words) + r')\b')
print(alt)
```

    re.compile('\\b(cat|par)\\b')


expected: \b(cat|par)\b


```python
alt.sub(r'X', 'cater cat concatenate par spare')
```




    'cater X concatenate X spare'



expected: 

```
Xer X concatenate X spare  
```

actual: 

```
Out[16]: 'cater X concatenate X spare'
```

This is how the above pattern looks like as a normal string:


```python
import re


alt.pattern
```




    '\\b(cat|par)\\b'




```python
Out[17]: '\\b(cat|par)\\b'
```

assertion gives no error, so the two are the same:



```python
assert alt.pattern == r'\b(cat|par)\b'
```

**There is a quicker way to add word boundaries using `re.fullmatch` matching
only whole words.**


```python
import re


terms = ['no','ten', 'it']

items = ['dip', 'nobody', 'it', 'oh', 'no', 'bitten']

pat = re.compile('|'.join(terms))

# matching only whole words
f = [w for w in items if(pat.fullmatch(w))]
print(f)
```

    ['it', 'no']




#### Matching anywhere


```python
import re


f = [w for w in items if(pat.search(w))]

print(f)
```

    ['nobody', 'it', 'no', 'bitten']



#### Precedence Rules

> In Python, the alternative which matches earliest in the input string gets 
> precedence. re.Match output comes handy to illustrate this concept.

`span` shows the start and end+1 index of matched portion match shows the text,
that was matched by the pattern.


```python
import re


words = 'lion elephant are rope not'

print(re.search(r'on', words))


print(re.search(r'ant', words))




# starting index of 'on' < index of 'ant' for given string input
# so 'on' will be replaced irrespective of order
# count optional argument here restricts no. of replacements to 1

print(re.sub(r'on|ant', 'X', words, count=1))


print(re.sub(r'ant|on', 'X', words, count=1))
```

    <re.Match object; span=(2, 4), match='on'>
    <re.Match object; span=(10, 13), match='ant'>
    liX elephant are rope not
    liX elephant are rope not


<br>

> What happens if alternatives match on same index? The precedence is then left to right in the order of declaration.

<br>




```python
import re


mood = 'best years'

print(re.search(r'year', mood))


print(re.search(r'years', mood))


# the following shows, that since the starting indexes for 'year' and 'years'
# are the same, whatever comes first in the alternation matches the string

print(re.sub(r'year|years', 'X', mood, count=1))


print(re.sub(r'years|year', 'X',mood, count=1))
```

    <re.Match object; span=(5, 9), match='year'>
    <re.Match object; span=(5, 10), match='years'>
    best Xs
    best X



```python
import re



mood = 'best years'

print(re.search(r'year', mood))

print(re.search(r'years', mood))

print(re.sub(r'year|years', 'X', mood, count=1))

print(re.sub(r'years|year', 'X',mood, count=1))
```

    <re.Match object; span=(5, 9), match='year'>
    <re.Match object; span=(5, 10), match='years'>
    best Xs
    best X



```python
import re


words = 'ear xerox at mare part learn eye'

# this is going to be the same as: r'ar'
print(re.sub(r'ar|are|art', 'X', words))

# this is going to be the same as: r'are|ar'
print(re.sub(r'are|ar|art', 'X', words))

# this one words as needed
print(re.sub(r'are|art|ar', 'X', words))
```

    eX xerox at mXe pXt leXn eye
    eX xerox at mX pXt leXn eye
    eX xerox at mX pX leXn eye


#### Deal with the precedence rule


```python
import re


words = ['hand', 'handy', 'handful']

alt = re.compile('|'.join(sorted(words, key=len, reverse=True)))

print(alt.pattern)
```

    handful|handy|hand


```python
import re


print(alt.sub('X', 'hands handful handed handy'))
```

    Xs X Xed X




```python
import re


# without sorting, alternation order will come into play
print(re.sub('|'.join(words), 'X', 'hands handful handed handy'))
```

    Xs Xful Xed Xy



## Exercises for alternation part

### 1.

For the given input list, filter all elements that start with `den` or end with
`ly`

---


```python
import re


items=['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\n', 'dent']

f = [print(ff) for ff in items if bool(re.search(r'\Aden|ly\Z', ff))]
print(f)
```

    lovely
    2 lonely
    dent
    [None, None, None]


### 2.

For the given list, filter all elements having a line starting with `den` or
ending with `ly`.

---


```python
import re


items = ['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\nfar', 'dent']

f = [print(ff) for ff in items if re.search(r'\nden|^den|ly$|ly\n', ff)]
print(f)
```

    lovely
    1
    dentist
    2 lonely
    fly
    far
    dent
    [None, None, None, None, None]


### 3. 

---

For the given input strings, replace all occurrences of `removed` or `reed` or
`received` or `refused` with `X`.



```python
import re


s1 = 'creed refuse removed read'

s2 = 'refused reed redo received'

words = ['removed', 'reed', 'received', 'refused']

pat = re.compile('|'.join(sorted(words, key=len, reverse=True)))

print(pat)

print(pat.sub('X',s1))

print(pat.sub('X',s2))
```

    re.compile('received|removed|refused|reed')
    cX refuse X read
    X X redo X


### 4.

For the given input strings, replace all matches from the list `words` with `A`.

---


```python
import re


s1 = 'plate full of slate'

s2 = "slated for later don't be late" 

# note to self, double quotes to escape the don't single quote in the string.

words = ['late', 'later', 'slated']

pat = re.compile('|'.join(sorted(words, key=len, reverse=True)))

print(pat)

print(pat.sub('A',s1))

print(pat.sub('A',s2))
```

    re.compile('slated|later|late')
    pA full of sA
    A for A don't be A


### 5.

Filter all whole elements from the input list `items` based on elements listed
in `words`.


```python
import re


items = ['slate', 'later', 'plate', 'late', 'slates', 'slated ']

words = ['late', 'later', 'slated']

pat = re.compile(r'\A(' + '|'.join(sorted(words, key=len, reverse=True)) + r')\Z')

print(pat)

f = [print(dd) for dd in items if pat.search(dd)]
print(f)
```

    re.compile('\\A(slated|later|late)\\Z')
    later
    late
    [None, None]


