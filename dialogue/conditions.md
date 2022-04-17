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
|`IF` or empty|The classic *if* statement. You don't need to type *if* though.|`IF apples > oranges`<br>or<br>`apples > oranges`|
|`ELIF`|If the previous condition failed, this one will be checked.|`ELIF apples > pears`|
|`ELSE`|If all other conditions failed, this will occur.`ELSE`|
|`MATCH`|A condensed pattern.|`MATCH apples`|

## Same line

This line will only show if the condition is met.
```
tramp: Spare some change? {{$player.coin > 0}}
```

## Multiple conditions

```
{{$player.coin > 0 AND @Scene.is_morning AND ~2+2==4}}
    The player has money,
    it's morning,
    and two plus two is still four!
{{else}}
    Things aren't go well, I suppose.
```

## Match

Check out the Godot [explanation](https://docs.godotengine.org/en/latest/tutorials/scripting/gdscript/gdscript_basics.html#match).

They can be a lot nicer/neater than if-else statements.

Match assumes the `$` (State) by default, but you can use any other.
<!-- {% raw %} -->
```
{{MATCH time.weekday}}
    {(MONDAY)}
        @sfx sad_audio
    {(TUESDAY)}
        john: Glad [b]mondays[] over.
    {(WEDNESDAY)}
        It's the middle of the week.
    {(THURSDAY)}
        john: The whole vibe shifts on thursday!
    {(FRIDAY)}
        @sfx happy_audio
        john: Aw yeah, friday!
    {(_)}
        It's the weekend.
```

### Array
You can use `AND` to test against an array.
```
{{MATCH time.month AND time.day_of_month AND time.period}}
    {(DECEMBER 24 EVENING)}
        It's Christmas eve. Get to bed.
    {{DECEMBER 25 MORNING}}
        Christmas morning!
    {(DECEMBER 25 _)}
        It's Christmas!
```

<!-- {% endraw %} -->


### Cases
<!-- {% raw %} -->
Cases use `{()}` instead of `{{}}`.

Case assume the `*` (Var) by default, but you can use any other.

```
{(TUESDAY)}             # "TUESDAY"
{(true)}                # true
{(x,y,1)}               # ["x", "y", 1]
{(class:archer lvl:3)}  # {"class": "archer", "lvl": 3}
{($score)}              # State.score
{(_)}                   # Special blank key
```

To test against mutltiple cases in the same brackets, use `OR`.
```
{(MONDAY OR TUESDAY)}
{(east OR west OR _)}
{(tint:green OR tint:blue OR tint:red)}

```

### Default case
Like Godot, the `_` key will be treated as an `ELSE` or default option. It will always evaluate to `true`.

<!-- {% endraw %} -->
