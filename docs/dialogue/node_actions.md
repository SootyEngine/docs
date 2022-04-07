---
title: Node actions
parent: Dialogue
nav_order: 20
---

# Node actions
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Node actions
Node actions are shortcuts for calling functions in the SceneTree.

Examples:
```
@Music.play song_id

@Scene.goto scene_id

@damage_hero 10 poison tint:green

@heal

@enemies_animate jump
```

## Adding node actions
There are two ways to *bind* to a node action.

![](/node_action_groups.png)

### Single function
Add a `Node` to a group starting with `@.` followed by a function name.
```gd
extends Node

func _init():
  add_to_group("@.damage")
  add_to_group("@.heal")

func _damage(amount: int, type: String, kwargs := {}):
  pass

func _heal(amount: int, kwargs := {}):
  pass
```
Now you can call `@damage` and `@heal` from a dialogue.
```
The orc slashes.

@damage 10 poison tint:green

Take a health potion?
  - Yes
    @heal 5
  - No
```

### All functions
Add a node to a group starting with `@` followed by any id you want.
```gd
extends Node

var health := 100

func _init():
  add_to_group("@hero")

func damage(amount: int, type: String, kwargs := {}):
  pass

func heal(amount: int, kwargs := {}):
  pass
```
Now you can call `@hero.damage` or `@hero.heal` or any other function it has.
```
The orc slashes.

@hero.damage 10

You have [@hero.health] health left.

Take a health potion?
  - Yes ((@hero.heal 5))
  - No
```

# Multiple responses

Actions are called for *all* nodes in the SceneTree that are part of the group.

You could have group `@john` and group `@mary` and both are part of group `@johnmary`:

```
#story.soot

@john.jump
john: What was that?

@mary.jump
mary: I heard it too!

@johnmary.jump
john mary: Woah!
```

Or you could add john and mary to group `@.jump` which could take a name or array.

```gd
#character.gd

func _init():
  add_to_group("@.jump")

func jump(id: Variant):
  if id is String and id == name:
    _jump()
  elif id is Array and name in id:
    _jump()
```
```
#story.soot

@jump john
john: What was that?

@jump mary
mary: I heard it too!

@jump john,mary
john mary: Woah!
```

# Type Conversion
Sooty tries to automatically convert strings to the appropriate type that the function wants. So try to make types explicit, or else Sooty will have to assume.

```
# not ideal
func my_func(id, amount):
  pass

# ideal
func my_func(id: String, amount: int):
  pass
```
