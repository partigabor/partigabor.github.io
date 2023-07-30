+++
title = "How to build and host a website with Hugo"
author = "Gabor Parti"
date = "2023-06-01"
weight = 11
description = "A concise tutorial on how to build and host a personal or professional website for free."
categories = ["technical","guide"]
tags = ["hugo","github","website","tutorial"]
menu = "main:posts"
# draft = "true"
+++

This is a concise, step-by-step guide on how to build a website - just like this one - with Hugo, and host it on Github Pages. Follow the hyperlinks for a quick explanation on each component.

## Requirements

{{< details "tldr" close >}}

1. Hugo (extended version)
2. Git
3. Github
4. VS Code (or whatever you use)

{{< /details >}}

### 1. Have [Hugo](https://gohugo.io/installation/) - the extended version - on your computer

[Hugo](https://www.youtube.com/watch?v=0RKpf3rK57I) is a website generator framework written in [Go](https://www.youtube.com/watch?v=446E-r0rXHI) (a computer language). It is a great tool to build static websites - FAST.

* To install Hugo on Windows, the easiest way is to first install [Scoop](https://scoop.sh/), a package manager for Windows, and then install Hugo (the extended version) from the command line using `scoop install hugo-extended`.

> {{< details "more..." close >}}
> {{< youtube 0RKpf3rK57I >}}
> {{< /details >}}

### 2. Have [git](https://git-scm.com/) on your computer

[Git](https://www.youtube.com/watch?v=hwP7WQkmECE) is a source code manager, a software that tracks the changes you make to your files in a project over time (version control), allowing you to update, inspect, and handle various stages of the project, even across a team of people.

* To install git 

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

## I. Building the website

We will create a new website using the theme [hugo-coder](https://github.com/luizdepra/hugo-coder) (MIT licence) authored and maintained by [Luiz de Prá](https://github.com/luizdepra). You can also find instructions on the theme's [GitHub page](https://github.com/luizdepra/hugo-coder.git).

{{< details "tldr" close >}}

1. `hugo new site whatever; cd whatever`
2. `git init`
3. `git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder`
4. add content and edit the `hugo.toml` config file, especially defining the theme to use (add the line: `theme = "hugo-coder"`)
5. `hugo server` to see your website locally on http://localhost:1313/
6. `hugo` to build your website

{{< /details >}}

### 1. Generate a new website with Hugo

Use your command line/terminal and navigate to where you want your project folder created (you can always move it somewhere else later) and run the command below, replacing `whatever` to whatever name you want. You can also open the terminal in VS Code by pressing <kbd>CTRL</kbd>+<kbd>`</kbd>.

    hugo new site whatever

 This command will create a folder with the name "whatever", and all the necessary files and folders for an empty Hugo website. Now navigate into this folder using `cd whatever`.

> if you get an error here, Hugo was not installed properly
 
{{< details "Navigation in the terminal" close >}}
E.g.: Make a directory called "new" by typing 

    md new

and hitting enter, then and navigate to it by typing

    cd new

and hitting enter. Now you should see that you are in `C:\Users\user\new>` on the terminal.

`md` = make directory, `cd` = change directory. To go up one level, enter 

    cd ..

{{< /details >}}

### 2. Initialize the git repo

Run a following command:

    git init

This will initialize a git repository of your folder, creating a `.git` hidden folder with lots of nasty code that you don't have to touch.

> If you get an error here, there is some problem with git.

### 3. Add a theme

We can now add a theme as a git submodule with the following code:

    git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder

This line of code will clone the Hugo theme's repository into our `themes` folder so we can use it on our website.

### 4. Edit the config file

In `hugo.toml` (previously `config.toml`), add the following line

    theme = "hugo-coder"

This tells our Hugo website to use the "Coder" theme we just downloaded to our themes folder. 

You also have to give the base URL for your website, edit the following line in the config file based on this example:

    baseURL = "https://username.github.io/whatever"

You can (and should) also edit other parameters later, since this config file contains all the main settings to your website. Look up the theme's Readme or the exampleSite to see how it works and what it can do, theme developers explain every option. You can also try and copy the contents of the exampleSite folder of the theme to your project's root folder and see what happens.

### 5. Run your website

    hugo server

This command will launch and host the website on your machine, you can access it in the browser http://localhost:1313/ (or by clicking this link from the terminal output). This is meant for development purposes, you can see and try using your website and even observe real-time changes as you tune your settings or add content!

### 6. Build

    hugo

That's it. Simply typing `hugo` into the command line and hitting enter will build and "publish" your website. The default location of this build will usually be a folder named `public`, which you can change by adding/editing a line in your configfile. For example: `publishDir = "docs"` will make your `hugo` command build and publish your website into a directory named `docs`.

## II. Hosting the website

### 7. Push to GitHub

After building your website with the `hugo` command, you have to push it to GitHub. This means that you will upload this git repository online and store it on [https://github.com/](https://github.com/) under your account. 

VS Code has a one-click solution for this via the button **<i class="fa fa-1x fa-github"></i> Publish to Github**, but you can use your terminal and call the classic lines below one-by-one to add all your changes to the present commit, add a commit message, add a new remote origin, and push the commit to the main branch of the repository (see [here](https://www.digitalocean.com/community/tutorials/how-to-push-an-existing-project-to-github)). 

    git add .
    git commit -m "First commit"
    git remote add origin https://github.com/user/repo.git
    git push -u -f origin main

>This is a step you must do every time you add new content to your website, and want to make the changes live.

### 8. Build and deploy

Now navigate to your repository on Github in your browser, click on "Settings" on the top panel, and find "Pages" on the left sidebar. This service, called *GitHub Pages*, is there to hosts websites. We will use *GitHub Actions* to automatically build and deploy the site, which even detects when you edit something and makes your changes live in a matter of minutes.

Under the section "Build and deployment", subsection "Source", select "GitHub Acions" instead of "Deploy from a branch". This will offer you to select from suggested *workflows*, where you will have to "browse all workflows" to find the one made for Hugo. Find and select the one for Hugo, and click **configure**. This step will create a `hugo.yml` in your project (whatever/.github/workflows/hugo.yml). You don't have to edit this file, unless you have previously changed the default directory to publish your website (public).

Click the green "Commit changes..." button in the top right corner, and wait a few minutes. You can follow GitHub Actions working in the background if you click on "Actions" in the top panel of your repository.

If all went well, you should have a website up and running under https://username.github.io/whatever, you can check if it's live under "Settings".

## III. Editing the website

If you want to edit your website, (1) just make the changes in your content, save them (2) run the `hugo` command to rebuild the website, and (3) commit and push your changes to GitHub. Good luck.

---

## IV. Extras

### Plotly

To host plotly visualizations on your website you need to add two shortcodes.

    load-plotly.html

```html
{{ if not ($.Page.Scratch.Get "plotlyloaded") }}
  {{ $.Page.Scratch.Set "plotlyloaded" 1 }}
  <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
{{ end }}
```

and

    plotly.html

```html
{{ $json := .Get "json" }}
{{ $height := .Get "height" | default "200px" }}
<div id="{{$json}}" class="plotly" style="height:{{$height}}"></div>
<script>
Plotly.d3.json({{$json}}, function(err, fig) {
    Plotly.plot('{{$json}}', fig.data, fig.layout, {responsive: true});
});
</script>
```

Then, you need to do 3 things. 

1. On the markdown page preamble, you need to add the line:

    `plotly = "true"`
2. Load plotly on the page with the load-plotly shortcode:

    `{{*< load-plotly >}}`

3. Call the plotly JSON file, which should be in your static folder. In the example below, the file is in a plotly subfolder inside static, and I have set the height to 400 pixels:

    `{{*< plotly json="/plotly/distribution_map.json" height=400 >}}`

{{< load-plotly >}}

{{< plotly json="/plotly/distribution_map.json" height=400 >}}



### BibTeX Citations

Use the [hugo-cite](https://github.com/loup-brun/hugo-cite) submodule.