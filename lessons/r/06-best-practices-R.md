---
layout: page
title: Programming with R
subtitle: Best practices for using R and designing programs
minutes: 30
---



> ## Learning Objectives {.objectives}
>
> Define some best practices when working with R

1. Start your code with a description of what it is:


~~~{.r}
#This is code to replicate the analyses and figures from my 2014 Science paper.
#Code developed by Sarah Supp, Tracy Teal, and Jon Borelli
~~~

2. Run all of your import statments (`library`):


~~~{.r}
library(ggplot2)
library(reshape)
library(vegan)
~~~

3. Set your working directory before `source()`ing a script, or start `R` inside your project folder:

One should exercise caution when using `setwd()`. Changing directories in your script can limit reproducibility:

* `setwd()` will throw an error if the directory you're trying to change to doesn't exit, or the user doesn't have the correct permissions to access it. This becomes a problem when sharing scripts between users who have organized their directories differently.
* If/when your script terminates with an error, you might leave the user in a different directory to where they started, and if they call the script again this will cause further problems. If you must use `setwd()`, it is best to put it at the top of the script to avoid this problem.

The following error message indicates that R has failed to set the working directory you specified:

```
Error in setwd("~/path/to/working/directory") : cannot change working directory
```

Consider using the convention that the user running the script should begin in the relevant directory on their machine and then use relative file paths (see below).

4. Use `#` or `#-` to set off sections of your code so you can easily scroll through it and find things.

5. If you have only one or a few functions, put them at the top of your code, so they are among the first things run. If you have written many functions, put them all in their own .R file, and `source` them. Source will define all of these functions so that you can use them as you need them. For the reasons listed above, try to avoid using `setwd()` (or other functions that have side-effects in the user's workspace) in scripts you `source`.


~~~{.r}
source("my_genius_fxns.R")
~~~

6. Use consistent style within your code.

7. Keep your code modular. If a single function or loop gets too long, consider breaking it into smaller pieces.

8. Don't repeat yourself. Automate! If you are repeating the same piece of code on multiple objects or files, use a loop or a function to do the same thing. The more you repeat yourself, the more likely you are to make a mistake.

9. Manage all of your source files for a project in the same directory. Then use relative paths as necessary. For example, use


~~~{.r}
dat <- read.csv(file = "/files/dataset-2013-01.csv", header = TRUE)
~~~

rather than:


~~~{.r}
dat <- read.csv(file = "/Users/Karthik/Documents/sannic-project/files/dataset-2013-01.csv", header = TRUE)
~~~

10. R can run into memory issues. It is a common problem to run out of memory after running R scripts for a long time. In order to inspect your R session objects, you can list the objects, search current packages and remove objects that are currently not in use. A good practice when running long lines of computationally intensive sequential code is to remove temporary objects after they have served their purpose in.

~~~{.r}
interim_object <- data.frame(rep(1:100,10),rep(101:200,10),rep(201:300,10)) # Sample dataset of 1000 rows
object.size(interim_object) # Reports the memory size allocated to the object
rm(interim_object) # Removes only the particular object
ls()  # Lists all the objects in your current workspace
rm(list = ls()) # If you want to delete all the objects in the workspace and start with a new slate
~~~

11. Don't save a session history (the default option in R, when it asks if you want an `RData` file). Instead, start in a clean environment so that older objects don't contaminate your current environment. This can lead to unexpected results, especially if the code were to be run on someone else's machine.

12. Where possible keep track of `sessionInfo()` somewhere in your project folder. Session information is invaluable since it captures all of the packages used in the current project. If a newer version of a project changes the way a function behaves, you can always go back and reinstall the version that worked (Note: At least on CRAN all older versions of packages are permanently archived).

13. Collaborate. Grab a buddy and practice "code review". We do it for methods and papers, why not code? Our code is a major scientific product and the result of a lot of hard work!

14. Develop your code using version control and frequent updates!

> ## Discussion - Best practice {.challenge}
>
> 1. What other suggestions do you have?
> 2. How could we restructure the code we worked on today, to make it easier to read? Discsuss with your neighbor.
> 3. Make two new R scripts called inflammation.R and inflammation_fxns.R
> 4. Copy and paste the code so that inflammation.R "does stuff" and inflammation_fxns.R holds all of your functions. __Hint__: you will need to add `source` code to one of the files.
