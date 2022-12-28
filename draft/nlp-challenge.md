+++
title = "NLP Challenge: Music"
date = "2022-10-26"
author = "Gábor Parti"
weight = 11
description = ""
categories = [
    "practice",
]
tags = [
    "jsgf",
]
menu = "main:posts"
+++

# NLP Challenge: JSGF Development

> Gábor Parti, 2022-10-27

Background
As part of the interview process, we would like you to complete a small NLP challenge.
The following is a Context Free Grammar, written using the Java Speech Grammar Format (JSGF)
(http://www.w3.org/TR/jsgf/):

```java
#JSGF V1.0 utf-8 en;

grammar music_play; 

public <music_play> = 
[can you] (put on | play) (<artist> | <song>); 

<artist> = 
the beatles | 
radiohead | 
lady gaga | 
pink floyd; 

<song> = 
comfortably numb | 
paranoid android | 
let it be | 
hey jude;
```

The above grammar is meant to be used to create utterances that express the desire (“intent”) to play music, which are then used as training data for statistical models for intent recognition and classification. As a reference, the above grammar can generate utterances like the following, using a custom parser:

```
[can you play]<unk> [the beatles]<artist> 

[can you put on]<unk> [paranoid android]<song>
```

To better understand the parsing process, keep in mind that:
* rules containing named entities that are used within the music play intent are used as tags for those entities (in the above grammar, this applies to `<artist>` and `<song>`).

* everything else is tagged as unknown (`<unk>`) by the parser.

## Your tasks

### Task 1: Extend the English grammar

#### 1.1 Extend the English JSGF grammar to cover at least the following utterances:

```
[i want to listen to]<unk> [jazz]<genre> [music]<unk>

[play me]<unk> [ummagumma]<album> [by]<unk> [pink floyd]<artist>

[put]<unk> [lady gaga]<artist> [on]<unk>
```

#### 1.1 Solution

```java
#JSGF V1.0 utf-8 en;

grammar music_play;

public <music_play> = 
(((i want to listen to) | ([can you] (put on | play [me] ))) 
((<song> | <album> [by <artist>] | <artist>) | [some] <genre> [music])) | 
(([can you] (put)) 
((<song> | <album> [by <artist>] | <artist>) | [some] <genre> [music]) on);

<artist> = the beatles | radiohead | lady gaga | pink floyd; 

<album> = ummagumma | yellow submarine | the fame;

<song> = comfortably numb | paranoid android | let it be | hey jude;

<genre> = jazz | pop | classical | hip-hop | [heavy] metal;
```

### Task 2: Localize the JSGF grammar in your language

#### 2.1 Localize the extended English grammar from Task 1.1 in your language (i.e., the language you are applying as a developer for). Feel free to add everything you think could help improve the quality of the generated utterances in your language.

#### 2.1 Solution

```java
#JSGF V1.0 utf-8 en;

grammar music_play;

public <music_play> = 
(((játssz | tegyél (fel | be) [nekem] [egy kis]) (<artist> | <genre>) [-t]) |
((tudsz [nekem] [egy kis]) (<artist> | <genre> [-t] játszani)) |
(((játszd le | le tudod játszani | lejátszod | tedd (fel | be) | (fel | be) tudod tenni | (felteszed | beteszed)) a) (((<song> | <album>) [-t]) (<album> [-t a] <artist> [tól]))))

<artist> = the beatles | radiohead | lady gaga | pink floyd; 

<album> = ummagumma | yellow submarine | the fame;

<song> = comfortably numb | paranoid android | let it be | hey jude;

<genre> = jazz | pop zene* | klasszikus zene* | hip-hop | metál zene*;
```

#### 2.2 Provide some sample utterances the JSGF can produce using the localized grammar.

```
[játssz]<unk> [the beatles]<artist> [-t]<unk>

[tudsz egy kis]<unk> [the beatles]<artist> [-t játszani]<unk>

[jazz]<genre> [-t akarok hallgatni]<unk>

[tegyél fel/be]<unk> [lady gaga]<artist> [-t]<unk>

[le tudod játszani a]<unk> [paranoid android]<song> [-t]<unk>

[lejátszod a]<unk> [paranoid android]<song> [-t]<unk>

[fel/be tudod tenni a]<unk> [paranoid android]<song> [-t]<unk>

[fel-/beteszed a]<unk> [paranoid android]<song> [-t]<unk>

[játszd le az]<unk> [ummagumma]<album> [albumot a]<unk> [pink floyd]<artist> [-tól]
```

#### 2.3 What possible issues do you think you could run into if you were asked to extend the grammar considerably and how would you suggest overcoming them? There is no single correct response to this question so please share any potential issues that come to mind.

The issue that I can think about now is about how the intent derived from the voice commands (rules) tie to the database of the device/software, how to connect songs to albums to artists. But this is not a grammar issue.

Other problems that come to mind relate to code-mixing, and multilingual commands. Can the speech recognition program listen to English named entities in a Hungarian sentence? What is the expectation for the pronunciation of languages with smaller resources? For example, would "play Celine Dion" be recognized even if the `<artist>` was pronounced with a strong Hungarian or French accent, when most voice assistants are trained on English speech?

Back to the question of extending the grammar to Hungarian, I currently see no major obstacles to overcome, but there are two specific features of the language that could complicate things. See 2.4.

#### 2.4 Which features of your language complicate the localization or writing of the grammar? How would you solve or work around these complications?

The most obvious feature of Hungarian that would complicate the grammar rule writing process is the **relatively free word order**. Essentially, this would just require the writing of more and/or extended rules to accommodate for the possible utterance structure users might say. With sufficient previous consideration, a whole range of possible variations can be written up to solve the issue of lax word order. 

Secondly, Hungarian is agglutinative, meaning that the language operates with a range of suffixes attached to the end of words. E.g., "play [Celine Dion]" would be "játssz [Celine Dion]t", where the '-t' is an object marker. This means that the actual named entities could have a different ending based on their role and position. (English solves this with prepositions, we use suffixes). It could even slightly change final vowels, (e.g. consider Hungarian rock band "Tankcsapda", and the utterance "play `<song>` from Tankcsapda", which would be rendered in Hungarian "játszad le a `<song>`-t a Tankcsapdától".

Lastly, Hungarian has vowel harmony, meaning that the suffix '-tól' ("from") as seen above could change into '-től' depending on the vowel (nucleus) of the final syllable.  

These problem have two possible solutions: either we extend the grammar to accommodate for different named entities with different endings (type of final syllable), or let the ML algorithm train itself to recognized named entities with and without suffixes.

On the other hand, other features of Hungarian can make this process easier, the orthography follows pronunciation and vice versa, and there are no significant differences between written and spoken Hungarian, nor huge variation in between regional dialects.