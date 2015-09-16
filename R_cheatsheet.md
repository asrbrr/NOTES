# R (language)


#### General commands

```R
<-              #assignment (also =)
<<-             #assignment in another environment
#               #comments
?help           #also   help(func)  ;  ?`:`for operators
example(func)

arguments(fun)  #lsit the arguments of the function
identical()     #compare two objects
  
save(list=c(objA, objB), file="filename.Rda")
load("filename.Rda")
```

#### Basic functions
``` R
#Object information
class()
str(x)          #compactly display internal structure of a R object, including functions

#Shape
length()      #vectors have length, not dim
dim(m)        #number of rows&columns in matrix or df

#Names, attributes
names(x)       #assign names to R objects
attributes()                       #attributes of an object
attr(object, "att_name") <- "m/s"  #set an attribute

#Retetition, spliting and joining
rep(NA, 100)  # repeat 100 times
unique()    #remove duplicates
split         #useful in conjunction with lapply or sapply
paste()       #join elements from a vector; if two sequences given, is pariwise






```

#### Filesystem navigation
```r
getwd()
setwd(abspath)        #in Windows ""C:\\etc"
setwd("./data")       #
setwd("../")          #move one dir up

list.files(path)      #also dir()
file.exists("dirName")
file.create()
file.copy()
file.path()
dir.create("dirName")
dir.exists()

unlink()              #delete directory; note the recursive flag for nested directories
```

#### Workspace
```r
ls()           #list of variables in the workspace; rm(list=ls()) to clear
```

#### Packages

``` r
install.packages('ggplot2')  
update.packages(checkBuilt=TRUE, ask=FALSE)
libary(ggplo2)    #load package for use (no quotes!)
R.version.string
```

#### Is functions
``` R
is.na(x)          
is.nan(x)
x[!is.na(x)]       #removes NA values
complete.cases(x,y)  #which cases are complete 
```

#### Coercion
``` R
as.numeric(x)
as.logical(x)
as.character(x)
```

#### Tools
```r
gl(n,k)     #factor vector, n levels and k repetitions each
```

---

## Atomic data types
Everythin is an object in R.  

#### character
```
"string"
```

#### numeric
```
Inf
NaN    #Undefined value - not a number. NaN is NA (but not the reverse)
```

#### integer
```
5L
```

#### complex
```

```

#### logical
```
T, F
TRUE, FALSE
```

#### missing values
``` r
NA         #NA has a type as well (NA character, etc)
```

#### Date-times
```r
as.Date("1970-01-01")
Sys.time()    #uses the POSIXct class, ie, seconds since 1970-01-01
as.POSIXlt(x) #list with sec, min, hour, mday, mon, year, wkday, yday, isdst
strptime("January 10, 2014", "%B %d %Y")

weekdays()
months()
```

## Data Structures


#### Vectors

- Only accepts elements of the same type  
- Mixing types will coherce to the lowest denominator of types  
- Can have named elements

``` R
vector()                      #empty vector
vector("numeric", length=10)  #initializes to default value, 0

c(0,1,2,3,4)                  #'combine' 

1:4                           #also 15:1 or pi:10
seq(1,10,by=0.5)              #generalizes the : operator
seq(5, 10, length=30)
seq_along(my_seq)             #also seq(along.with = my_seq), or 1:length(my_seq)
rep(pi,10)

c(foo = 1, bar = 2)           #named elements
```



#### Matrices
 - All the data has to be same type (numeric, integer, logical, character).
 - Special type of vector, with a dimension attribute being a vector of length 2
 - a matrix is simply an atomic vector with a dimension attribute
 - Matrix multiplication with `a%*%b`
 
``` r
matrix(1:6, nrow = 2, ncol = 3)
matrix(1:10, ncol=2)  
#can also be created by adding a dimension attr to a vector
dim(1:6) <- c(2,3)  ; dim(v) = c(2,3)
#also by combining vectors
x <- 1:3; y=10:12 ; cbind(x,y) ; rbind(x,y)
```



#### data.frame
``` R
df <- data.frame(colA = c(1,2,3), colB = c('y','n','y'))    
df$colA
df[,1]               #first col
def[1,]              #first row

#Attributes
names(df)           #column names
colnames()
row.names           #row names

#New elements
`X$var4 <- rnorm(5)`    #new column var4
cbind(X,rnorm(5))       #like above
```


#### lists
 - stores other objects
 - can contain different types
 - indexed with double brackets [[]]
```r
list(1, "string", 3.2)
list(foo=1:4, bar=0.6)

unlist                     #flatten
```


#### factors
Factors are variables in R which take on a limited number of different values; such variables are often refered to as categorical variables.
There are two types: ordered and unordered.

