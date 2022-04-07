---
title: State overview
parent: States
nav_order: -1
---

# State overview
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## State overview
State data is what will be saved from play to play. Things like score, health, character stats, achievements, unlockables...

|Autoload|Data that will...|Folder|Examples|
|--------|-----------------|:----:|:------:|
|`State`|Change on each playthrough.|`res://states`|Score<br>Health<br>Stats|
|`Persistent`|Stay the same each playthrough.|`res://persistent`|Achievements<br>Unlockables|



## Adding state data

- Create a script extending a `Node`.
- Initialize your variables.
- Add any functions you may want.
- Save to `res://states/`
- Done

This data will be available in script, and will automatically save if changed.

*Alternatively there are [`.soda` files](./docs/states/data_files.md).*

```gd
#my_states.gd

extends Node

var score := 0
var my_name := "Traveler"
var health := 100
var has_key_1 := false
var has_key_2 := false
var has_key_3 := false
var has_prize := false

func boost_score(amount := 1):
    score += amount

func has_all_keys() -> bool:
    return has_key_1 and has_key_2 and has_key_3
```

Now we can access these in a dialogue.
<!-- {% raw %} -->

```
#story.soot

=== the_rabbits_keys

    You come across the rabbit.

    {{has_all_keys()}}
        {{not has_prize}}
            rabbit: You got them all, [$my_name]! Good job.
            ~has_prize = true
            $boost_score 20
        {{else}}
            rabbit: Good job finding those keys.
    {{else}}
        rabbit: I need those keys!


```
<!-- {% endraw %} -->

## Accessing

They can be accessed at:
- `State` in Godot: `State.characters.paul.name`.
- `~` in dialogue: `~characters.paul.name`


## Saving
Sooty will automatically save any values that changed, and only values that changed.

**WARNING:** Properties across scripts should be unique, as only the first property with a name will ever be returned.

Only one of these properties will be saved.
```gd
#characters.gd

var fields := Character.new({name="Mr. Fields"})
```
```gd
#locations.gd

var fields := Location.new({name="The Fields"})
```

## State signals
The `State` class has signals you may find useful:  

|Signal|Desc|
|------|----|
|`changed(property: Array[String])`|Property that was changed.|
|`changed_to(property: Array[String], to: Variant)`|Property that was changed and what it was changed to.|
|`changed_from_to(property: Array[String], from: Variant, to: Variant)`|Property that was changed, it's old value, and it's new value.|

`property` is often a path: `my.nested.property`.

You can manually trigger them by calling:
```gd
State["nested.property.path"] = value
# or
State._set("nested.property.path", value)
```
