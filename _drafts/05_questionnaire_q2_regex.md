```python
import re

# pattern matches the literal c character, followed by any character except new line, followed by the literal t.
print(re.sub(r"c.t", "X", "tac tin cat abc;tuv acute"))
# expected output: 'tac tin X abXuv aXe'
```

    taXin X abXuv aXe



```python
import re

# matches the literal r, followed by two characters that can be anything but newline character, followed by the literal d
print(re.sub(r"r..d", "X", "breadth markedly reported overrides"))
# expected output: 'bXth maXly repoX oveXes'
```

    bXth maXly repoX oveXes



```python
import re

# matches literal 2 followed by what dot metacharacter matches and then literal 3
print(re.sub(r"2.3", "8", "42\t35"))
```

    485



```python
import re

# The dot in the pattern is a metacharacter, but since the dot does not match new line (line feed in this case), the pattern does not match the string
print(bool(re.search(r"a.b", "a\nb")))
```

    False



```python
import re

print(re.split(r"-", "apple-85-mango-70"))
print(re.split(r"-", "apple-85-mango-70", maxsplit=1))
print(re.split(r":.:", "bus:3:car:5:van"))
```

    ['apple', '85', 'mango', '70']
    ['apple', '85-mango-70']
    ['bus', 'car', 'van']



```python
import re

print(re.sub(r"e?ar", "X", "far feat flare fear"))
# expected output: 'f feat flXe fX'
```

    fX feat flXe fX



```python
import re

# pattern will match coming from left side: word boundary character [^\w] followed by the literals, in immediate succession `par` followed by optional literal t, followed by another word boundary. It will look for the word par or part, as whole words.
print(re.sub(r"\bpart?\b", "X", "par spare part party"))
# expected output: 'X spare X party'
```

    X spare X party



```python
import re

words = ["red", "read", "ready", "re;d", "road", "redo", "reed", "rod"]
[print(w) for w in words if re.search(r"\bre.?d\b", w)]
# expected output: 'red', 'read', 're;d', 'reed'
```

    red
    read
    re;d
    reed





    [None, None, None, None]




```python
import re

# pattern matches literal par then will capture liters ro zero or one time, followed by literal t
print(re.sub(r"par(ro)?t", "X", "par part parrot parent"))
```

    par X X parent



```python
import re

# pattern matches literals par, followed by optional capture group, that either matches literals en or ro, followed by non-optional literal t.
print(re.sub(r"par(en|ro)?t", "X", "par part parrot parent"))
# expected output: 'par X X X' - correct
```

    par X X X



```python
import re

# pattern matches literals t, followed by a 0 or more times, followed by literal r
print(re.sub(r"ta*r", "X", "tr tear tare steer sitaara"))
# expected output: 'X tear Xe steer siXa'
```

    X tear Xe steer siXa



```python
import re

# pattern matches 't' followed by 'e' or 'a' 0 or more times, followed by one time 'r'
print(re.sub(r"t(e|a)*r", "X", "tr tear tare steer sitaara"))
# expected output: 'X X Xe sX siXa' - correct
```

    X X Xe sX siXa



```python
import re

#
print(re.sub(r"1*2", "X", "31111111111111125111142"))
# expected output: '3X5111142'
```

    3X511114X



```python
import re

ns = "3111111111125111142"
print(re.split(r"1*2", ns))
# expected output: '3' '511111111114' ''
```

    ['3', '511114', '']



```python
import re

ns = "3111111111125111142"
print(re.split(r"1*2", ns, maxsplit=1))
# expected output: '3' '511111111114' '' - correct
```

    ['3', '5111142']



```python
import re

print(re.split(r"u*", "cloudy"))
# expected output: 'clo' 'dy'
```

    ['', 'c', 'l', 'o', '', 'd', 'y', '']



```python
import re

print(re.sub(r"ta+r", "X", "tr tear tare steer sitaara"))
# expected output: 'tr tear Xe steer siXa'
```

    tr tear Xe steer siXa



```python
import re

# pattern matches 't' followed by capture group, that matches either 'e' or 'a' 1 or more times, followed by 'r'
print(re.sub(r"t(e|a)+r", "X", "tr tear tare steer sitaara"))
# expected output: 'tr X Xe sX siXa' - correct
```

    tr X Xe sX siXa



```python
import re

ns = "3111111111125111142"
# pattern will match digit 1, 1 or more times, followed by digit 2.
print(re.sub(r"1+2", "X", ns))
# expected output: 3X5X42
```

    3X5111142



```python
import re

ns = "3111111111125111142"
# pattern will match digit 1, 1 or more times, followed by digit 2.
print(re.split(r"1+", ns))
# expected output: 3X25X42
```

    ['3', '25', '42']



```python
import re

# pattern will match 'u' one or more time in a row
print(re.split(r"u+", "cloudy"))
# expected output: cloXdy - correct
```

    ['clo', 'dy']



```python
import re

demo = ["abc", "ac", "adc", "abbc", "xabbbcz", "bbb", "bc", "abbbbbc"]
[print(w) for w in demo if re.search(r"ab{1,4}c", w)]
```

    abc
    abbc
    xabbbcz





    [None, None, None]




```python
import re

# match 'Error' followed by zero or more characters followed by 'valid'
print(bool(re.search(r"Error.*valid", "Error: not a valid input")))
print(bool(re.search(r"Error.*valid", "Error: key not found")))
```

    True
    False



```python
import re

sentence = "that is quite a fabricated tale"
print(re.sub(r"t.*a", "X", sentence, count=1))
```

    Xle



```python
import re

sentence = "that is quite a fabricated tale"
print(re.sub(r"t.*a", "X", sentence, count=2))
```

    Xle



```python
import re

sentence = "that is quite a fabricated tale"
print(re.sub(r"t.*a", "X", sentence))
```

    Xle



```python
import re

ip = "a+42//5-c pressure*3+42/5-14256"
print(re.sub(r"42/+5", "8", ip))
```

    a+8-c pressure*3+8-14256



```python
import re

items = ["handed", "hand", "handled", "handy", "unhand", "hands", "handle"]
[print(ii) for ii in items if re.search(r"\Ahand([a-z]?|le)\Z", ii)]
```

    hand
    handy
    hands
    handle





    [None, None, None, None]




```python
import re

eqn1 = "a+42//5-c"
eqn2 = "pressure*3+42/5-14256"
eqn3 = "r*42-5/3+42///5-42/53+a"
print(re.split(r"42//5", eqn1))
print(re.split(r"42/5", eqn2))
print(re.split(r"42/5", eqn3))
```

    ['a+', '-c']
    ['pressure*3+', '-14256']
    ['r*42-5/3+42///5-', '3+a']



```python
import re

s1 = "remove the special meaning of such constructs"
s2 = "characters while constructing"
pat = re.compile("i{1}")
print(pat.split(s1)[0])
print(pat.split(s2)[0])
```

    remove the spec
    characters wh



```python
import re

s1 = "remove the special meaning of such constructs"
s2 = "characters while constructing"
pat = re.compile("i{1}[\w\s]*\Z")
print(pat.sub("", s1))
print(pat.sub("", s2))
```

    remove the spec
    characters wh

