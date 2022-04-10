---
title: String actions
nav_order: 500
---

# String actions
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## About
The `StringActions` autoload allow doing all kinds of things with simple commands.

They have automatic type conversion and `kwargs`.

### Type Conversion
The type conversion works off looking at the way you wrote you're function, so please be explicit.
```
# not ideal. StringActions will have to assume.
func my_func(x, y):
    pass

# better. default arguments can be used to assume.
func my_func(x := "", y := false):
  pass

# ideal. no guessing on what type is needed.
func my_func(x: String = "", y: bool = false):
    pass
```

### kwargs
Inspired by Python because I really like `kwargs` (Key word arguments).

They allow you to skip over default arguments and are more obvious/explicit about what is happening:
```
# here is our function
func doit(a: String, b := false, c := true, kwargs := {}):
    pass

# we will add it as a command
StringActions.add_command(doit)

# from Godot
StringActions.do_command("doit x tint:blue")
StringActions.do_command_w_args("doit", ["x", {"tint": "blue"}])

# from Dialogue
>doit x tint:blue
```

All those calls will evaluate to
```
doit("x", false, true, {"tint": "blue"})
```

## `>` Commands

### Calling from Godot
```gd
StringActions.do("> my_command true 0.0 tint:blue")
StringActions.do_command("my_command true 0.0 tint:blue")
StringActions.do_command_w_args("my_command", [true, 0.0, {tint="blue"}])
```

### Calling from dialogue
```
> my_command true 0.0 tint:blue
```

### Adding commands
```gd
StringActions.add_command(my_object.my_command)
```

## `@` Node actions
See [here](./dialogue/node_actions.md).

### Calling from Godot
```gd
StringActions.do("@enemies reset 1,2,3")
StringActions.do_node_action("@enemies reset 1,2,3")
StringActions.do_node_action_w_args("@enemies", ["reset", [1, 2, 3]])
```

## `$` State actions
See [here](./dialogue/state_actions.md).

```gd
StringActions.do("$enemies reset 1,2,3")
StringActions.do_state_action("$enemies reset 1,2,3")
StringActions.do_state_action_w_args("$enemies", ["reset", [1, 2, 3]])
```

## `~` State expressions

Access properties and functions in the State scripts.

### Calling from Godot
```gd
StringActions.do("~ score += 20")
StringActions.do_expression("score += 20")
```

### Calling from dialogue
```
~ score += 20
~ score += pow(my_state_function(false), 2) * another_function()
~ reset_my_stats()
~ trigger(["orcs", "elves"], "trigger_x", 321)
```
