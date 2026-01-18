# Some git basics


For starting off with git there are a small number of concepts you have to know.

Let's assume you are starting off with an existing repository on github.  
You want to "check out" the repository, which means to make a copy of all its code on your computer (or your account in RStudioServer).

The easiest way to do this is to create a new project in RStudio.

When you create the project, pick the option to "Use version control" and then git. 

Then copy the code link (that ends in .git) from the home page of the repository. 

Past the link into the space.  

Then the rest should happen automatically.

## Ready, Set, Go

Unlike the word processors that you may have used before git requires you to _intentionally save change.  This is actually really good, so long as you
remember to do it.

Saving is a three step process.   You can do this in the RStudio git pane or you can do it in the commant line.

Step 1: Stage your changes.  This mean mark which files you are ready to save.  You may not always want to save all of 
the files at one time. What's neat is that you can stage multiple files at once. Stage is the 'Ready' step, you are saying these
files are ready to be added, removed, renamed or modified. 

Step 2: Commit your changes.  Commit means that you are making a change that you expect to be permanent.  When you make a commit,
you have to include a commit message.  THis helps later for trying to remember what you were thinking at the time. This is the 'Set'
stage.

Step 3: Push your changes. This means to send your changes to the github repository.  This works as both a backup and to let other people (in this case your
instructor) .

One more command you will want to know is `Pull`.

When you pull, your files will update to match any changes that have been committed to the githug repository.  For example, your instructor may make a change.

Every time you start working, you should start by doing a Pull just in case there are changes.


