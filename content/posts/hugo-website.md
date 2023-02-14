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

# !!! UNDER CONSTRUCTION !!!

This is a concise, step-by-step guide on how to build a website - just like this one - with Hugo, and deploy/host it on Github Pages. Follow the hyperlinks for a quick explanation on each component.

## Prerequisites/installations

1. Have Hugo - the extended version - on your computer (install from: https://gohugo.io/installation/)

> [Hugo](https://www.youtube.com/watch?v=0RKpf3rK57I) is a website generator framework written in [Go](https://www.youtube.com/watch?v=446E-r0rXHI) (a computer language). It is a great tool to build static websites fast.

2. Have git on your computer (install from https://git-scm.com/)

> [Git](https://www.youtube.com/watch?v=hwP7WQkmECE) is a version control manager, a software that tracks the changes you make to your files in a project over time, allowing you to handle to source code across a team of people 

3. Have a Github account (sign up on https://github.com/)

> [GitHub](https://www.youtube.com/watch?v=HkdAHXoRtos) is a website and a hosting service that allows you to manage your projects remotely (on the internet). Projects hosted here are called "repositories", and a repository is basically a folder to store your project files.

Essentially, any website (in fact any software) is just a folder with a bunch of text files organized in precise ways. In this context, terms such as "Hugo project", "Git repo", or "root directory" all refer to the same folder. In this tutorial we will generate this folder and the necessary files with the help of Hugo (the tool), and we will publish it as a git repository (the project folder) on GitHub (the storage).

We will also learn how to use an existing [Hugo theme](https://themes.gohugo.io/) to supply the looks for our website, and I will show you how to build and deploy your website on GitHub Pages, a feature on GitHub with this exact purpose (and how to automate deployment).

Lastly, we want to manage our files and folder structures conveniently, so we need a text/code editor.

4. Have Visual Studio Code (https://code.visualstudio.com/)

> [VS Code](https://www.youtube.com/watch?v=KMxo3T_MTvY) is a lightweight code editor that provides you with an integrated environment to inspect, edit, and manage your files; with extensions to accommodate every possible technical need later.

**All the above programs are free and open-source.**




## Steps

#### 1. Open VSCode

Run VSCode and open the terminal inside VSCode by pressing <kbd>CTRL</kbd>+<kbd>`</kbd>

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