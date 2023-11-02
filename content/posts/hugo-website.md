+++
title = "How to Build and Host a Website with Hugo"
author = "Gabor Parti"
date = "2023-06-01"
weight = 11
description = "A concise tutorial on how to build and host a personal or professional website for free."
categories = ["technical","guide"]
tags = ["hugo","github","website","tutorial"]
menu = "main:posts"
# draft = "true"
plotly = "true"
+++

This is a concise, step-by-step guide on how to build a website - just like this one - with Hugo, and host it on Github. Follow the steps and check out the links for further explanation on each component. This guide is made for non-experts, because I found most Hugo tutorials utterly useless and sparse for people new to ~~computers~~ web-development.

It might look daunting at first to go through all these steps below, but the reward is that once you get it right, updating and maintaining your website will be incredibly fast and easy. Comments and suggestions below are welcome!

## Table of Contents

[1. Requirements](#i)

[2. Building the Website](#ii)

[3. Hosting the Website](#iii)

[4. Editing the Website](#iv)

### Some explanations

* Essentially, any website (and in fact most software) is just a folder with a bunch of text files *"organized in a precise way"*. In this context, terms such as "Hugo project", "Git repo", or "root directory" all refer to the same folder: your future website.

* In this tutorial we will *generate* this folder and the necessary files with the help of **Hugo** (the tool), and then we will publish it as a **git repository** (the project folder) on **GitHub** (the online storage), where it will be hosted.

* In the meantime we will also learn how to use an existing Hugo **theme** (a template made by someone else) to supply the *looks* for our website.

* Finally, I will show you how to build and deploy your website with **GitHub Pages**, a service on GitHub with this exact purpose, and how to automate (!) future deployment after updating your content.



# 1. Requirements {#i}

{{< details "**tl;dr**" >}}
1. Hugo (extended version)
2. Git
3. Github
4. VS Code (or whatever you use)
{{< /details >}}

## 1.1. Have [Hugo](https://gohugo.io/installation/) - the extended version - on your computer

[Hugo](https://gohugo.io/) is a website generator framework written in [Go](https://www.youtube.com/watch?v=446E-r0rXHI) (a computer language). It is a great tool to build static websites - fast.

> {{< details "more..." close >}}
> {{< youtube 0RKpf3rK57I >}}
> {{< /details >}}

* To install Hugo on Windows, the easiest way is to first install [Scoop](https://scoop.sh/), a package manager for Windows, and then install Hugo from the command line (terminal) using `scoop install hugo-extended`. If you use Linux, you can probably figure it out yourself.
* In the future you can update Hugo from here as well. First, call `scoop update` to update Scoop and see the new versions of packages available to you (in this case we can type `scoop search hugo`, and then update it with `scoop update hugo-extended`.
* Use `hugo version` to check your Hugo version.

## 1.2. Have [git](https://git-scm.com/downloads) on your computer

[Git](https://git-scm.com/) is a source code manager, a software that tracks the changes you make to your files in a project over time (version control), allowing you to handle various stages and branches of your project (update, inspect, revert to, etc.), even across a team of people.

> {{< details "more..." close >}}
> {{< youtube hwP7WQkmECE >}}
> {{< /details >}}

* To install git, just follow the steps on its website.

## 1.3. Have a [Github](https://github.com/) account

[GitHub](https://github.com/) is a website and a hosting service that allows you to manage your projects "remotely" (on the internet, as opposed to "locally", meaning on your machine). Projects hosted here are called "repositories", and a repository is basically a folder to store your project files. The technical term for a folder is "directory".

> {{< details "more..." close >}}
> {{< youtube HkdAHXoRtos >}}
> {{< /details >}}

* Sign up/login on [https://github.com/](https://github.com/)

Ideally, we want to edit and manage our files conveniently, so we need a text/code editor. (If you want to use the Notepad and the vanilla terminal, you can, but you will be on your own.)

## 1.4. Have [Visual Studio Code](https://code.visualstudio.com/)

[VS Code](https://code.visualstudio.com/) is a lightweight, customizable code editor that provides you an integrated environment to inspect, edit, and manage files (including an explorer for your folder structure, advanced search functions, git, command lines, debugger, etc.). It is expandable with community built **extensions** to accommodate for every possible technical need later, from code highlighters and compilers, to spell-checkers and Spotify shortcuts.

> {{< details "more..." close >}}
> {{< youtube KMxo3T_MTvY >}}
> {{< /details >}}

* Download and install from [https://code.visualstudio.com/](https://code.visualstudio.com/)

<i class="fa fa-cc-nc" aria-hidden="true"></i> **All the above programs are free and open-source**

***

# 2. Building the Website {#ii}

{{< details "**tl;dr**" >}}
1. `hugo new site whatever; cd whatever`
2. `git init`
3. `git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder`
4. add content and edit the `hugo.toml` config file, especially defining the theme to use (add the line: `theme = "hugo-coder"`)
5. `hugo server` to see your website locally on http://localhost:1313/
6. `hugo` to build your website
{{< /details >}}

We will create a new website using the theme [hugo-coder](https://github.com/luizdepra/hugo-coder) (MIT licence) authored and maintained by [Luiz de Prá](https://github.com/luizdepra). You can also find instructions on the theme's [GitHub page](https://github.com/luizdepra/hugo-coder.git). You can choose other Hugo themes at [https://themes.gohugo.io/](https://themes.gohugo.io/), most of them will work similarly, (some might cause headaches), I chose a simple one here.

## 2.1. Generate a new website with Hugo

Use your command line/terminal and navigate to where you want your project folder created (you can always move it somewhere else later) and run the command below, replacing `whatever` to whatever name you want. You can also open the terminal in VS Code by pressing <kbd>CTRL</kbd>+<kbd>`</kbd>.

    hugo new site whatever

 This command will create a folder with the name "whatever", and all the necessary files and folders for an empty Hugo website. Now navigate into this folder using `cd whatever`.

> if you get an error here, Hugo was not installed properly
 
{{< details "Help on navigation in the terminal" close >}}
E.g.: Make a directory called "new" by typing 

    md new

and hitting enter, then and navigate to it by typing

    cd new

and hitting enter. Now you should see that you are in `C:\Users\user\new>` on the terminal.

`md` = make directory, `cd` = change directory. To go up one level, enter 

    cd ..

{{< /details >}}

### 2.2. Initialize the git repo

Run the following command:

    git init

This will initialize a git repository of your folder, creating a `.git` hidden folder with lots of nasty code that you don't have to touch.

> If you get an error here, there is some problem with git.

### 2.3. Add a theme

We can now add a theme as a git submodule with the following:

    git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder

This line of code will clone the Hugo theme's repository into our `themes` folder so we can use it on our website.

### 2.4. Edit the config file

In `hugo.toml` (previously `config.toml`), add the following line

    theme = "hugo-coder"

This tells our Hugo website to use the "Coder" theme we just downloaded to our themes folder. 

You also have to give an URL for your website, for this, you must edit the baseURL parameter in the config file (`hugo.toml`), see the example below. Basically, the "slug" after github.io is your repository's name.

    baseURL = "https://username.github.io/whatever"

If you name your repository to "username.github.io", you can use the simple "https://username.github.io" domain name for your personal website.

You can (and should) also edit other parameters later, since this config file contains all the main settings to your website. Look up the theme's Readme or the exampleSite to see how it works and what it can do, theme developers often explain every option. You can also try and copy the contents of the exampleSite folder of the theme to your project's root folder and see what happens.

### 2.5. Run your website

    hugo server

This command will launch and host the website on your machine, locally. You can access it in the browser http://localhost:1313/ (or by clicking this link from the terminal output). This is meant for development purposes, you can have a look and feel of your website and even observe real-time changes as you tune your settings or add content!

### 2.6. Build

    hugo

That's it. Simply typing `hugo` into the command line and hitting enter will build and "publish" your website. The default location of this build will usually be a folder named `public`, which you can change by adding/editing a line in your configfile. For example: `publishDir = "docs"` will make your `hugo` command build and publish your website into a directory named `docs`.[^hugo]

[^hugo]: I recently found out that you do not actually have to do this, GitHub Pages/Actions will build your website using Hugo automatically every time you push changes to it.

---

# 3. Hosting the Website {#iii}

{{< details "**tl;dr**" >}}
1. Git push
2. Configure GitHub Pages
{{< /details >}}

## 3.1. Push to GitHub

After building your website with the `hugo` command, you have to push it to GitHub. This means that you will upload this git repository online and store it on [https://github.com/](https://github.com/) under your account. 

VS Code has a one-click solution for this via the button **<i class="fa fa-1x fa-github"></i> Publish to Github**, but you can use your terminal and call the classic lines below one-by-one to add all your changes to the present commit, add a commit message, add a new remote origin, and push the commit to the main branch of the repository (see [here](https://www.digitalocean.com/community/tutorials/how-to-push-an-existing-project-to-github)). 

    git add .
    git commit -m "First commit"
    git remote add origin https://github.com/user/repo.git
    git push -u origin main

>This is a step you must do every time you add new content to your website, and want to make the changes live.

By the way the terminal and VSCode might ask you to configure your GitHub username and email address if you are doing this for the first time. I recommend installing the [GitHub CLI](https://cli.github.com/) and the command `gh auth login` to make this easier (= never appear again) in the future.

## 3.2. Build and deploy

Now we are going from <i class="fa fa-keyboard-o" aria-hidden="true"></i> *klackity-klack*... to <i class="fa fa-mouse-pointer" aria-hidden="true"></i> *clickety-click*.

* Go to your repository on **GitHub** in your browser, click on "Settings" on the top panel, and find "Pages" on the left sidebar. 

This service, called **GitHub Pages**, is there to hosts websites made by various website building tools (such as Hugo). We will use **GitHub Actions** to automatically build and deploy the site, which will even detect when you edit something and makes your changes live in a matter of minutes.

* Under the section "Build and deployment", subsection "Source", select "GitHub Acions" instead of "Deploy from a branch". This will offer you to select from suggested *workflows*, where you will have to "browse all workflows" to find the one made for Hugo. Find and select the one for Hugo, and click **configure**. This step will create a `hugo.yml` in your project (whatever/.github/workflows/hugo.yml). You don't have to edit this file, unless you have previously changed the default directory to publish your website (public), then you have to change it here as well.

* Click the green "Commit changes..." button in the top right corner, and wait a few minutes. You can follow GitHub Actions working in the background if you click on "Actions" in the top panel of your repository.

If all went well, you should have a website up and running under https://username.github.io/whatever, you can check if it's live under "Settings".

---

# 4. Editing the website {#iv}

If you want to edit your website, you just

1. Make the changes in your content and save them, 
2. Run the `hugo` command to rebuild the website, and 
3. Commit and push/sync your changes to GitHub.

Good luck!

---

{{< details "secret chapter for those who are determined" >}}

# 5. Extras {#v}

## 5.1. Plotly

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



## 5.2. BibTeX Citations

Use the [hugo-cite](https://github.com/loup-brun/hugo-cite) submodule.


## 5.3. Comments

If you want comments with [Utteranc.es](https://utteranc.es/), you need 3 steps.

1. Install Utteranc.es into your github repository

2. Create the partial `comments.html`:

```html
<script src="https://utteranc.es/client.js"
        repo="partigabor/partigabor.github.io"
        issue-term="pathname"
        theme="photon-dark"
        crossorigin="anonymous"
        async>
</script>
```

3. Set the config.toml/hugo.toml parameters:

```toml
[params.utterances]
  repo = "" # https://utteranc.es/#heading-repository
  issueTerm = "" # https://utteranc.es/#heading-mapping
  label = "" # https://utteranc.es/#heading-issue-label
  theme = "" # https://utteranc.es/#heading-theme
```

{{< /details >}}
