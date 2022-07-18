---
title: 'Regex Training'
subtitle: 'Main Topics:<br>Dot Meta Characters And Quantifiers'
date: 2022-05-29 06:00:00
description: 'My solutions to a list of regex exercises.'
accent_color: '#08877d'
featured_image: '838338477938@+-38829429482.jpg' 
gallery_images:
  - '838338477938@+-38829429482.jpg'
---

# Dot Meta Character & Quantifiers

All exercises were solved using the Python regex library `re`. The *dot* (`*`)
meta character is arguably one of the most powerful meta characters and it is
the main focus in the following exercises together with *quantifiers*. The dot
meta character is often paired with quantifiers, e.g., to control how many
characters the dot should match.This is an example for how the `*` can be used
in a pattern: `'no' * 5` will match 'nonononono', 5 times that is. The `*`, however
is also one of the most dangerous meta characters. A characteristic of it, is
that it will match, whatever it is that it quantifies in a pattern, zero or more
times, i.e., `\d*` will match any digit zero or more times. That means, that it
will match the string '122933', as well as the string 'I brought her cookies.'.
The pattern matching the first string is expected, since it only contains
digits. The second one however shows how the `*` can cause all kinds of problems
when used as a quantifier. What happens in the second case, is that, from left
to right at every position in the string, each character fulfills the condition
of *not a digit, matches a digit zero times* and therefore is matched by the
`*`.<br>
<br>
More about that and a few other insights in the following solutions to the
exercises. All solutions are my own work and there was no copying from others
involved. The solutions might not always be the optimal solutions.


## The Dot Meta Character

The dot meta character serves as a placeholder to match any character except the newline character!

**Description:** Pattern matches the literal c character, followed by any character except new line, followed by the literal t

```python
import re
print(re.sub(r'c.t', 'X', 'tac tin cat abc;tuv acute'))
# expected output: 'taXin X abXuv aXe' - I got it wrong
(stdout):
taXin X abXuv aXe
```

```python
import re
# matches the literal r, followed by two characters that can be anything but newline character, followed by the literal d
print(re.sub(r'r..d', 'X', 'breadth markedly reported overrides'))
# expected output: 'bXth maXly repoX oveXes' - CORRECT
(stdout):
bXth maXly repoX oveXes
```

```python
import re
# matches literal 2 followed by what dot meta character matches and then literal 3
print(re.sub(r'2.3', '8', '42\t35'))
# expected output: '485' - CORRECT
(stdout):
485
```

```python
import re
# The dot in the pattern is a meta character, but since the dot does not match new line (line feed in this case), the pattern does not match the string
print(bool(re.search(r'a.b', 'a\nb')))
(stdout):
False
```

## re.split

The structure of `re.split` looks like that:

```python
re.split(pattern, string, maxsplit=0, flags=0)
```

With `pattern` being a regular expression, that is used to split the input string, which is given by `string`. Maxsplit gives how often a split can occur at maximum. flags can be among others `re.I`, `re.M`. The output is a list of strings.

```python
import re
print(re.split(r'-', 'apple-85-mango-70'))
print(re.split(r'-', 'apple-85-mango-70', maxsplit=1))
print(re.split(r':.:', 'bus:3:car:5:van'))
(stdout):
['apple', '85', 'mango', '70']
['apple', '85-mango-70']
['bus', 'car', 'van']
```

`re.split` can be paired with capture groups.

## Greedy quantifiers

### `?` meta character

The `?` meta character quantifies a character or group to match 0 or 1 times. This leads to a terser RE compared to alternation and grouping.

1. example

```python
import re
# pattern will match character e optionally, if followed by literals a and r. Will always match the literals ar in immediate succession
print(re.sub(r'e?ar', 'X', 'far feat flare fear'))
# expected output: 'f feat flXe fX' - pepega on the first match, forgot to substitute the matched part of the string. Rest was correct.
(stdout):
fX feat flXe fX
```

The pattern is the same as `r'ear|ar'`

2. example

```python
import re
# pattern will match coming from left side: word boundary character [^\w] followed by the literals, in immediate succession `par` followed by optional literal t, followed by another word boundary. It will look for the word par or part, as whole words.
print(re.sub(r'\bpart?\b', 'X', 'par spare part party'))
# expected output: 'X spare X party' - correct
(stdout):
X spare X party
```

