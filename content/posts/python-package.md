+++
title = "How to Publish a Python Package: A Rudimentary Pipeline"
author = "Gabor Parti"
date = "2022-10-01"
weight = 11
description = "A concise tutorial on how to publish an open source python package."
categories = ["technical"]
tags = ["python","github","documentation","tutorial"]
menu = "main:posts"
+++

# PIPELINE

This is a concise step by step rough-guide on how to package and publish an open source python project, accompanied by an auto-generated documentation website (readthedocs.io). This post are my own notes for my future self in case I forget how to do this, so the explanations are minimal. If lost, follow the actual tutorials in the footnotes.

> Sources and links to tutorials on the bottom.

##### Step 1. Create a python project manually[^7], or with Poetry[^8], or the cookiecutter[^1] package:

    pip install cookiecutter

    cookiecutter https://github.com/audreyr/cookiecutter-pypackage.git

##### Step 2. Manually add python scripts (submodules) in project subfolder(s) (modules).

Pay attention to folder structure[^7],

    root/
    └── scikit-talk/
        ├── __init__.py
        └── preprocessor.py

and the commenting syntax (docstrings) format.

    def add_nums(num1, num2):
        """This method will be used to add two numbers
            :param int num1: The first number
            :param int num2: The second number
            :returns: The sum of two numbers
            :rtype: int
        """
        answer = num1 + num2
        return 

##### Step 3. Build package for pypi[^2]:

    py -m pip install --upgrade pip

    py -m pip install --upgrade build

    py -m build

##### Step 4. Upload package to pypi[^2]:

    py -m pip install --upgrade twine

    py -m twine upload dist/*

##### Step 5. Create a git repo and push the package onto it:

    git init

    git add .

    git commit -m "ini"

    git branch -M main

    git remote add origin https://github.com/xyz/xyz.git

    git push -u origin main

then sync the repo in VSCode for future comfort.

##### Step 6. Make a "Read the Docs" account and import the project, build documentation[^3], follow the tutorial

    https://readthedocs.org/accounts/signup/

##### Step 7. Install Sphinx for generating documentation[^4], get familiar with it [^5]:

    pip install sphinx

with a readthedocs theme:

    pip install sphinx sphinx_rtd_theme 

##### Step 8. Initialize Sphinx. See tutorial![^6]

    sphinx-quickstart

then, accept defaults, then *change config*. Example conf.py below:

***

    # Configuration file for the Sphinx documentation builder.
    #
    # This file only contains a selection of the most common options. For a full
    # list see the documentation:
    # https://www.sphinx-doc.org/en/master/usage/configuration.html

    # -- Path setup --------------------------------------------------------------

    # If extensions (or modules to document with autodoc) are in another directory,
    # add these directories to sys.path here. If the directory is relative to the
    # documentation root, use os.path.abspath to make it absolute, like shown here.
    #
    import os
    import sys
    sys.path.insert(0, os.path.abspath('..'))


    # -- Project information -----------------------------------------------------

    project = 'Name'
    copyright = '2022, Copyright holder'
    author = 'Gabor Parti'

    # The full version, including alpha/beta/rc tags
    release = '0.0.01'


    # -- General configuration ---------------------------------------------------

    # Add any Sphinx extension module names here, as strings. They can be
    # extensions coming with Sphinx (named 'sphinx.ext.*') or your custom
    # ones.
    extensions = [
        'sphinx.ext.autodoc',
        'sphinx.ext.viewcode',
        'sphinx.ext.napoleon'
    ]

    # Add any paths that contain templates here, relative to this directory.
    templates_path = ['_templates']

    # List of patterns, relative to source directory, that match files and
    # directories to ignore when looking for source files.
    # This pattern also affects html_static_path and html_extra_path.
    exclude_patterns = ['_build', 'Thumbs.db', '.DS_Store']


    # -- Options for HTML output -------------------------------------------------

    # The theme to use for HTML and HTML Help pages.  See the documentation for
    # a list of builtin themes.
    #
    html_theme = 'sphinx_rtd_theme'

    # Add any paths that contain custom static files (such as style sheets) here,
    # relative to this directory. They are copied after the builtin static files,
    # so a file named "default.css" will overwrite the builtin "default.css".
    html_static_path = ['_static']

***

##### Step 8. Actually generate *.rst markdown files from python files using Sphinx (modules of scripts), run in parent folder:

    sphinx-apidoc -o docs xyz/

where xyz is the module folder containing python scripts

##### Step 9. include the generated modules.rst file in your index.rst, under contents write "modules":[^6]

Example:

    Welcome to XYZ's documentation!
    =======================================

    .. toctree::
    :maxdepth: 2
    :caption: Contents:

    modules

    Indices and tables
    ==================

##### Step 10. go into docs folder

    cd docs

##### Step 11. create html (if not first time, do clean before)

    (make clean html)

    make html

or

    (.\make clean html)

    .\make html

##### Step 12. Sync git in VSCode or push manually, should be live soon

##### Step 13. Done

## EXTRAS

If you want a DOI, consider uploading to Zenodo or OSF.

## SOURCES

[^1]: https://cookiecutter.readthedocs.io/en/stable/tutorials/tutorial1.html#questions
[^2]: https://packaging.python.org/en/latest/tutorials/packaging-projects/
[^3]: https://docs.readthedocs.io/en/stable/tutorial/index.html
[^4]: https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html
[^5]: https://www.sphinx-doc.org/en/master/tutorial/index.html
[^6]: https://towardsdatascience.com/documenting-python-code-with-sphinx-554e1d6c4f6d
[^7]: https://packaging.python.org/en/latest/tutorials/packaging-projects/ 
[^8]: https://python-poetry.org/docs/basic-usage/