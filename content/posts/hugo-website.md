+++
title = "(BETA) How to build a website with Hugo"
author = "Gábor Parti"
date = "2022-12-01"
weight = 11
description = "A concise tutorial on how to build and host a personal website for free."
categories = ["technical","guide"]
tags = ["hugo","github","website","tutorial"]
menu = "main:posts"
# draft = "true"
+++

{{< typography font="Raleway" size="90px" >}}
# NOT READY
{{< /typography >}}


This is a concise, step-by-step guide on how to build a website - just like this one - with Hugo, and deploy/host it on Github Pages. Follow the hyperlinks for a quick explanation on each component.

## Requirements

{{< details "tldr" close >}}

1. Hugo (extended version)
2. Git
3. Github
4. VS Code (or whatever you use)

{{< /details >}}

### 1. Have [Hugo](https://gohugo.io/installation/) - the extended version - on your computer

[Hugo](https://www.youtube.com/watch?v=0RKpf3rK57I) is a website generator framework written in [Go](https://www.youtube.com/watch?v=446E-r0rXHI) (a computer language). It is a great tool to build static websites - FAST.

> {{< details "more..." close >}}
> {{< youtube 0RKpf3rK57I >}}
> {{< /details >}}

### 2. Have [git](https://git-scm.com/) on your computer

[Git](https://www.youtube.com/watch?v=hwP7WQkmECE) is a source code manager, a software that tracks the changes you make to your files in a project over time (version control), allowing you to update, inspect, and handle various stages of the project, even across a team of people.

> {{< details "more..." close >}}
> {{< youtube hwP7WQkmECE >}}
> {{< /details >}}

### 3. Have a [Github](https://github.com/) account

[GitHub](https://www.youtube.com/watch?v=HkdAHXoRtos) is a website and a hosting service that allows you to manage your projects "remotely" (on the internet).[^remote] Projects hosted here are called "repositories", and a repository is basically a folder to store your project files. The technical term fo a folder is "directory".

[^remote]: As opposed to "locally", meaning on your machine.

> {{< details "more..." close >}}
> {{< youtube HkdAHXoRtos >}}
> {{< /details >}}

* Essentially, any website (and in fact most software) is just a folder with a bunch of text files "organized in a precise way". In this context, terms such as "Hugo project", "Git repo", or "root directory" all refer to the same folder: your future website.

* In this tutorial we will **generate** this folder and the necessary files with the help of Hugo (the *tool*), and we will publish it as a git repository (the project folder) on GitHub (the *storage*).

* We will also learn how to use an existing [Hugo theme](https://themes.gohugo.io/) (a template made by someone else) to supply the **looks** for our website. 

* Finally, I will show you how to build and **deploy** your website on [GitHub Pages](https://pages.github.com/), a feature on GitHub with this exact purpose, and how to automate(!) deployment.

Ideally, we want to edit and manage our files conveniently, so we need a text/code editor. (If you want to use the Notepad and the vanilla terminal, you can, but you are on your own.)

### 4. Have [Visual Studio Code](https://code.visualstudio.com/)

[VS Code](https://www.youtube.com/watch?v=KMxo3T_MTvY) is a lightweight, customizable code editor that provides you an integrated environment to inspect, edit, and manage files (including an explorer for your folder structure, advanced search functions, git, command lines, debugger, etc.). It is expandable with community built **extensions** to accommodate every possible technical need later, from code highlighters and compilers, to spell-checkers and Spotify shortcuts.

> {{< details "more..." close >}}
> {{< youtube KMxo3T_MTvY >}}
> {{< /details >}}

**All the above programs are free and open-source.**

***

## Main Steps: First Time Build

We will create a new website using the theme [hugo-coder](https://github.com/luizdepra/hugo-coder) (MIT licence) authored and maintained by [Luiz de Prá](https://github.com/luizdepra). You can also find instructions on the theme's GitHub page.

{{< details "tldr" close >}}

1. `hugo new site <name>`
2. `cd <name>`
3. `git init`
4. `git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder`
5. add content and edit `config.toml` (can also just copy the contents of the `exampleSite` directory from the theme's folder to the project root)
6. `hugo server` and http://localhost:1313/ to see your website locally
7. `hugo` to build your website

{{< /details >}}

#### 1. Open VSCode

Run VS Code and open the terminal inside VS Code by pressing <kbd>CTRL</kbd>+<kbd>`</kbd>.

#### 2. Generate a new website with Hugo

Navigate to the directory where you want to create your website project (you can always move it somewhere else later).

{{< details "more" close >}}
E.g.: Make a directory called "Projects" by typing 

    md Projects

and hitting enter, then and navigate to it by typing

    cd Projects

and hitting enter. Now you should see that you are in `C:\Users\USER\Projects>` on the terminal.

`md` = make directory, `cd` = change directory. To go up one level, enter 

    cd ..

{{< /details >}}

Type the following command into the command line (terminal)

    hugo new site whatever

This command will create a folder with the name "whatever", and all the necessary files for a Hugo website.

3. Install a theme


cont...