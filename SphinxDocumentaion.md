# Generating Python Documentation with Sphinx

modified from https://sphinx-rtd-tutorial.readthedocs.io/en/latest/index.html

To replicate what was done for this first draft of GRiD docs (link), follow along below. To add to the existing draft with function/class descriptions, skip to Writing Docstrings. 

## Install Sphinx

## Create the Folder Structure

Create a folder to house your documentation. Most projects will have an additional folder that contains both the empty folder for documentation along with the project itself, but the project is specified with a path so this isn't essential.

Example folder structure: \
|-my_project \
  |-docs \
  |-project \
  |-README.md \

If the project has subfolders, each subfolder must have an `__init__.py` file. 

## Initialize and Configure a Sphinx Project

### Initialization
Inside your empty documentation folder (in the example, `docs`) run `sphinx-quickstart`. 

Set the project name and other information, and select `y` for build and source being separate. 

### Install Themes and Modify `conf.py`

### Modify `index.rst`

## Build the HTML Page

## Push to github pages

# Writing Docstrings

# Collaborating
