---
title: States
has_children: true
nav_order: 20
---

# Mods
[About mods](#docs/states/mods.md)

Everything is treated as a mod.  
`res://` is loaded as if it were a mod.  

# Adding State Data
State data is what will be saved from play to play. Things like score, health, character stats, achievements, unlockables...

|Type|Data that will...|Examples|Folder|Autoload|
|----|-----------|:------:|:----:|:-----------------------:|
|Temporary|Change on each playthrough.|Score<br>Health<br>Stats|`res://states`|`State`|
|Persistent|Stay the same regardless of playthrough.|Achievements<br>Unlockables|`res://persistent`|`Persistent`|

Simply create one or more scripts in the appropriate folder, extending any *Node*, and initialize like any other variable.  
These nodes are created at startup and added to their autoload (State or Persistent) and should only be accessed through their Autoload parent.

```
# my_states.gd
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

Now we can access these in a `.soot` dialogue.

```
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

## Initializing the state
Create a script in `res://states` that extends any `Node`.  
On startup, Sooty will add all scripts in this folder as children of the `State` node.  
All of their properties and functions are now accessible to the scripting system.

```
#state.gd
extends Node

var score := 0

func my_score():
	return "[b]%s[]" % score

func boost_score(amount := 1):
	score += amount


#story.soot
My score is [$my_score].
$boost_score 1234567
My score plus 1,234,567 is [$score].
```

Sooty will automatically save any values that changed, and only values that changed.

*WARNING:* Properties across scripts should be unique, as only the first property with a name will ever be returned.

```
# Only one of these properties will be saved.

#characters.gd
var fields := Character.new({name="Mr. Fields"})


#locations.gd
var fields := Location.new({name="The Fields"})
```

The `State` class has signals you may find useful:  

|Signal|Desc|
|------|----|
|`changed(property: Array[String])`|Property that was changed.|
|`changed_to(property: Array[String], to: Variant)`|Property that was changed and what it was changed to.|
|`changed_from_to(property: Array[String], from: Variant, to: Variant)`|Property that was changed, it's old value, and it's new value.|

`property` is often a path: `my.nested.property`.
