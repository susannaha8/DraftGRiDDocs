# Generating Python Documentation with Sphinx

Sphinx is software that autogenerates documentation for a python codebase based on the strings inside the files. I created a draft of Sphinx documentation for GRiD inside this repository (in the folder `/grid_draft_docs3`). To replicate what was done for this first draft of GRiD docs, follow along below. To add to my draft with function/class descriptions, Use the existing .rst files in this repository and skip to "Writing Docstrings". 

instructions modified from https://sphinx-rtd-tutorial.readthedocs.io/en/latest/index.html

## Install Sphinx

Open terminal on your computer and install Sphinx with the command specific to your computer's operating system (macOS, Linux, Windows etc.) 
https://www.sphinx-doc.org/en/master/usage/installation.html 

## Create the Folder Structure

Create a folder to house your documentation. Below is an example folder structure that shows both the docs folder and the project  with the code you are trying to document. The project and docs don't need to be in a folder together, this is just a common structure. 

Example folder structure: \
|-my_project \
\t  |-docs \
\t  |-project \
\t  |-README.md

If the project has subfolders, each subfolder needs an `__init__.py` file. 

## Initialize and Configure a Sphinx Project

### Initialization
Use `$ cd` to move into your empty documentation folder (in the example, `/docs`). Run `$ sphinx-quickstart`. 

Set the project name and other information, and select `y` for build and source being separate. 

### Install Themes, Set Project Path, and Modify `index.rst`

#### Themes
Sphinx has a variety of themes (https://sphinx-themes.org/). To use the "ReadTheDocs" theme, run the command `$ pip install sphinx-rtd-theme`. Open the `conf.py` file and set the html theme: `html_theme = 'sphinx_rtd_theme'`. You can do this for any other theme.

#### Path
To set the path to your code base, add the following lines to the top of your `conf.py` file:

`import os`

`import sys`

`sys.path.insert(0, os.path.abspath('../../GRiD'))`


If you put your project folder somewhere different than in the example, adjust the path to that folder accordingly. 

In `conf.py`, make sure that  `extensions = ['sphinx.ext.autodoc']`

#### index.rst

Since GRiD is made up of multiple files and folders, after the line `:caption: Contents:`, on a new line, add the word `modules`. This makes sure that Sphinx creates a modules.rst file and includes all the folders and files in the codebase. 

<img src="/modules.png" alt="index.rst file after edits" style="height: 300px;"/>

### Add and Modify the Template Files

Sphnix has an odd default where the word 'module' and 'package' show up after each entry in the table of contents. To remove this, follow this, I follow this stack overflow post: https://stackoverflow.com/questions/50361218/remove-the-word-module-from-sphinx-documentation/57520238#57520238

Use `$python3 -m site` to find where python's site-packages are on your computer. Go there and find `/sphinx/templates`. Inside, copy all the files into your `docs/source/_templates` folder. In those files, make the modification they show in the stack overflow post. 

## Build the HTML Page

Now that you have set up your project, you can run the command that will generate the .rst files. Inside your documentation folder (ex. `/docs`), run 
`$ sphinx-apidoc -f -M --separate -t=./source/_templates  -o ./source ../GRiD`. The last argument-- `../GRiD`-- is the path to your project, so adjust it accordingly. `-f` forces through the changes if the .rst files already exist, and the `-M` flag puts the module itself first instead of it's contents.

After running this command, a ton of .rst files show up in your `/docs/source` folder. Make any modifications to the .rst files manually.

Finally, run `$ make html` to build the webpages for your documention. To view your documentation, get the full path of the `index.html` file and put it into the search bar of your internet browser. It might look something like this:

<img src="/example.png" alt="GRiD draft table of contents" style="height: 300px;"/>

## Current GRiD Specific Issues

- Before you build, you cannot have the `__init__.py` in the top GRiD directory. To generate test docs, delete this file or create a docs specific /GRiD folder. 
- Current commands autogenerate to make the table of contents include `GRiD`, the top level directory. To manually correct this, go to `modules.rst` and delete the first two lines (`GRiD` and `====`). Adjust the tree's max_depth in `index.rst` to 1. 
- All of the functions associated with a CodeGenerator object appear in the same section of the docs, instead of their separate files (ex. `/algorithms` or `/helpers`)
- the path at the top of the page sometimes says `GRiD`, sometimes says `<no title>`

# Writing Docstrings

After you have written all of your functions, after the function template and before the function's contents, add a string with triple quotations. ("""description"""). This is a docstring, and it will appear in the autogenerated documentation. There is a specific format for sphinx docstrings that shows arguments and return values.

Visual Studio code has a great extension called autoDocString. After you install this, when you go to add a triple quote comment after the function description, you will see the following:

<img src="/docstring.png" alt="image of docstring being generated" style="height: 300px;"/>

once you press enter, the formated template will appear. You fill in your description, and sphinx will add it to the documentation when you run `$make html`. 

