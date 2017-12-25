

# R analysis workflow


## Motivation

Having standarized ways of doing things is a good idea:  
 
 - it helps you while doing things because it removes friction
 - it helps others understand your work
 - it can be made to offer the 'toolkit' or the 'batteries-included' approach
 - it is cool
 - it inspires others
 
 
 Many of the things that I do are a one-off kind of thing. You
 woldn't want to build a proper package for it because it is not 
 aimed at being reused elsewhere. Instead, there is a problem
 or question, there is some input, and hopefully there is some
 output or conclusions and that's it.
 
 Simple R scripts (plus R projects) are convenient for this: 
 you access the project, you source the scripts, you call 
 the functions, you write some conclusions somewhere
 and you are more or less done. However it is all too tempting to leave
 them barebone and skip other parts that *will* help you
 or others in the future (such as documentation, tests, use cases etc),
 or that can help reuse some parts of the code.
 
After reading various recommendations in the interet, I believe the optimum
is to follow as closely as possible the R packages structure, while using
the contents as scripts. The key feature here is `devtools::load_all()`,
and this changes your life :-)


## Requirements

This is in relation to the R programming language, so you need:

 - RStudio
 - [devtools](https://github.com/hadley/devtools)
 - Read H.Wickham's excellent [R packages](http://r-pkgs.had.co.nz/) book


## Workflow

### 0 Think

#### 0.1 Choose a name

This is well known to be amongst the most difficult steps in the process...

#### 0.2 Think the approach

What is the true questions, what are the challenges, 
what are the options, what structure to attempt, 
what tools to use, what is the concrete use case, 
who are the users, will it need productionizing or not,
etc

This is the step that eventually (after many days of work) you
are likely to end up thing *"if only I had thought of this at the
beggining..."*

#### 0.3 Draft some diagrams on paper/board

Paper is underrated these days...

#### 0.4 Explore available datasets, explore potential tools

But keep it as simple as possible. It is all too tempting
to try out the new shiny & trendy package, but this
might as well be an overkill or simply a bad decision 
because of the hidden burden it introduces in learning it, 
mastering it, mantaining it, comminicating it to colleagues etc

#### 0.5 Iterate

Go back to point 0.2 and iterate this loop until
you start to *see* things with some clarity...

### 1. Create Rstudio project of type package

### 2. Create files containing functions under R/

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
you should very frequently use the F2 search option for functions.


### 3. Write functions 

#### 3.1 Use Roxygen2 documentation

In RStudio, press Ctr+Alt+Shift+R to add the documentation
section on top of each function.

Always add the description, param, return, export, import and example.


#### 3.2 Dependencies and functions form other packages

Do not use the `library(x)` or `require(x)` calls. 
Instead write it as you would in a 
package (in the `DESCRIPTION` and/or `NAMESPACE` files, but making
use of Roxygen2), as follows:  

 1. When requiring functions from a package (say, dplyr), 
    add it to the DESCRIPTION file, under the
   **`Depends:`** section (instead of the `IMports:` section).
   This makes sure that the packages
   are installed when you load your analysis, and complains if not.
   Note that this is perhaps *not* the best practice for packages (see 
   [this](http://r-pkgs.had.co.nz/namespace.html) section
   of R packaes book: "*Unless there is a good reason otherwise, 
   you should always list packages in Imports not Depends*"), but 
   remember that we are not trying to 
   build a real package but an analysis. The effect
   that this has is that the packages listed there are loaded 
   *and* attached when your code is 'attached', so they are the facto available
   for you in intereactive use.  However, note also that if you were to
   actually  build it as a true package and call
   functions within it with the mypckg::func notation, then
   your package is *loaded* but not *attached*, and neither are 
   the packages under the `Depends` section, which causes the function
   calls to these packages that are not fully qualified (with `::`) to fail.
   
 2. Additionally, strive to use the `package::function` notation 
 to call external functions whenever reasonable. This is to
 follow best practices, to add clarity to the code, and to try 
 to simplify the process of reusing the code elsewhere (perhaps
 builind a true package later on, or moving parts of the code of
 your analysis to an actual package).
 
 3. For extra clarity, if you are not going to follow  `package::function`
 notation, then add the package name as a Roxygen2 `@import` tag on the function
 documentation section: for example, `@import assertthat`. (Or if
 you are more picky, for example `@importFrom assertthat assert_that`)




