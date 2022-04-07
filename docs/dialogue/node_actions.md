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
Node actions are a way to access functions and properties inside of `Nodes` that can be anywhere in the Godot `SceneTree`.

## Adding node actions
There are two ways the `@` action works:

*Without* a period: `@action true 2.0`  
For every node in the *SceneTree* that is part of group `sa:action`, it's `func action():` will be called with `[true, 2.0]`.

*With* a period: `@group.function true 2.0`  
For every node in the *SceneTree* that is part of group `group`, it's `func function():` will be called with `[true 2.0]`.

When doing dialogue, you can include actions in `()` brackets:

```
john (jump): What was that!

// is like doing:

@john.jump
john: What was that!
```

Nodes can be part of as many groups as you like:

```gd
extends Node

func _init():
    add_to_group("sa:action")
    add_to_group("sa:reset")
    add_to_group("fade_in")
    add_to_group("fade_out")

func action(id := "default"):
    pass

func reset():
    pass

func fade_in(time := 1, color := "BLACK"):
    pass

func fade_out(time := 1, color := "BLACK"):
    pass
```

You could have group *john* and group *mary* and both are part of group *john_and_mary*:

```
@john.jump
john: What was that?

@mary.jump
mary: I heard it too!

@john_and_mary.jump
john mary: Woah!
```
