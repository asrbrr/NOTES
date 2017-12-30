

# R analysis workflow


## MOTIVATION

Having standarized ways of doing things is a good idea:  
 
 - it helps you while doing things because it removes friction
 - it helps others understand your work
 - it can be made to offer a 'batteries-included' approach
 - it is cool
 - it inspires others
 
 
Many of the things that we do are a one-off kind of analysis. You
woldn't want to build a proper package for it because it is not 
aimed at being reused elsewhere. Instead, there is a problem/question, 
there is some input, and hopefully in the end you arrive at some
output/conclusions. And that's it.
 
Simple R scripts (plus R projects) are convenient for this: 
you access the project, you source the scripts, you call 
the functions, you write some conclusions somewhere
and you are more or less done. However it is all too tempting to leave
them barebone and skip other parts that *will* help you
or others in the future (such as documentation, tests, use cases etc),
or that can help reuse some parts of the code.
 
Based on experience, I have ended up believing the best
is to follow as closely as possible the R packages structure, while using
the contents as scripts. You get the freedom of simple scripts
with the power of the project structure: the best of both worlds (sort of).
The key feature here is `devtools::load_all()`.


## Requirements

This is in relation to the R programming language, so you need:

 - RStudio
 - [devtools](https://github.com/hadley/devtools)
 - Read H.Wickham's excellent [R packages](http://r-pkgs.had.co.nz/) book


## WORKFLOW

### 1. Think

This is the hardest part in truth...

#### 1.1 Choose a (good) name


#### 1.2 Devise the overall approach

What is the true questions, what are the challenges, 
what are the options, what structure to attempt, 
what tools to use, what is the concrete use case, 
who are the users, will it need productionizing or not,
etc

This is the step that eventually (after many hours of work) you
are likely to end up thing *"if only I had thought of this at the
beggining..."*

#### 1.3 Draft some diagrams on paper/board

Paper is underrated these days...

#### 1.4 Explore available datasets, explore potential tools, ask

But keep it as simple as possible. It is all too tempting
to try out the new shiny & trendy package, but this
might as well be an overkill or simply a bad decision 
because of the hidden burden it introduces in learning it, 
mastering it, mantaining it, comminicating it to colleagues etc.
Hear the [Not So Standard Deviations](http://nssdeviations)
podcast for good advise on this.

#### 1.5 Iterate

Go back to point 0.2 and iterate this loop until
you start to *see* things with some clarity...




### 2. Create contents


#### 2.1 Create Rstudio project (of type package)

#### 2.2 Fill in the DESCRIPTION file

See [here](http://r-pkgs.had.co.nz/description.html) about it.


#### 2.3 Create files containing functions under R/

As usual, the file names should be ideally concise and self
describing and intuitive and all, and the same goes for the
function names. Which is so difficult to achieve...

It is practical to have conventions for file names, like:  
  - `analysis.R` for the main function(s) to call to run the analysis. 
  They orchestrate all the rest.
  - `plots.R` for plotting functions
  - `utils.R` (or `utils_dates.R`, `utils_db.R`, `utils_files.R` etc) for 
    auxiliary functions
  
I tend to have few files and quite some functions in each of them. This is
probably *not* the most widely recommended approach. However I feel very confortable
with this, because RStudio has the nice 'Document outline' tool that gives
you a great index view of the functions (and sections) it each file. Relatedly,
you should very frequently use the F2 and Ctr+. search options for functions.


#### 2.4 Write functions 

You may find convenient to create and use the 
following RStudio snippet. Just type "fun" and 
the this placeholder will be written for you.
What I like is that you get a (seggested) test
file related to this function right at the end for
easy creation/edit.

```r
snippet fun
	#' Title
	#'
	#' @param x
	#'
	#' @return
	#'
	#' @examples
	#' 
	#' @import assertthat
	#' @export
	#'
	${1:name} <- function(${2:x}) {
		${0}
	}
	#
	#   file.edit("tests/testthat/test-${1:name}.R")
	#   devtools::test(filter="${1:name}")
```


**Use Roxygen2 documentation**

Either use to structure created above by the snippet,
or in RStudio, press Ctr+Alt+Shift+R to add the documentation
section on top of each function.

Always add the description, param, return, export, import and example.
I tend to always add `@import assertthat` as a reminder
to use assertions, which is a very good idea.

**About the dependencies**

Do not use the `library(x)` or `require(x)` calls, as you would in scripts.
Instead write it as you would in a 
package in the `DESCRIPTION` file 
(also at times in `NAMESPACE` files, but making
use of Roxygen2, read [this](http://r-pkgs.had.co.nz/namespace.html) ), 
as follows:  

When requiring functions from a package (say, dplyr):
 1. Add it to the DESCRIPTION file under **`Depends:`**.
    It is a good idea to add version numbers (like `dplyr (>= 0.7)`).
    It is also a good idea to use `package::func` notation.
 2. Or add it to the DESCRIPTION file under `Imports`
    and always use `package::func` notation.
 3. Or add it to the DESCRIPTION file under `Imports`
    and also add it as a `@Import package` tag 
    (or more selectively, `@ImportFrom package fun`) in 
    the Roxygen header of the function.

The recommended way for packages in general is 2 
(see [this](http://r-pkgs.had.co.nz/namespace.html)),
but because this is in truth an analysis and not a full-featured
package, i simply use option 1. 
The rationel behing the options is this:
 *	Having dependencies explicit in a signle place 
 	(the DESCRIPTION file), with
 	version numbers, is great message for others.
 * 	The **`Depends:`** section (within the DESCRIPTION file) 
 	makes sure the packages are installed, and *attaches* them.
 	This allows you to skip the `package::fun` notation *in principle*.
	Besides, this is very convenient when coding/debugging, because
	at times you end up typing things in the console, and 
	`Depends` makes them facto available
	for you in intereactive use. As opposed
	to this, the **`Imports`** section does *not* attach the packages.
 * 	Remember however that if you end up building an actual
	package, not using the `package::fun` notation is bad, it 
	can make things not work. This is
	because `package::fun` would only load you package
	instead of attaching it.
	For packages, "*unless there is a good reason otherwise, 
	you should always list packages in Imports not Depends*" 
	[H.Wickham](http://r-pkgs.had.co.nz/namespace.html). 
 *	The `package::func` notation is a good idea in general,
 	regardless of the use of `Depends`/`Imports`,
 	because it adds clarity. However some packages are
	becoming lingua franca (like dplyr, ggplot2 etc) and
	doesnt make much sense to always fully quality them.
	That is why I thing `Depends` is good enough.
	For extra clarity, when opting to skip the `::`
	notation, ideally we would add the package or 
	function to our NAMESPACE with the `@import` tag.






