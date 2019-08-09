---
title: Software Coding - Python
keywords: software, development, coding, python
tags: [software_development, coding, language]
sidebar: coding_sidebar
permalink: /coding_python
folder: coding
---

## Introduction

Latest Python version 3.14.

## Setup `virtualenv` & `virtualenvwrapper`

It's a good practice to use isolated virtual environments for prototyping,
or starting a completely new Python project especially if introducing new 
or unfamiliar packages. `virtualenv` is a tool to create isolated Python 
environments.

`virtualenvwrapper` is a set of extensions to virtualenv that include: 
wrappers for creating and deleting virtual environments, managing development 
workflow, making it easier to work on more than one project at a time without 
introducing conflicts in their dependencies.

### Reference 

- [Python Guide - virtualenvs](https://docs.python-guide.org/dev/virtualenvs/)
- [Doc - virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/install.html)

### Installation

- Install packages

```
sudo pip3 install virtualenv virtualenvwrapper
virtualenv --version
```

- Set locations in `.bashrc` file; the folders for each virtual 
  environment will be stored in the `.virtualenvs` folder in the user's
  `$HOME` directory;

```
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
```

- Reload startup file
```
source ~/.bashrc
```

### Create virtual environment

For example, create a **new environment** called `tfserving` for a project:

```
mkvirtualenv tfserving -p python3
workon tfserving
```

If the project has a preset package requirements specified in the
`requirements.txt` file, then proceed to install:

``` 
cd <home_directory>/tfserving_project
pip3 install -r requirements.txt
```


## Online IDE

- [Repl.it](https://repl.it)