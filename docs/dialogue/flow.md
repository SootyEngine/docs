---
title: Flow control
parent: Dialogue
nav_order: 1
---

# Flow control
{: .no_toc }

A flow is a set of actions to call one after another, like, displaying a caption, playing a sound, changing the scene...

## Table of contents
{: .no_toc .text-delta }

- TOC
   {:toc}

## Writing
To go to another flow in the file, use `=> other_flow`.

To call another flow, and then return to where we are, use `== other_flow`.  
This is useful for having common lines:

```
=== monday
    == start_of_day
    Time to get to class.
    // do a bunch of stuff here
    == end_of_day

=== tuesday
    == start_of_day
    Today is the big day.
    // do a bunch of stuff here
    == end_of_day

=== start_of_day
    ~money_at_start = money
    Today is {{time.day_of_week}}.

=== end_of_day
```~money_earned = money - money_at_start
    {{money_earned > 0}}
        I earned [~money_earned] today.
    {{elif money_earned < 0}}
        I lost [~-money_earned] today.
    {{else}}
        I didn't make any money today.
```

## `=>` Goto flow
Runs a flow at the given path.

If there is no `/`, it's treated as local to the file.

## `==` Call flow
Runs a flow at the given path, and then returns to this line.

## `><` End flow
Ends the current flow.

If called from a `==` this will just return to it's line.

If called from a `=>` this will end the dialogue.

## `>><<` End dialogue
End's the dialogue, regardless of how nested we are.

## `__` Pass
This does nothing. But has [uses](#docs/lang/line_ids.md).
