---
title: String actions
has_children: true
nav_order: 500
---

*TO WRITE*

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