``` r
x <- factor(c("y","n","y"))
x <- factor(c("y","n","y"), levels=c("y","n")) #ordered
```

#### data.table
```r
library(data.table)
tables()      #all the datatables in memory
dt[c(2,3]     #careful: when subsetting wtih single index, subsets rows! 
df[,list(mean(x), sum(z))]   #applies expressions to the table (x,y are colNames)
dt[,w:=z^2]   #creates new column (without copying, as dataframe)
dt[,a:=x>0]   #new column of T/F-s
```

## Subsetting and sorting

#### [ ]
 - Single square bracket always returns __objects of the same class__ as the original
 - To get multiple elements of a list, use [ ]
 - Drop argument in the [ ] operator reduces dimensions of the returned object by default: so subsetting a matrix and taking one element gives back a 1 dim vector.
 - Index vectors can be logical, integers (pos or neg) and character (if named elements exist)
 
``` r
x[1]
x["bar"]   
x[1:4]        #numeric index
x[c(1,3)]     #List with elements 1 and 3 of the list
x[c(-2, -10)] #all elements except 2 and 10th. Also x[-c(2, 10)]
```
Rows and columns
```r
x[,1]         #first col in a matrix/df
x[,"colname"]
x[1,]         #first row
x[1:2,"var2"]
```
Logical index

``` r
x[x>2]       
x[!is.na(x)]
`X[(X$var1 <3 | X$var2>10), ]`
`X[which(X$var2>8), ]`         #skips the NA by itself

```

 
#### [[ ]]
 - Double bracket operator used to extract a single element of a list and dataframe.  
 - For example, with `x <- list(foo=1:4, bar=0.6)`, x[[1]] gives an integer vector, while x[1] gives a list (which is the same class as the original object).  
 - Accepts computed arguments
 - Recursive access: `x[[1]][[3]]` equivalent to  x[[c(1,3)]], gives third element of the first element. Nota that this is **not** the same as x[c(1,3)]!

#### `$`
 - Dollar sign used with lists or dataframes to get the element by name
 - Needs to be a literal symbol.
 - Accepts partial matching: ` x$a or x[["a", exact=FALSE]] ` retrieves `x$asdf`
 in the console)
``` r
x$bar equivalent to x[["bar"]]
```

#### existance or pertainance
```r
a %in% v
any()
all()
```

#### sort

```r 
sort             
`X[order(X$var1)]`    #order the df according to var1
```

#### Set operations
```r
intersect(X,Y)
```

## Summarizing & transforming data 

Summarize
```r
head(df,n)
tail(df,n)
str(df)
summary(df)
table(df$col, useNA="ifany")
table(v1,v2)
table(x)                     #gives the count of number of items
quantile(df)
sum(is.na(col))
xtabs(Freq ~Gender + Admit, data=DF)  #pivot table: values=Freq, rows=Gender, cols=Adm 
ftable(xt)                    #hierarchical summary of xtabs
```

Create variables
```r
col %in% c('A','B')               #subset indication
ifelse(col<0,TRUE,FALSE)          #binary variables
cut(col, breaks=quantiles(col))   #factor variable breaking up the variable in groups
factor(col)
as.numeric(col)
mutate(df, newcol=...)            #adds new columns???
```

Reshape data
```r
library(reshape)
melt                              #function to reshape (one row for each measure vars)
dcast(df, cyl~variable, mean)
```

Merge data
```r
merge(x,y, by.x, by.y, all)       #by default all the columns overlapping; else, use by.x etc)
```

## plyr/dplyr packages

#### plyr

``` r
arrange(X,var1)                   #order
arrange(X,desc(var1))             #order desc
join                              #plyr package; only joins by common names              
join_all(list(df1,df2,df3))       #
```

#### dplyr
Format: 
 - first arg: df
 - subsequent args ; note that column names can be referred without the $.     

```r
select(df, col1:col3             #selects columns
select(df, -(col1:col3))         #excludes columns
filter(df, col2>10 & col1<100)   #selectes rows
arrange(df, date)                #sort
arrange(df, desc(date))          #sort descending
rename(df, newname=oldname)
mutate(df, detrend=var-mean(var))  #create new variable
summarize(group_by(df, var), colA=mean(colA))
%>%                              #pipeline operator

```

## Reading /Writing data  

```r
read.table()          #parameters: file, header, sep, row.names, nrows
read.csv()
read.csv2()
readLines              #lines of a text file
source                 #read R code files
dget                   #read R code files
unserialize            #read R objects in binary form

write.table(df, file="outputfile.csv", sep=',')
```


