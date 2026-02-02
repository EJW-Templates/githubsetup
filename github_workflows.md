
# Github Workflows

In the postcards repository, there is a file that we have not looked at yet:  

build-postcards.yml

that is located in the `.github/workflows` folder.

"yml" as a ile extension refers to "yet another markup language." 
You also will see yaml at the beginning of many RMarkdown files.  



```
name: Build and Deploy Postcards

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  build-postcards:
    runs-on: ubuntu-latest
    permissions:
      contents: write  # Required for pushing to gh-pages branch

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup R
        uses: r-lib/actions/setup-r@v2
        with:
          r-version: 'release'

      - name: Setup Pandoc
        uses: r-lib/actions/setup-pandoc@v2

      - name: Install R dependencies
        run: |
          install.packages(c('rmarkdown', 'postcards'),
                          repos = 'https://cloud.r-project.org')
        shell: Rscript {0}

      - name: Render postcards site
        run: |
          rmarkdown::render('index.Rmd')
        shell: Rscript {0}

      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: postcard-site
          path: index.html

      - name: Deploy to GitHub Pages
        if: github.ref == 'refs/heads/main' && github.event_name == 'push'
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: .
          publish_branch: gh-pages
          exclude_assets: '.github,README.md,.gitignore,*.Rmd,*.Rproj'


```

Let's take it step by step.

First 
```
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:
```
This says that "on" (whenever there is a new) push or pull request to the main branch that the work flow should run.

(We'll talk about branches next.)

Next 

```
jobs:
  build-postcards:
    runs-on: ubuntu-latest
    permissions:
      contents: write  # Required for pushing to gh-pages branch

```

This is saying to run the build-postcards on the latest version of the Ubuntu operating system.  
Ubuntu is a variation of the Linux operating system. 

Next it takes us through the steps of the job.

```
     - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup R
        uses: r-lib/actions/setup-r@v2
        with:
          r-version: 'release'

      - name: Setup Pandoc
        uses: r-lib/actions/setup-pandoc@v2

```

This is checking out the repository just like you would check out any repository using git.
Then it installs R and a library called Pandoc, which is used to take a document from one format and translate it
to another format.

With that done
```
    - name: Install R dependencies
        run: |
          install.packages(c('rmarkdown', 'postcards'),
                          repos = 'https://cloud.r-project.org')
        shell: Rscript {0}

      - name: Render postcards site
        run: |
          rmarkdown::render('index.Rmd')
        shell: Rscript {0}
```
it installs the packages needed.  
And then it runs a function, exactly in the way you would in RStudion.  `rmarkdown::render('index.Rmd')`

Which is to say it is using the render command on the index.Rmd file that you edited with your information.

This creates a file `index.html` which you can also see if you run the render command. 

```
  - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: postcard-site
          path: index.html

      - name: Deploy to GitHub Pages
        if: github.ref == 'refs/heads/main' && github.event_name == 'push'
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: .
          publish_branch: gh-pages
          exclude_assets: '.github,README.md,.gitignore,*.Rmd,*.Rproj'
```

Then it uploads the file file from the gh-pages branch. It excludes certain files from the upload because those are not needed
for the web page. If you add your profile picture it will _not_ exclude that.

One thing that is interesting about it is that there are a lot of other files and resources that are needed
to make your web page look the way it does. 


