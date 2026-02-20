# githubsetup
Instructions

To set things up make sure that you are already logged into github.  It may also ask you for your github password. 

Things have somewhat changed with new version of Rstudio aka Posit Workbench.

Basic set up for the class. 

If you are using your own computer, make sure you have the `usethis` package installed. This should also install the credentials package.

##  Identify yourself to git. Do this in the console.

Make sure your email is the same as the one you used in github. 

```
   usethis::use_git_config(user.name = "YourName", user.email = "your@mail.com")

```



## Now create your token 
In the Console type the command below. THis will open up a new tab/window in your browser.
  
```
  usethis::create_github_token()
```

Give it a name like token_348
Leave all the settings as they are exept change the expiration date to the end of the semester or June 15 to give it a couple of extra weeks.

Copy the token somewhere that you can retrieve it. For example a temporary text file or a note.


### If you are on rstudioServer setting your github PAT (Personal Access Token) has extra steps.

First set the cache.
```
usethis::use_git_config(credential.helper="cache --timeout=9000000")
```
This is only necessary on linux.  

##

Now set your credentials. Put your PAT where it says "YourPAT"

```
credentials::set_github_pat("YourPAT")
```

You should now be able to push to and pull from github.