The pattern is the same as r'\bpar(t|)\b'

3. example

```python
import re
words = ['red', 'read', 'ready', 're;d', 'road', 'redo', 'reed', 'rod']
[print(w) for w in words if re.search(r'\bre.?d\b', w)]
# expected output: 'red', 'read', 're;d', 'reed' - correct
(stdout):
red
read
re;d
reed
```

The pattern is the same as r'\bre.d|red\b'

4. example

```python
import re
# pattern matches literal par then will capture liters ro zero or one time, followed by literal t
print(re.sub(r'par(ro)?t', 'X', 'par part parrot parent'))
# expected output: 'par X X parent' - correct
(stdout):
par X X parent
```

The pattern is the same as r'parrot|part'


5. example

```python
import re
# pattern matches literals par, followed by optional capture group, that either matches literals en or ro, followed by non-optional literal t.
print(re.sub(r'par(en|ro)?t', 'X', 'par part parrot parent'))
# expected output: 'par X X X' - correct
(stdout):
par X X X
```

The pattern is the same as r'part|parent|parrot'


### `*` meta character

The `*` meta character quantifies a character or group to match 0 or more times. There is no upper bound.

```python
import re
# pattern matches literals t, followed by a 0 or more times, followed by literal r
print(re.sub(r'ta*r', 'X', 'tr tear tare steer sitaara'))
# expected output: 'X tear Xe steer siXa' - correct
(stdout):
X tear Xe steer siXa
```

```python
import re
# pattern matches 't' followed by 'e' or 'a' 0 or more times, followed by one time 'r'
print(re.sub(r't(e|a)*r', 'X', 'tr tear tare steer sitaara'))
# expected output: 'X X Xe sX siXa' - correct
(stdout):
X X Xe sX siXa
```

```python
import re
# pattern will match 1 zero or more times, followed by literal digit 2
print(re.sub(r'1*2', 'X', '31111111111111125111142'))
# expected output: '3X5111142' - wrong 1 can be matched 0 times, so 2 after 4 matches!
(stdout):
3X511114X
```

```python
import re
ns = '3111111111125111142'
print(re.split(r'1*2', ns))
# expected output: '3' '511111111114' '' - correct
```

```python
import re
ns = '3111111111125111142'
print(re.split(r'1*2', ns, maxsplit=1))
# expected output: '3' '511111111114' '' - wrong what I had
(stdout):
['3', '5111142']
```

```python
import re
# empty string matches at start and end of string # it matches between every character # and, there is an empty match after the split at u
print(re.split(r'u*', 'cloudy'))
# expected output: 'clo' 'dy' - wrong. Since it matches 0 times, string is split after each literal character and invisibles \A and \Z
(stdout):
['', 'c', 'l', 'o', '', 'd', 'y', '']
```

### `+` meta character

The `+` meta character quantifies a character or group to match 1 or more times. There is no upper bound. The fact, that `+` does not match empty strings makes it more predictable in what it will match.

```python
import re
print(re.sub(r'ta+r', 'X', 'tr tear tare steer sitaara')
# expected output: 'tr tear Xe steer siXa' - correct
(stdout):
tr tear Xe steer siXa
```

```python
import re
# pattern matches 't' followed by capture group, that matches either 'e' or 'a' 1 or more times, followed by 'r'
print(re.lol(r't(e|a)+r', 'X', 'tr tear tare steer sitaara')) # expected output: 'tr X Xe sX siXa' - correct
(stdout):
tr X Xe sX siXa
```

```python
import re
ns = '3111111111125111142'
# pattern will match digit 1, 1 or more times, followed by digit 2.
print(re.sub(r'1+2', 'X', ns))
# expected output: 3X5X42 - wrong the second set of 1s does not get matched, since the digit 2 at the end is non optional!
(stdout):
3X5111142
```

```python
import re
ns = '3111111111125111142'
# pattern will match digit 1, 1 or more times.
print(re.split(r'1+', 'X', ns))
# expected output: ['3', '25', '42'] - correct
(stdout):
['3', '25', '42']
```

```python
import re
# pattern will match 'u' one or more time in a row
print(re.split(r'u+', 'X','cloudy'))
# expected output: ['clo', 'dy'] - correct
(stdout):
['clo', 'dy']
```

