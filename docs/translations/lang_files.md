---
title: Translation files
parent: Translations
---

# Translation files `*.sola`
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## About
**So**oty **La**nguage files `*.sola` are for translating or modifying lines in existing dialogue files `*.soot`.

## Generating

## Writing
![](/lang_1.png)
![](/lang_2.png)

## Installing

## Line ids

Line ids aren't just for translations, but for keeping track of choices, list states, and more.

The save system will probably bug out if you load a save game after modifying dialogue lines that don't have ids. So be sure to at least setup ids for choices and lists.

### Manually adding

```
#file.soot

orc: Let me tell you a story. #{orc1}
orc: It all started... #{ork2}

# mutiple lines can be 'clumped' in the file.
Once upon a time. #{intro}
There lived a king. #{+}
In a castle.        #{+}

# because sooty allows mutiple lines on one using the || pattern
# each can have a unique id
Are you sure? #{ask} || |> Yes, take me there. #{choose_y} || |> No, I could be wrong. #{choose_m}

# it's most important for lists and options to have unique ids
{[stop]} #{stop_1}
  Line 1
  Line 2
# You can call Dialogue.reset_list("stop_1") now to reset.

Do you want the dog or cat?
  - Cat #{chose_cat}
  - Dog #{chose_dog}
  - Return cat {{@chose chose_cat}}
      @reset_choice chose_cat
  - Return dog {{@chose chose_dog}}
      @reset_choice chose_cat
```

### Auto generating

*To write*
