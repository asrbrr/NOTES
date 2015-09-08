
REGULAR EXPRESSIONS cheat sheet (Pyhton)
========================================


Search
------------------------

These functions return a matchobject, or None if not sucessful

`re.search(pattner, string[, flags]) ` : searches *anywhere* the string.
`re.match(pattern, string[, flags])`  : searches at the *beginning* of the string.
`re.findall(pattern, string[, flags])` : returns all matches as a list of strings
`re.split(pattern, string[, maxsplit, flags])` : returns list of strings

To view the results:
`matchobject.group()`   : returns is the matching text. .group(0) is the entire match. .group(1) si the first parenthesized subgroup. Multiple arguments such as .group(1, 2) give us a tuple.


---

Manipulation
--------------------
`re.sub(pattern, repl, string[, count, flags])` : replace instances by repl
`re.split()` : split string by the occurrences of pattern. If capturing parentheses are used in pattern, then the text of all groups in the pattern are also returned as part of the resulting list
`re.sub(pattern, repl, string,  count=0, flags=0)` : return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string. `count` is the maximum number of pattern occurrences to be replaced

---


Various
-------
- `re.compile(pattern[, flags])` : Compiles a RegExp pattern into a RegexObject , which can be used for matching using its `match()` and `search()` methods
- Ignore capital characters : `**re.I**,  re.IGNORECASE  `
- The 'r' at the start of the pattern string designates a python "raw" string which passes through backslashes without change which is very handy for regular expressions  

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

`. (a period) ` : matches any single character except newline '\n'

`\s  (\S) ` : 
 -  \s matches whitespace [ \t\n\r\f\v]  
 -  \S is the opposeite (matches non-whitespace)

`\d    (\D)`
 - > `\d` matches digits. Equivalent to [0-9].  
 - > `\D` is the opposite (matches nondigits).

`\w (\W)`
 - \w matches alphanimeric characters [0-9a-zA-Z_]  
 - \W is the opposite (non-alphanumeric)


---


References
----------
1. intro: https://developers.google.com/edu/python/regular-expressions 
2. cheatsheet: https://github.com/tartley/python-regex-cheatsheet/blob/master/cheatsheet.rst
3. comprehensive: http://www.tutorialspoint.com/python/python_reg_expressions.htm
4. interactive: http://pythex.org/
