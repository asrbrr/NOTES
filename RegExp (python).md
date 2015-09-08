
#Regular Expressions (Python)

---


#SEARCH FUNCTIONS/METHODS

###search()
`re.search(pattner, string[, flags]) -> MatchObject`  
>Searches for that pattern **within** the string. If the search is successful, it returns a match object; otherwise ir returns `None`.  `match.group()` is the matching text

### match()
` re.match(pattern, string[, flags]) -> MatchObject`  
>Checks for a match only at the **beginning** of the string, while `re.search` checks for a match anywhere in the string

### findall()
 `re.findall(pattern, string[, flags]) -> list of strings`  
>Finds *all* the matches and returns them as a list of strings, with each string representing one match
 
### sub()
`re.sub(pattern, repl, string[, count, flags]) -> string`  
>Searches for all the instances of pattern in the given string, and replaces them.

### split()
`re.split(pattern, string[, maxsplit, flags]) -> list of strings`
>Returns list of strings

### .group()
`matchobject.group()`  
>Returns is the matching text. .group(0) is the entire match. .group(1) si the first parenthesized subgroup. .group(1, 2), multiple arguments give us a tuple.

### compile()
`re.compile(pattern[, flags]) -> RegexObject  `
>Compile a regular expression pattern into a regular expression object, which can be used for matching using its `match()` and `search()` methods


#MANIPULATION FUNCTION/METHODS
###split()
`re.split()`
>Split string by the occurrences of pattern. If capturing parentheses are used in pattern, then the text of all groups in the pattern are also returned as part of the resulting list

###re.sub()
`re.sub(pattern, repl, string,  count=0, flags=0)`
>Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string. `count` is the maximum number of pattern occurrences to be replaced

#VARIOUS
- The 'r' at the start of the pattern string designates a python "raw" string which passes through backslashes without change which is very handy for regular expressions
- **re.I**,   re.IGNORECASE
