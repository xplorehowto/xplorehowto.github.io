---
title: Software Coding - Python
keywords: software, development, coding, python
tags: [software_development, coding, language]
sidebar: coding_sidebar
permalink: /coding_python
folder: coding
---

## Introduction

Latest Python version `3.7.4`.
Ubuntu `18.04` comes with pre-installed Python `3.6.5`.

**NOTE:** upgrading Python on Ubuntu requires build from source. 

### References:

- [Real Python](https://realpython.com/){:target="_blank"}  
  Excellent Python tutorial website;


## Python "modules" and "packages"

Python provides two constructs to facilitate [modular programming](https://en.wikipedia.org/wiki/Modular_programming): 
modules and packages.
- module is the most basic method; module can be built-in, or written in Python,
  or C. A "python" file (i.e., contains python codes and has `py` filename 
  extension is a module
- package is a grouping of modules in a folder such that it can be referenced
  using dot notation to avoid module names collision.  

Python package is distributed in the form of archived file (`.whl`). 
The wheel file is uploaded to repository, [Python Package Index](https://pypi.org/)
and other indexes, to share with others.
  
`pip` is the recommended "package installer" for python.

### Install `pip`

```
apt install python3-pip
```

Use pip to install packages from the [Python Package Index](https://pypi.org/)
and other indexes. Additional setup is needed to pull from other indexes 
(i.e., package repository) as discussed below.
  
  
[ALTERNATIVE] - Download and Install
```
# Download and install pip
wget https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
```

### Setup additional package repository

The setup file is `pip.conf`, or `pip.ini` for Windows; that can be found in
one or more locations due to: platform variations, or scope (i.e., site-wide,
per-user, etc.)

For Ubuntu, the file does not exist by default; can be added to `/etc/pip.conf`:  
```
[global]
timeout = 60
index-url = https://download.zope.org/ppix
```

For Raspbian, the default setup, `/etc/pip.conf`, points to an extra repo:
```
[global]
extra-index-url=https://www.piwheels.org/simple
```

For detailed, refer to [Pip User Guide](https://pip.pypa.io/en/stable/user_guide/)

### Setup trusted-host

For example,
```
pip install --trusted-host pypi.python.org
```

### Useful commands

```
pip install [package-name]
pip uninstall [package-name]
pip search [package-name]
pip freeze > requirements.txt
pip install -r requirements.txt --trusted-host

```


### References

- [Python Modules and Packages](https://realpython.com/python-modules-packages/){:target="_blank"}

- [Packaging Python Projects](https://packaging.python.org/tutorials/packaging-projects/#uploading-your-project-to-pypi){:target="_blank"}

- [Pip User Guide](https://pip.pypa.io/en/stable/user_guide/){:target="_blank"}


## Setup `virtualenv` & `virtualenvwrapper`

It's a good practice to use isolated virtual environments for prototyping,
or starting a completely new Python project especially if introducing new 
or unfamiliar packages. `virtualenv` is a tool to create isolated Python 
environments.

`virtualenvwrapper` is a set of extensions to virtualenv that include: 
wrappers for creating and deleting virtual environments, managing development 
workflow, making it easier to work on more than one project at a time without 
introducing conflicts in their dependencies.

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
`requirements.txt` file, then proceed to install. For example,

``` 
cd <home_directory>/tfserving_project
pip3 install -r requirements.txt
```

### Exit from the virtual environment

```
deactivate
```

### Delete virtual environment

```
rmvirtualenv <ve_name>
```

### Reference 

- [Python Guide - virtualenvs](https://docs.python-guide.org/dev/virtualenvs/){:target="_blank"}

- [Doc - virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/install.html){:target="_blank"}


## Jupyter

- [Jupyter](https://jupyter.org/index.html){:target="_blank"}
- [Jupyter Doc](https://jupyter.org/documentation){:target="_blank"}
- [Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/){:target="_blank"}
- [JupyterLab](https://jupyterlab.readthedocs.io/en/latest/index.html){:target="_blank"}

Notebook:
```
jupyter notebook
```

JupterLab:
```
jupyter lab
```

### JupyterHub

- [JupyterHub Github](https://github.com/jupyterhub){:target="_blank"}


## Online IDE

- [Repl.it](https://repl.it){:target="_blank"}

- [Python Fidde](http://pythonfiddle.com/)

- [Trinket](https://trinket.io/)

- [Python.org console](https://www.python.org/shell/)

- [Colaboratory - Google interactive python notebook](https://colab.research.google.com){:target="_blank"}
