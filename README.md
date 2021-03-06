# PySAL's Main Site 

This is the updated source to pysal.org

# Build instructions

This site is built using Hugo, see [Hugo website](https://gohugo.io/) for documentation and details. 

# Local testing 

Clone this repository locally, and cd into it:

``` 
git clone https://github.com/pysal/pysal.github.io
cd pysal.github.io 
```

Install `Hugo` to build the site. You can use [Homebrew](https://brew.sh/) to install Hugo on macOS and Linux.

```
brew install hugo
```

If you work with a different operating system please see the [Hugo documentation](https://gohugo.io/getting-started/installing/) for additional installing instructions. 

Run the following commands on your terminal to verify that Hugo runs correctly:

Show Hugo's location:
```
which hugo
/usr/local/bin/hugo
```
Verify it runs correctly:
```
hugo version
```
You should see something similar to this:
```
Hugo Static Site Generator v0.13 BuildDate: 2020-10-23T21:34:47-05:00
```
Now you can have Hugo build the website:

```
hugo server -D
```
Open your browser to `localhost:1313/`

Hugo is a fast site generator and will rebuild pages almost instantly. Depending on your text editor, you may have to manually save the file(s) you are working on to see the changes made to the website. 

To stop the server simply press `Ctrl` - `C` in your terminal. 

# Site Structure

Hugo uses the following [directory structure](https://gohugo.io/getting-started/directory-structure/) to organize content:

```
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes
```
The PySAL wesbite structure emulates this directory structure. 

# Updating the website

We have set up the website so that Hugo will automatically use the `partials` files under the `layouts` folder to render markdown files under the `content` folder. Unless the format/appereance needs to be changed, the files under `layouts` should be kept the same. 

The magic will happen once new files are added to the appropiate `content` folder which includes all of the files needed to render the site.

### how it works
Hugo will automatically look for front matter in each of the `markdown` file under the `content` directory and render the content using the structure of an html file under the `layouts/partials` directory. 

# what could potentially need to change

## subpackages
### how to update
If a new PySAL release contains a new subpackage, you will want to update the website with a new subpackage page. To do this, add another markdown file to the `content/"package"`  directory (replacing the "package" with the appropiate directory) and fill in the information contained in the front matter in the following format:

```
---
title: "esda" <!--name of the subpack-->
type : "explore" <!-- name of package that the submodule belongs to-->
image: "/esda.png" <!--path to image-->
description: "Esda implements methods for the analysis of both global (map-wide) and local (focal) spatial autocorrelation, for both continuous and binary data. In addition, the package increasingly offers cutting-edge statistics about boundary strength and measures of aggregation error in statistical analyses." <!-- description of package-->
link: "https://pysal.org/esda/index.html" <!--url to landing page of the submodule-->
---
```


## team
### how to update
to update the team page with a new team member, add another markdown file to the `content/team/` directory and fill in the information contained in the front matter in the following format:
```
---
type: "people" <!-- type wiill always equal people -->
title: "Levi Wolf" <!-- full name here -->
avatar: ""<!-- link to a user's image -->
affiliation: "University of Bristol" <!-- developer's affiliation -->
ghname: "ljwolf" <!-- Github username here -->
dev: "core" <!-- options are 'core' and 'alumni'-->
---
```
be sure to include the three dashes for YAML. Use "lastname.md" for the file naming convention


## news
### how to update
Add another markdown file with the following format to the `content/news/` directory:
```
---
title: "esda 2.0.0"
date: 2018-08-25
month: "08.25"
year: "2018"
rls: "08.25.2018"
description: "esda 2.0.0 released" 
type: "news"
url: "pypi.org/project/esda/2.0.0/"
---
```

## Deploying to GitHub Pages

In order to deploy the site you will need to follow the following commands, assuming you have cloned the repo locally, otherwise the changes may not be reflected on the site.

1. Make sure to `cd` into the directory where the site files are stored.  
2. Run the command `rm -rf public` to remove the public folder that may have been created by accident. *Note that you only have to run this command once. Running it after this step may cause problems in the deployment.
3. You will need to add the repository where the site will live as a submodule with the following command:
   
``` 
git submodule add -b master https://github.com/<USERNAME>/<USERNAME>.github.io.git public
```
* Make sure that the correct repositories are filled in. 
* You may get an error message similar to this: 
```
fatal: 'origin/master' is not a commit and a branch 'master' cannot be created from it
Unable to checkout submodule 'public'
```
 You can ignore this message. 

4.  Create the `deploy.sh` file using [Hugo's script](https://gohugo.io/hosting-and-deployment/hosting-on-github/#put-it-into-a-script). Make sure to save it on the main directory for the project. 
5.  Go back to your terminal and run the command:
```
./deploy.sh "your optional commit message"
```
The site should now live under the `<USERNAME>.github.io` or whichever custom domain it may have.

1. In order to make changes to the already deployed site, all you need to do is make any desired edits and follow the git workflow. Push the changes to the repo and don't forget to run the 
```
./deploy.sh "optional message" 
```
command. This command will collect the changes from the site files repo and push them to the deployed site. 

