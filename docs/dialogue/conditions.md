---
title: Conditions
parent: Dialogue
nav_order: 2
---

# Conditions
{: .no_toc }


## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Overview
![](/conditions.png)

<!-- {% raw %} -->
Conditions prevent lines from running if they don't pass a test.  
They are written between `{{}}` tags.
<!-- {% endraw %} -->

|Head|Description|Example|
|----|-----------|-------|
|`if` or empty|The classic *if* statement. You don't need to type *if* though.|`if apples > oranges`<br>or<br>`apples > oranges`|
|`elif`|If the previous condition failed, this one will be checked.|`elif apples > pears`|
|`else`|If all other conditions failed, this will occur.`else`|
|`match`|A condensed pattern.|`match apples`|

## Match

Check out the Godot [explanation](https://docs.godotengine.org/en/latest/tutorials/scripting/gdscript/gdscript_basics.html#match).

Sometimes they can be a lot nicer/neater that if-else statements.

<!-- {% raw %} -->
```
{{match time.weekday}}
    {{MONDAY}} @sfx sad_audio
    {{TUESDAY}} john: Glad [b]mondays[] over.
    {{WEDNESDAY}} It's the middle of the week.
    {{THURSDAY}}
        john: The whole vibe shifts on thursday!
    {{FRIDAY}} @sfx happy_audio
        john: Aw yeah, friday!
    {{_}} It's the weekend.
```
<!-- {% endraw %} -->

Soon this will support array and dict patterns.