#### xls files:
xlsx package, but alto xlsx2, XLConnect
```r
library ( xlsx ) 
read.xlsx ("datafile.xlsx", sheetIndex=1,header=TRUE)
write.xlsx()
#xls files:
library ( gdata )
data <- read.xls ( "datafile.xls" )
```

#### XML
Componentes: Markup and Content.  
Examples:  
 - elements `<Greeting> Hello! </Greeting>`
 - empty tags `<line-break/>`
 - attributes `<step number=3> Connect A </step>`
```r
library(XML)
doc <- xmlTreeParse(fileUrl, useInternal=T)
rootNode <- xmlRoot(doc)
xmlName(rootNode)
rootNode[[1]] etc
```

#### Json

```r
library(jsonlite)
jsonData <- fromJSON("...")
names(jsonData) 
names(jsonData$field)
tojson(df, pretty=T)
```

##### mySQL
```r
install.packages("RMySQL")
conn <- dbConnect(MySQL(), user="...", host="...")
dbGetQuery(conn, "show databases"")   #shows all databases in the server
dbDisconnect(conn)

conn2 <- dbConnect(MySQL(), user="...", db="...", host="...")
dbListTables(conn2)
dbListFields(conn2, "tablename")
dbReadTable(conn2, "tablename")
dbGetQuery(conn2, "sql_sentence")
q <- dbSendQuery(conn2, "sql_sentence")
  fetch(q, n=10) #10 rows of table
  dbClearResult(query)  #clear query from server
```

#### HDF5
Contains groups (with zero or more sets and their metadata):
 - A group has a header, with group name and list of attributes
 - Also a symbol table, with list of objects in the group.
Contains datasets (data and metadata)
 - Header (name, dtype, dataspace, storage layout)
 - Array with the data
```r
source("http://bioconductor.org/biocLite.R")
biocLite("rhdf5")
library(rhdf5)
h5createFile("a.h5")
h5createGroup("a.h5", "foo")   #create group
h5ls("a.h5")                   #see the groups 
h5write(df, "a.h5", "foo")     #foo is a group; or can be "df" to put at upper level
h5read("a.h5", "foo/A", index=list(1:3,1))  #read elements 1:3 of columns 1 
```

#### Web
Webscraping
```r
conn = url("url")
htmlCode = readLines(conn)
close (conn)

library(XML)
html <- htmlTreeParse(url, useInternalNodes=T)
xpathSApply(html, "//title", xmlValue)
```

Alternative way to parese the data is httr, which allows authentication.
```r
library(httr)
html2 = GET(url)
content2 = content(html2, as="text")
parsedHtml = htmlParse(content2, asText=T)
xpathSApply(...)
```

Using handles to not need to authenticate time and again
```r
g = handle("http://...")
pg1 = GET(handle=g, path="/")

```

#### API
```r
library(httr)
myapp = oauth_app("twitter", key="..", secret="..")
sig = sign_oauth1.0(myapp, token="..", token_secret="..")
homeTL = GET("https://...json", sig)
j = content(homeTL)
j2 = jsonlite::fromJSON(toJSON(j)
```

#### Etc
Rough memory requirement calculation: 8bytes/numeric. But R need about 2 times this amount

Other textual formats that preserve the metadata:
 - `dput / dget`  : writes R code which can reconstruct the R object
 - `dump`    : as dput can be used on multiple objects
 
Interfaces to files/sites
 - `file() ; close()`  : opens a conection to a file
 - `url()`             : connection to a webpage

Get data from the internet:   
`download.file()`      #use flag method="curl" if https



##  Control structures

#### IF statemen
```R
if(i==1){
    ...
}
else{
    ...
}
#shortcut : ifelse(i==1, ..., ...)
#also : y <- if(...){1}else{0}
```

#### FOR loops
``` r
for(i in 1:5){...}
for(i in seq_along(x)) {x[i]}
```

#### WHILE loops
```r
while(z>3 && z<10){...}
```

#### REPEAT loops
```r
repeat {...}
```

#### Control structures
 - To exit loops:  `return`?? (stops the function) 
 - To continue to next iteration: `next`


#### logical operators
```R
! x
x & y
x && y        #only evaluates the first member of a vector, & does elementwise
x | y
x || y        #only evaluates the first member of a vector, | does elementwise
xor(x, y)
isTRUE()
which()       #returns indices of the TRUE *indices* of a vector
any()
all()
```

## Loop functions ('apply' functions)

Like lookuping through elements, but more compact. These functions make use of anonomous functions. Split-apply-combine strategy

#### lapply / sapply / vapply
 - lapply: loops over list and applyes func to each of them, returning list
 - sapply: (variant of lapply) tries to put elements as vector or matrix when possible  
 -  similar to sapply, but you can specify the output format requested; else it will error out
 
