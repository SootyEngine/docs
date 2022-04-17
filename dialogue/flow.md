---
title: Flow control
parent: Dialogue
nav_order: 1
---

# Flow control
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Writing

A flow is a set of actions to call one after another, like, displaying a caption, playing a sound, changing the scene...

To go to another flow in the file, use `=> other_flow`.

To call another flow, and then return to where we are, use `== other_flow`.  
This is useful for having common lines:

They work like the Godot `NodePath` or a file system.
- `.sibling`
- `..parent`
- `child`
- `/root_level`
- `/root_level/child`
- `..parent/child`
```
=== top_level
    === child_flow
        Once upon a time.
        => .next_child

    === next_child
        There lived a bird.
        => /other_top_level/child

=== other_top_level
    === child
        The bird was cool.
        => my_child

        === my_child
            The end.
```

```
=== monday
    == .start_of_day

    Time to get to class.

    # do a bunch of stuff here

    == .end_of_day

=== tuesday
    == .start_of_day

    Today is the big day.

    # do a bunch of stuff here

    == .end_of_day

=== start_of_day
    ~money_at_start = money

    Today is [time.day_of_week].

=== end_of_day
    ~money_earned = money - money_at_start
    {% raw %}{{money_earned > 0}}{% endraw %}
        I earned [~money_earned] today.
    {% raw %}{{elif money_earned < 0}}{% endraw %}
        I lost [~-money_earned] today.
    {% raw %}{{else}}{% endraw %}
        I didn't make any money today.
```

## Types

### `=>` goto
Runs a flow at the given path.

```
# goto a local flow
=> flow_id

# goto a flow in another file
=> other_file/flow_id
```

### `==` call
Runs a flow at the given path, and then returns to this line.

```
# call a local flow
== flow_id

# call a flow in another file
== other_file/flow_id
```

### `__` pass
This does nothing. But has [uses](#docs/lang/line_ids.md).

### `><` break
Ends the current flow.

If called from a `==` this will just return to it's line.

If called from a `=>` this will end the dialogue.

### `>><<` return
End's the dialogue, regardless of how nested we are.
