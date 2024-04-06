+++
title = "How to set up LaTeX for multiscripted documents."
author = "Gabor Parti"
date = "2023-02-01"
weight = 11
description = ""
categories = []
tags = []
menu = "main:posts"
+++

This is a sample preamble of a LaTeX document I use for writing multiscripted documents, where the main document language is English. This is currently the best way I have found so far to make it all work the simplest way possible, including Chinese, Japanese, Korean (CJK), right-to-left scripts (RTL), and rendering Devanagari ligatures; all with a harmonious look and feel. I feel like academic publishers and typsetters are still scared of using "foreign scripts", maybe this can help a few people to include them more in their documents. We are using LuaLaTeX to compile.

### Latin, Greek, Cyrillic

Greek and Cyrillic are usually included in serious typefaces, such as [The Brill](https://brill.com/page/BrillFont/brill-typeface) (free for non-commercial use), [Noto Serif](https://fonts.google.com/noto/specimen/Noto+Serif), or the completely open [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine). Some fonts have their own packages to make your life easier (`\usepackage{libertine}`).

Free and open source font pairings that go well together (serif-sansserif-mono):

* Linux Libertine 
* Linux Biolinum
* Inconsolata

I can also recommend the classic [EB Garamond](https://en.wikipedia.org/wiki/EB_Garamond), if you wanna go for that 16th-century feel.

### Arabic, Hebrew, Devanagari

Automatically setting RTL scripts is a bit complicated, but it is possible. We can use the `babel` package to recognize and import a corresponding script whenever we detect a character from that script, and then we define fonts for that script. We have to set the `bidi` (bidirectional) parameter to basic. This way we don't have to use a macro or command to manually choose Arabic whenever we need it. See example:

```latex
% Languages, scripts, and fonts
\usepackage[main=english, bidi=basic]{babel}

% Automatic typesetting of writing systems
\babelprovide[import=ar, onchar=ids fonts]{arabic}
\babelfont[*arabic]{rm}{Noto Naskh Arabic}
```

You need to have the font on your system for it to work, or tell the compiler where to find it!

If you have more than a few words of Arabic and god forbid you use punctuation and brackets in the same line as a LTR script, or you mix English and Arabic paragraphs, you better just set the language to Arabic using `babel` just how the Overleaf [tutorial](https://www.overleaf.com/learn/latex/Multilingual_typesetting_on_Overleaf_using_babel_and_fontspec) tells you. 

Hebrew works the same.

For Devanagari you can set the renderer to Harfbuzz to render ligatures correctly.

```latex
\babelprovide[import=sa-Deva, onchar=ids fonts]{sanskrit-devanagari}
\babelfont[*devanagari]{rm}[Renderer=Harfbuzz]{Noto Serif Devanagari}
```

Babelfont allows you to scale your font to match the main font's uppercase or lowercase letters' heights, or you can set it to a specific scale. Example:

```latex
\babelfont[*devanagari]{rm}[Scale=MatchUppercase]{Noto Serif Devanagari}
```

### Chinese, Japanese, Korean (CJK)

For CJK scripts, I use the Noto typefaces, which are free and open source, available in many weights, in regular and bold styles, with or without *serifs*. 

After years of trial and error and figuring out this mess that are CJK, I found the easiest way to type Chinese (Traditional and Simplified), Japanese (Kanji, Hiragana, Katakana), and Korean (including Hangul and Hanja) in LaTeX, **without** using any commands or macros is the following:

1. Download CJK fonts from the [noto-cjk] (https://github.com/notofonts/noto-cjk) repository, for example, I am using the Regular and Bold styles of `NotoSerifCJKtc` found [here](https://github.com/notofonts/noto-cjk/tree/main/Serif/OTF/TraditionalChinese). (Variable fonts could not render bold styles correctly in my tests, so I use the regular and bold styles separately.)
2. Install them on your system.
3. Use the `kotex` package in your LaTeX file, and set the font you want to use. This package was originally created to support Korean, but it can also handle Chinese and Japanese, and if you specify a CJK font that has all three scripts, they wil all render correctly! See below:

```latex
\usepackage{kotex}
\setmainhangulfont{Noto Serif CJK TC}
```

That's it. If your latex compiler cannot find the font, maybe you have to wait a bit for the system to update the font cache. Alternatively, you can place them in a folder and set the path explicitly.

### Other fonts

If you want to use any other font occasionally, you can define them in the preamble using the `fontspec` package. For example, I use the Noto Serif Tibetan font for the Tibetan script, and I defined a command to use it:

```latex
% Other fonts
\usepackage{fontspec}
\defaultfontfeatures{Ligatures={TeX}}

% Define new fonts
\newfontfamily{\tibetanfont}{Noto Serif Tibetan}

% Commands to use the scripts
\newcommand{\bo}[1]{\tibetanfont{#1}\rmfamily}
```

In the document I can use the `\bo{}` command to write in Tibetan.

```latex
Tibetan: \bo{བོད་སྐད་}
```

This works for anything. Let's say you want to go wild with Cuneiform, but you don't want to install it on your system. You can do the following:

1. Download the font, e.g., [Noto Sans Cuneiform](https://fonts.google.com/noto/specimen/Noto+Sans+Cuneiform).
2. Move it to your project folder, under, say, 'fonts'.
3. Define a new font family:

```latex
\newfontfamily{\cuneform}[
    Path=./fonts/,
    Extension=.ttf,
    UprightFont=*-Regular,
    ]{NotoSansCuneiform}
```

4. Define a command to use it:

```latex
\newcommand{\cf}[1]{\cuneform{#1}\rmfamily}
```
5. Call it in the document:

```latex
Cuneiform: \cf{𒀭𒊩𒆪}
```

## The complete preamble

```latex
\documentclass[12pt]{article}

% Languages, scripts, and fonts
\usepackage[main=english, bidi=basic]{babel}

% Automatic import of scripts
\babelprovide[import=ar, onchar=ids fonts]{arabic}
\babelprovide[import=he, onchar=ids fonts]{hebrew}
\babelprovide[import=sa-Deva, onchar=ids fonts]{sanskrit-devanagari}

% Setting fonts for each script
\babelfont[*arabic]{rm}{Noto Naskh Arabic}
\babelfont[*hebrew]{rm}{Noto Serif Hebrew}
\babelfont[*devanagari]{rm}[Renderer=Harfbuzz]{Noto Serif Devanagari} 
% Available settigs: Scale=MatchUppercase; Scale=MatchLowercase; Scale=1.0; Language=Default

% Define default fonts to suppress warnings (https://tug.org/FontCatalogue/)
% \babelfont{rm}{Linux Libertine}
% \babelfont{sf}{Linux Biolinum}
% \babelfont{tt}{Inconsolata}



% Other fonts
\usepackage{fontspec}
\defaultfontfeatures{Ligatures={TeX}}
\setmainfont{Brill}

% East Asian writing systems
\usepackage{kotex}
\setmainhangulfont{Noto Serif CJK TC}

% Define new fonts
\newfontfamily{\tibetanfont}{Noto Serif Tibetan} % Font is installed on your system
\newfontfamily{\cuneform}[
    Path=./fonts/,
    Extension=.ttf,
    UprightFont=*-Regular,
    ]{NotoSansCuneiform} % Font is in your project folder

% Commands to use the fonts
\newcommand{\bo}[1]{\tibetanfont{#1}\rmfamily}
\newcommand{\cf}[1]{\cuneform{#1}\rmfamily}

\begin{document}

Testing fonts...

Latin: Latin \textbf{Latin} \textit{Latin} 

Greek: Ελληνικά \textbf{Ελληνικά} \textit{Ελληνικά}

Cyrillic: Кириллица \textbf{Кириллица} \textit{Кириллица}

Simplified Chinese: 简体中文 \textbf{简体中文}

Traditional Chinese: 繁體中文 \textbf{繁體中文}

Japanese: 日本語 \textbf{日本語} 

Hiragana: ひらがな \textbf{ひらがな} 

Katakana: カタカナ \textbf{カタカナ}

Korean: 한국어 \textbf{한국어}

Arabic: العربية \textbf{العربية}

Hebrew: עִבְרִית \textbf{עִבְרִית}

Devanagari: देवनागरी \textbf{देवनागरी}

Tibetan: \bo{བོད་སྐད་ \textbf{བོད་སྐད་}}

Cuneiform: \cf{𒀭𒊩𒆪}

\end{document}
```

Result:

![Multiscript](/images/multiscript.png)