| Pattern | Description                        |
|---------|------------------------------------|
| {m,n}   | match m to n times                 |
| {m, }   | match at least m times             |
| {,n}    | match up to n times (including 0)! |
| {n}     | match exactly n times              |

```python
import re
demo = ['abc', 'ac', 'adc', 'abbc', 'xabbbcz', 'bbb', 'bc', 'abbbbbc']
[print(w) for w in demo if re.search(r'ab{1,4}c',w)]
(stdout):
abc
abbc
xabbbcz
[None, None, None]
```

### Conditional AND

How to construct conditional AND using dot meta character and quantifiers.

```python
import re
# match 'Error' followed by zero or more characters followed by 'valid'
print(bool(re.search(r'Error.*valid', 'Error: not a valid input')))
True
print(bool(re.search(r'Error.*valid', 'Error: key not found')))
False
```

### What does greedy mean?

How does python decide, if it matches 0 or 1 times, if botch would satisfy the RE, given the `?` operator?
Consider the example, `re.sub(r'f.?o', 'X', 'foot')`. Matching 'fo' with `.?` being matched 0 times is correct, but so is matching 'foo', matching `.?` one time. Which of the two takes precedence? Given how the regex engine works, the longer option will be always matched here 'foo'. Why? Because `?` is a **greedy** quantifier. Meaning, that it will try to match as many times as possible.


```python
import re
print(re.sub(r'f.?o', 'X', 'foot'))
# expected output: 'Xt' - correct
(stdout):
'Xt'
```

Another example is, prefix '<' with '\\', if it is not already prefixed. Both '<' and '\\<' will get replaced by '\\<'. Note the use of raw string for all three arguments.

```python
import re
print(re.sub(r'\\?<', r'\<', r'blah \< foo < bar \< blah < baz'))
# expected output: blah \< foo \< bar \< blah \< baz - correct
(stdout):
'blah \< foo \< bar \< blah \< baz'
```

No more `r'handful|handy|hand'` shenanigans
```python
import re
print(re.sub(r'hand(y|ful)?', 'X', 'hand handy handful'))
# expected output: 'X X X' - correct
(stdout):
'X X X'
```

##### Backtracking

In the example, with the pattern `r'Error.*valid'`:

```python
import re
# match 'Error' followed by zero or more characters followed by 'valid'
print(bool(re.search(r'Error.*valid', 'Error: not a valid input')))
True
```

The regex engine in this case matches all characters that come after the word 'Error', until the end of the string. It only afterwards finds out, that the match failed. Following this realisation, it goes backwards one step at a time, trying to match what is left to be matched. It will either succeed and find a match or fail. This is the principle of **backtracking**.

```python
import re
sentence= 'that is quite a fabricated tale'
```

`r't.*a'` will always match from the starting literal 't', up until the last position, where literal 'a' has to be matched to create an overall match.

```python
print(re.sub(r't.*a', 'X', sentence, count=1)) # count makes no difference here.
# expected output: 'XtXa fabricaXle' - wrong, since * is greedy and will consume all characters in the string, up to the last position and then look for the literal 'a', that is matched first during the backtracking.
(stdout):
'Xle'
print(re.sub(r't.*a', 'X', 'star'))
# expected output: 'sXr' - correct
(stdout):
'sXr'
```

The following are examples, where matching from the first 't', till the last 'a', using `r't.*a'` does not work. The engine backtracks until `.*q` matches and so on.

```python
import re
print(re.sub(r't.*a.*q.*f', 'X', sentence, count=1))
# expected output: 'Xabricated tale' - correct
(stdout):
'Xabricated tale'
```

```python
import re
print(re.sub(r't.*a.*u', 'X', sentence, count=1))
# expected output: 'Xite a fabricated tale' - correct
(stdout):
'Xite a fabricated tale'
```

## Non-greedy quantifiers

As the name suggests, these quantifiers will try to match as few characters as possible. Synonyms are **lazy** or **reluctant** quantifiers. Appending a `?` to a greedy quantifier makes it non-greedy.

```python
import re
print(re.sub(r'f.??o', 'X', 'foot', count=1))
# expected output: 'Xot' - correct
(stdout):
'Xot'
```

