

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