```r
lapply(list, fun, ...)  #applies fun to each element in list; returns *list^
                        #the ... arguments go to fun
lapply(df, range)
lapply(df, unique)
sapply(df, class)       #vector
sapply(df, sum)         #vector

#With Annonimous function
lapply(list, function(x) x[,2])  #takes the second col of each element

#vapply
vapply(df, class, character(1))
```


#### apply
Works over the margins of the array (rows or columns of matrix for ex)
```r
apply(mymatrix, 2, sum)   #sumes the columns; margin=2 means keep the second dimension (cols) and collaps the other dim
```
Note that specifically for row/col *sums* and *means*, there are specialized and optimized functions:
```r
rowSums = apply(x, 1, sum)     #colSumns
rowMean = apply(x, 1, mean)    #colMeans
```

#### tapply
Apply function over subsets of a vector
```r
tapply(x, index, fun)    #index should be a factor that groups the observations of x
```
 
#### mapply
Can take multiple list arguments; applies in parallel to various objects; there should be as many lists as arguments nneded by mapply. A way to vectorize a function.  
```r
mapply(rep,1:4, 3:7)     #repeat number 1 three-times, number 2 four-times etc
```

#### split
Similar to tapply but without the summary funcion.  
 

#### replicate
replicate(100, rpois(5, 10))   #returns a matrix




## Creating functions

``` R
myfunc <- function(x,y){
    ...
}
```

 - R functions return the last expression in the function
 - Default values to arguments like in python (n=10, m=NULL)
 - Partial matching of argument names allowed
 - R uses lazy evaluation: ie, `f(a,b){}` can be called with `f(2)` if b not used in f.
 - Variable number of arguments with ... (ie, \*\*kwargs):  `f(a,b,...)` . Any argument after ... must be named explicitly (an din full, ie, no partial matching)
 - The function can end with invisible(x) so not to autoprint object to console
 
Scoping rules:  

 - First R looks for the symbol in the 'global' environment (ie, our defined symbols)
 - If not found, R will look in the namespaces of each of the packages on the searchlist. The last included library goes in the top of the list.
 - There are separate namespaces for functions and non-functions
 - R uses 'Lexical scoping', ie, the values of free-variables (ie, not defined within a function) are searched for in the environment in which the function was defined, up to the top. Other languages use 'dynamic scoping' (ie, values are assigned looking at the environment where the function was *called* from).
 - An environment is a collection of symbolvalue pairs. A function plus an environment is a function closure.



## Debugging & Profiling

#### Debug
Indication levels:
 - message
 - warning : execution continues; warning appears at the end of execution
 - error : execution stopped
 - condtion : meaning exception, can be user defined
 
Debugging tools:
 - traceback() : prints function call stack; does nothing if there is no error
 - debug : flags a function and allows execution one line at a time; `n` next line
 - browser : supends execution of a funct at that particular point
 - trace : insert debugging code at specific places
 - recover : change default behaviour (during R session) of getting the console back, and instead will freez the execution of the failed function and look around with the browser
 
#### Profiling

Timing
 - user time: cpu
 - elapsed time: experienced by we (the users)

Rprof()
 - by.total : note that top level function takes always 100%.
 - by.self : most interesting format; substracts all other functions

```r
system.time()    #evaluates an expression
Rprof()
summaryRprof()
```

## Random number generation

Functions
```r
rnorm   #generate random normal variates
rpois   #generate random Poisson variates
rbinom  #binomial, discrete values
...

dnorm   #evalueate the normal probability density at a point
pnorm   #evaluate the cumulative distr func fo a Normal distr
qnorml  #evaluate the quantile function
...
```

Sample from aribrary vectors
``` r
sample(1:10, 4)   #take 4 randomly; default replace=FALSE
sample(1:10)      #permutation; default replace=FALSE
```

Seed  
```r 
set.seed(1)
```

## Plots

```r
plot(x,y,...)    #arguments:  xlab, ylab, main (title), col (color), xlim
plot(dist ~ speed, cars)    #'formula' interface

boxplot(formula = mpg ~ cyl, data = mtcars)

#Paramenters:
colors: red=2, 
```


## Snippets

```r
x <- matrix (rnorm(200), 20, 10)
```

## References  

- Base contents are from the Coursera course on R programming (Johns Hopkins)   https://github.com/rdpeng/courses/tree/master/02_RProgramming , and also from the genreal 'Data Science' specialization (Johns Hopkins)
- [Introduction to R Programming Part 1](https://www.youtube.com/watch?v=HKjSKtVV6GU)   (youtube video)  
- https://cran.r-project.org/doc/contrib/Torfs+Brauer-Short-R-Intro.pdf  
- https://www.rstudio.com/resources/cheatsheets/  