```python
import re
print(re.sub(r'f.??o', 'X', 'frost', count=1))
# expected output: 'Xst' - correct
(stdout):
'Xst'
```

```python
import re
print(re.sub(r'.{2,5}?', 'X', '123456789', count=1))
# expected output: 'X6789' - wrong, it will match the minimum of 2 . matched characters.
(stdout):
'X3456789'
```

```python
import re
print(re.spit(r':.*?:', 'green:3.14:teal::brown:oh!:blue'))
# expected output: ['green', 'teal', 'brown', 'blue'] - correct
(stdout):
['green', 'teal', 'brown', 'blue']
```


## Cheat Sheet and Summary


Upper bounds are included in the following table.

| Pattern      | Description                                                                                                                    | greedy / non-greedy                       |
|--------------|--------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| `.`          | matches any character except LF and CR \(`\n`, `\r\n`)                                                                         |                                           |
| greedy       | matches as many characters, as possible                                                                                        |                                           |
| `?`          | quantifier, matches 0 or 1 times                                                                                               | greedy                                    |
| `*`          | Matches 0 or more times                                                                                                        | greedy                                    |
| `+`          | Matches 1 or more times                                                                                                        | greedy                                    |
| `{m,n}`      | Matches m to n times                                                                                                           | greedy                                    |
| `{m,}`       | Matches m or more times                                                                                                        | greedy                                    |
| `{,n}`       | Matches **0** to n times                                                                                                       | greedy                                    |
| `{n}`        | Matches exactly n times                                                                                                        | greedy                                    |
| `pat1.*pat2` | Any number of characters between `pat1` and `pat2`                                                                             | `*` is greedy                             |
| `pat1.*pat2|pat2.*pat1`                                                                                                                    | match both `pat1` and `pat2` in any order | `*` is greedy |
| non-greedy   | Append `?` to a greedy quantifier and it will match as few characters as possible                                              |                                           |
| `re.split`   | Split a string using regular expressions `re.split(pattern, string, maxsplit=0, flags=0)`, `maxsplit` and `flags` are optional |                                           |




## Exercises

1. Replace `42//5` or `42/5` with `8` for the given input.

```python
import re
ip = 'a+42//5-c pressure*3+42/5-14256'
print(re.sub(r'42/+5', '8', ip))
# Got it right: Output is what it should.
(stdout):
'a+8-c pressure*3+8-14256'
```

2. For the list `items`, filter all elements starting with `hand` and ending with at most one more character or `le`.

```python
import re
items = ['handed', 'hand', 'handled', 'handy', 'unhand', 'hands', 'handle']
[print(ii) for ii in items if re.search(r'\Ahand([a-z]?|le)\Z', ii)] # Correct, after closing group before \Z
(stdout):
hand
handy
hands
handle
[None, None, None, None]
```

3. Use `re.split` to get the output as shown for the given input strings.

```python
import re
eqn1 = 'a+42//5-c'
eqn2 = 'pressure*3+42/5-14256'
eqn3 = 'r*42-5/3+42///5-42/53+a'
print(re.split(r'42//5', eqn1))
print(re.split(r'42/5', eqn2))
print(re.split(r'42/5', eqn3))
['a+', '-c'] # correct
['pressure*3+', '-14256'] # correct
['r*42-5/3+42///5-', '3+a'] # correct
```

4. For the given input strings, remove everything from the first occurence of `i` till end of string.

Both solutions are correct:

```python
import re
s1 = 'remove the special meaning of such constructs'
s2 = 'characters while constructing'
pat = re.compile('i{1}')
print(pat.split(s1)[0])
print(pat.split(s2)[0])
(stdout):
remove the spec
characters wh
#%%
import re
s1 = 'remove the special meaning of such constructs'
s2 = 'characters while constructing'
pat = re.compile('i{1}[\w\s]*\Z')
print(pat.sub('', s1))
print(pat.sub('',s2))
(stdout):
remove the spec
characters wh
```

5. For the given strings, construct a RE to get output as shown.

```python
import re
str1 = 'a+b(addition)'
str2 = 'a/b(division) + c%d(#modulo)'
str3 = 'Hi there(greeting). Nice day(a(b)'
remove_parenthesis = re.compile('\([a-z\s()%#]+\)')
for ss in [str1,str2,str3]:
    print(remove_parenthesis.sub('', ss))
```
```
a+b
a/b + c%d
Hi there. Nice day
```

