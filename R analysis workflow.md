

# R analysis workflow


### Motivation

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


# Dependencies

This is in relation to the R programming language, so you need:

 - RStudio
 - [devtools](https://github.com/hadley/devtools)


# Workflow

### 0 Think

#### 0.1 Choose a name

This is well known to be amongst the most difficult steps in the process...

#### 0.2 Think the approach

What is the true questions, what are the challenges, 
what are the options, what structure to attempt, 
what tools to use, what is the concrete use case, 
whoe are the users, will it need productionizing or not,
etc

This is the step that eventually (after many days of work) you
are likely to end up thing *"if only I had thought of this at the
beggining..."*

#### 0.3 Draft some diagrams on paper/board

Paper is underrated these days...

#### 0.4 Explore datasets, explore tools

#### 0.5 Iterate

Go back to point 0.2 and iterate this loop until
you start to *see* things

### 1. Create Rstudio project of type package

### 2. Write functions under R/

(I must say that I havent found really good use cases
for R classes, so I stick to functions and pipes)

As usual the file names should be ideally concise and self
describing and intuitive and all, and the same goes for the
function names. Which is so difficult to achieve!

It is practical to have conventions for file names, like:  
  - `analysis.R` for the main functions to call to run the analysis. 
  They orchestrate all the rest.
  - `plots.R` for plotting functions
  - `utils.R` (or `utils_dates.R`, `utils_db.R`, `utils_files.R` etc) for 
    auxiliary functions
  
I tend to have few files and quite many functions in each of them. This is
probably *not* the most widely recommended approach. However I feel very confortable
with this, because RStudio has the nice 'Document outline' tool that gives
you a great index view of the functions (and sections) it each file. Relatedly,
you should very frequently use the F2 search option for functions.

#### Dependencies

Do not use the `library(x)` or `require(x)` calls. 
Instead write that as you would in a 
package (in the `DESCRIPTION` and/or `NAMESPACE` files).

