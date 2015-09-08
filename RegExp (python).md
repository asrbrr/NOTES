
Regular Expressions cheat-sheet (Python)
========================================



SEARCH FUNCTIONS/METHODS
------------------------

`re.search(pattner, string[, flags]) ` : searches *anywhere* the string.

` re.match(pattern, string[, flags]) -> MatchObject` : searches at the *beginning* of the string.

 `re.findall(pattern, string[, flags]) -> list of strings` : returns all matches as a list of strings
 
`re.sub(pattern, repl, string[, count, flags])` : replace instances by repl

##### split()
`re.split(pattern, string[, maxsplit, flags]) -> list of strings`
>Returns list of strings

#### group()
`matchobject.group()`  
>Returns is the matching text. .group(0) is the entire match. .group(1) si the first parenthesized subgroup. .group(1, 2), multiple arguments give us a tuple.

##### compile()
`re.compile(pattern[, flags]) -> RegexObject  `
>Compile a regular expression pattern into a regular expression object, which can be used for matching using its `match()` and `search()` methods

---


MANIPULATION METHODS
--------------------

##### split()
`re.split()`
>Split string by the occurrences of pattern. If capturing parentheses are used in pattern, then the text of all groups in the pattern are also returned as part of the resulting list

##### re.sub()
`re.sub(pattern, repl, string,  count=0, flags=0)`
>Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string. `count` is the maximum number of pattern occurrences to be replaced

---


VARIOUS
-------
- The 'r' at the start of the pattern string designates a python "raw" string which passes through backslashes without change which is very handy for regular expressions  
- Ignore capital characters : **re.I**,  **re.IGNORECASE**  


---


PATTERNS  
--------
Except for control characters, `(+ ? . * ^ $ ( ) [ ] { } | \)`, all characters match themselves

|pattern   |descr   |
|:---|:---|
|`^`	|Matches beginning of line.|
|`$`	|Matches end of line.|
|.	|Matches any single character except newline. Using m option allows it to match newline as well.|
|[...]	|Matches any single character in brackets.|
|[^...]	|Matches any single character not in brackets|
|`re*`	|Matches 0 or more occurrences of preceding expression.|
| re+	|Matches 1 or more occurrence of preceding expression.|
|re?	|Matches 0 or 1 occurrence of preceding expression.|
|re{ n}	|Matches exactly n number of occurrences of preceding expression.|
|re{ n,}	|Matches n or more occurrences of preceding expression.|
|re{ n, m}	|Matches at least n and at most m occurrences of preceding expression.|
|ab	|Matches either a or b.|
|(re)	|Groups regular expressions and remembers matched text.|
a|b	Matches either a or b.

#####  . (a period)
> matches any single character except newline '\n'

#####  \s  (\S)
> \s matches whitespace [ \t\n\r\f\v]  
> \S is the opposeite (matches non-whitespace)

##### \d    (\D)
> `\d` matches digits. Equivalent to [0-9].  
> `\D` is the opposite (matches nondigits).

#####  \w (\W)
> \w matches alphanimeric characters [0-9a-zA-Z_]  
> \W is the opposite (non-alphanumeric)


---


References
----------
1. intro: https://developers.google.com/edu/python/regular-expressions 
2. cheatsheet: https://github.com/tartley/python-regex-cheatsheet/blob/master/cheatsheet.rst
3. comprehensive: http://www.tutorialspoint.com/python/python_reg_expressions.htm
4. interactive: http://pythex.org/