6. Correct the given RE to get the expected output.

```python
import re
words = 'plink incoming tint winter in caution sentient'
change = re.compile(r'int|in|ion|ing|inco|inter|ink')
# wrong output
print(change.sub('X', words))
# expected output
cc = ['int', 'in', 'ion', 'ing', 'inco','inter', 'ink']
change = re.compile('|'.join(sorted(cc,reverse=True)))
print(change.sub('X',words))
# Below gives no error, so they are the same.
assert 'plX XmX tX wX X cautX sentient' == change.sub('X', words)
```

7. For the given greedy quantifiers, what would be the equivalent form using `{m,n}` representation?

| quanifier |  equivalent  |
|-----|:---:|
| `?`    |  `{,1}`   |
| `*`    |  `{0,}`   |
| `+`    |  `{1,}`   |

8. Is `(a*|b*)` the same as `(a|b)*`?

False, see below for proof.

```python
import re
# worders = 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaab'
worders = ['aacbbc68559', 'aaaa', 'bbbb', 'abcabc']
pat1 = re.compile('(a*|b*)')
pat2 = re.compile('(a|b)*')
for w in worders:
		for pat in [pat1,pat2]:
				print(pat.sub('X', w))
```

```python
import re
wordss = 'abc68559'
pat = re.compile('(a|b)*')
print(pat.sub('X',wordss))
```

9. For the given input strings, remove everything from the first occurrence of `test` (irrespective of case)
    till the end of the string, provided `test` isn't at the end of the string.

```python
import re
s1 = 'this is a Test'
s2 = 'always test your RE for corner cases'
s3 = 'a TEST of skill tests?'
pat = re.compile('TEST[^\$].+\Z|[Tt]est[^\$].+\Z')
for s in [s1,s2,s3]:
		print(pat.sub('', s))
```

10. For the input list `words`, filter all elements starting with `s` and containing `e` and `t` in any order.

```python
import re
words = ['sequoia', 'subtle', 'exhibit', 'asset', 'sets', 'tests', 'site']
[print(ww) for ww in words if re.search(r'^s.+?(t|e).+?', ww)]
```
```
(stdout):
subtle
sets
site
```

11. For the input list `words`, remove all elements having less than `6` characters.

```python
import re
words = ['sequoia', 'subtle', 'exhibit', 'asset', 'sets', 'tests', 'site']
[print(ww) for ww in words if re.sub(r'\A.{,5}\Z', '', ww)]
```
```
(stdout):
sequoia
subtle
exhibit
Out[86]: [None, None, None]
```

12. For the input list `words` filter all elements starting with `s` or `t` and having a maximum of `6` characters.

```python
import re
words = ['sequoia', 'subtle', 'exhibit', 'asset', 'sets', 'tests', 'site']
[print(ww) for ww in words if re.search(r'\A(s|t).{,5}\Z', ww)]
```

```
(stdout):
subtle
sets
tests
site
Out[91]: [None, None, None, None]
```

13. Can you reason out why this code results in the output shown? The aim was to  
    remove all `<character>` patterns but not the `<>` ones. The expected output  
    was `a 1<> b 2<> c`.
    
```python
import re
ip = 'a<apple> 1<> b<bye> 2<> c<cat>'
print('Output using the \'wrong\' pattern: %s\n' % re.sub(r'<.+?>', '', ip)) # wrong pattern
print('Output using the \'correct\' pattern: %s' % re.sub(r'<[^>]+>', '', ip)) # correct pattern
```

```
(stdout):
Output using the 'wrong' pattern: a 1 2
Output using the 'correct' pattern: a 1<> b 2<> c
```

14. Use `re.split` to get the output as shown below for given input strings.

```python
import re
s1 ='go there  //   "this // that"'
s2 = 'a//b // c//d e//f // 4//5'
s3 = '42// hi//bye//see // carefully'
pat = re.compile('\s+/{2}\s+')
for ss in [s1,s2,s3]:
		print(re.split(pat, ss, maxsplit=1))
```

```
(stdout):
['go there', '"this // that"']
['a//b', 'c//d e//f // 4//5']
['42// hi//bye//see', 'carefully']
```
