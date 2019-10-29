# [Projects](https://likarajo.github.io/Projects)
Website for my portfolio of projects and articles created using Blogdown, Hugo, and GitHub pages.

## Install R and RStudio
[cran.r-project.org](https://cran.r-project.org/)

## Create Project
Launch RStudio and create a New Project.

## Install *devtools* package
In RStudio console<br>
```r
install.packages("devtools")
```

## Install *blogdown* using *devtools*
In RStudio console<br>
```r
devtools::install_github("rstudio/blogdown")
library(blogdown)
```

## Install *hugo* using *blogdown*
In RStudio console<br>
```r
install_hugo()
```

## Create new site using *blogdown*
Go inside the project directory.<br>
In RStudio console<br>
```r
new_site()
```

## Install theme using *blogdown*
```r
install_theme("githubusername/theme-repository", theme_example = TRUE, update_config = TRUE)
```
OR<br>
Download the theme folder and put it inside /themes

## Setup GitHub pages to work with Hugo
Create a sub-branch **master** within the branch **sources**.<br>
Keep all the files inside the /public folder on the **master** branch, and keep everything on the **sources** branch.<br>

* Create a branch **sources** in the GitHub repository. So now there are two branches: **sources** and **master**.
* Make **sources** as the default branch.
* Checkout the **sources** branch in the project directory
  ```sh
  git checkout -b sources
  ```
* Run *setup.sh* to set up the sub branch 
  OR
  Perform the following steps
  * Add a README.md file to **sources** branch
    ```sh
    touch README.md
    ```
  * Delete the original ***master*** branch
    ```sh
    git branch -D master
    git push origin --delete master
    ```
  * Create and checkout an empty, orphaned **master** branch
    ```sh
    git checkout --orphan master
    ```
  * Clear cache
    ```sh
    git rm --cached $(git ls-files)
    ```
  * Create commit and push to the new **master** branch a file from the **sources**
    ```sh
    git checkout sources README.md
    git commit -m "Initial commit on master branch"
    git push origin master
    ```
  * Return to the **sources** branch
    ```sh
    git checkout -f sources
    ```
  * Remove the stale /public folder
    ```sh
    rm -rf public
    git add -u .
    git commit -m "Remove stale public folder"
    ```
  * Add the new **master** branch as a subtree
    ```sh
    git subtree add --prefix=public https://github.com/likarajo/Projects.git master --squash
    ```
  * Pull the just committed file(s) to avoid merge conflicts
    ```sh
    git subtree pull --prefix=public https://github.com/likarajo/Projects.git master
    ```
* Make, check and commit any new changes made in the local repo
  ```sh
  git status
  git add .
  git commit -m "updates"
  git push origin sources
  ```
* Run *deploy.sh* to make updates to the website 
  OR
  Perform the following steps
  * Pull the **master** branch into /public to help avoid merge conflicts
    ```sh
    git subtree pull --prefix=public https://github.com/likarajo/Projects.git origin master -m "Merge origin master"
    ```
  * Build the website
    ```sh
    hugo
    ```
  * Commit and Push all the updates to the **source** branch
    ```sh
    git add .
    git commit -m "updates"
    git push origin sources
    ```
  * Commit and Push the updated /public folder to the **master** branch
    ```sh
    git subtree push --prefix=public https://github.com/likarajo/Projects.git master
    ```
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
