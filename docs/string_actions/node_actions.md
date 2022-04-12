---
title: Node actions
parent: String actions
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

## Built in

The following are built in.

|Name|Desc|Examples|
|----|----|-------|
|`@Dialogue`|Dialogue autoload.|`@Dialogue.reset_list(id)`
|`@Music`|Music autoload.|`@Music.play song`<br>`@Music.stop_all`<br>`@Music.current`|
|`@SFX`|Sound effects autoload.|`@SFX.play coin`
|`@Scene`|Scene autoload.|`@Scene.goto`
|`@scene`|Current scene.<br>Automatically set whenever a scene is made current.
|`@msg`|Emits:<br>`Global.message(id: String, payload: Variant)`|`@msg msg_id true`
|`@version`|Returns current Sooty version.|`@version`|
|`@show_caption`|Called internally.|`@show_caption dog "Bark bark bark."`
|`@hide_caption`|Called internally.|
|`@captioner`|Set the current captioner, if there are more than one.|`@captioner top_left`

## Arguments
Arguments are seperated by spaces.
```
@my_func abc true 10
#my_func("abc", true, 10)
```
If you want to pass a string with spaces, wrap it in `""`
```
@msg "A message with spaces."
#msg("A message with spaces.")
```
To pass an array, join items with `,`
```
@boost_health 10 jane,mary,paul
#boost_health(10, ["jane", "mary", "paul"])
```

The last argument can be a `Dictionary` where items are separated by spaces, keys and values joined.
```
@damage 10 type:poison 2x:true tint:neon_green rand:3
#damage(10, {"type": "poison", "2x": true, "tint": "neon_green", "rand": 3})
```
## Adding node actions
There are two ways to add a node action.

![](/node_action_groups.png)

### Single function
Add a `Node` to a group starting with `@.` followed by a function name.
```gd
extends Node

func _init():
  add_to_group("@.damage")
  add_to_group("@.heal")

func damage(amount: int, type: String, kwargs := {}):
  pass

func heal(amount: int, kwargs := {}):
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

# Properties
When using `@` to request a property, it will only return the last Node's result.

```
# if there are multiple enemies, only the last one's result will show up here.

Enemy health is [@enemy.get_health].
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
