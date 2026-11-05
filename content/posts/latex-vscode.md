+++
title = "How to set up LaTeX on a local machine"
author = "Gabor Parti"
date = "2022-11-01"
weight = 11
description = ""
categories = ['technical']
tags = []
menu = "main:posts"
+++

This is a short step-by-step guide to setting up LaTeX on your local machine if you are using a cursed OS called Windows. The result is a stable offline solution, where you are not dependent on an internet connection, or third party servers like Overleaf.

## 1. Install TexLive

Download the latest version of [TexLive](https://tug.org/texlive/windows.html) installer from the official website. Running the installer will download and install LaTeX and hundreds of packages that are part of the deal. The installation process is pretty straightforward, but it takes **long**, so make sure you have a stable internet connection and a charging cable.

The installation will ask you if you need the front-end software called TeXworks, which is essentially a LaTeX editor. You can install it if you want, but I recommend using something else: 

## 2. Install VSCode as a LaTeX editor

Visual Studio Code is a light and snappy freeware, developed by Microsoft that you can tailor to your needs. It is an IDE (integrated development environment), i.e. code editor, a more versatile tool with Git integration and plenty of extensions to handle any kind of file not just those related to tex. You can use it for writing code, markdown, and of course LaTeX.

Download and install [Visual Studio Code](https://code.visualstudio.com/). 

## 3. Install LaTeX Workshop extension

Open VSCode and go to the Extensions tab on the left sidebar. Search for "LaTeX Workshop" and install it. This extension will allow you to compile your LaTeX documents directly from VSCode.

## 4. Configure LaTeX Workshop

Open the settings in VSCode (Preferences: Open User Settings (JSON)) by hitting `Ctrl + Shift + P` and search for preferences. You can configure LaTeX on which compiler and what recipes to use. For this, you need to edit the settings JSON file, like adding this:

```json

    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk (lualatex)",
            "tools": [
                "lualatexmk"
            ]
        },
        {
            "name": "lualatex➞biber➞lualatex2",
            "tools": [
                "lualatex",
                "biber",
                "lualatex",
                "lualatex"
            ]
        }
    ],
```

For example, this above will allow you to compile your document with LuaLaTeX using `latexmk` (which is the best compiler for modern documents with Unicode characters and other fancy stuff). You can fully customize the components and the recipes, you can search online how to do it.

If you sign in to VSCode (via GitHub for example), you can sync your settings across devices.





