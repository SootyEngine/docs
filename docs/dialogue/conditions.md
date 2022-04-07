---
title: Conditions
parent: Dialogue
nav_order: 2
---

# Conditions

|Condition|Description|Example|
|---------|-----------|-------|
|`{{if}}` or just `{{}}`|The classic *if* statement. You don't need to type *if* though.|`{{if apples > oranges}}` `{{apples > oranges}}`|
|`{{elif}}`|If the previous condition failed, this one will be checked.|`{{elif apples > pears}}`|
|`{{else}}`|If all other conditions failed, this will occur.`{{else}}`|
|`{{match}}`|A condensed pattern.||

## Match

Check out the Godot [tutorial](https://docs.godotengine.org/en/latest/tutorials/scripting/gdscript/gdscript_basics.html#match).

Sometimes they can be a lot nicer/neater that if-else statements.

```
{{*time.weekday}}
    {{MONDAY}} @sfx sad_audio
    {{TUESDAY}} john: Glad [b]mondays[] over.
    {{WEDNESDAY}} It's the middle of the week.
    {{THURSDAY}}
        john: The whole vibe shifts on thursday!
    {{FRIDAY}} @sfx happy_audio
        john: Aw yeah, friday!
    {{_}} It's the weekend.
```
