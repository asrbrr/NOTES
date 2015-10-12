## Excel VBA snippets


####Loop through files in a directory
```vb
MyFile = Dir(path & "*.xls")    
Do While MyFile <> ""
       ...
        MyFile = Dir()   'this jumps into the next file in the dir
Loop
```
