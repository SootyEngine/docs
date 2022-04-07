---
title: Conditions
parent: Dialogue
nav_order: 2
---

# Conditions
{: .no_toc }

![](/docs/dialogue/conditions.png)

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Overview

|Head|Description|Example|
|----|-----------|-------|
|`if` or empty|The classic *if* statement. You don't need to type *if* though.|{% raw %}`{{if apples > oranges}}`{% endraw %} {% raw %}`{{apples > oranges}}`{% endraw %}|
|`elif`|If the previous condition failed, this one will be checked.|{% raw %}`{{elif apples > pears}}`{% endraw %}|
|`else`|If all other conditions failed, this will occur.{% raw %}`{{else}}`{% endraw %}|
|`match`|A condensed pattern.|{% raw %}`{{match apples}}`{% endraw %}|

## Match

Check out the Godot [explanation](https://docs.godotengine.org/en/latest/tutorials/scripting/gdscript/gdscript_basics.html#match).

Sometimes they can be a lot nicer/neater that if-else statements.

```
<!-- {% raw %} -->
{{match time.weekday}}
    {{MONDAY}} @sfx sad_audio
    {{TUESDAY}} john: Glad [b]mondays[] over.
    {{WEDNESDAY}} It's the middle of the week.
    {{THURSDAY}}
        john: The whole vibe shifts on thursday!
    {{FRIDAY}} @sfx happy_audio
        john: Aw yeah, friday!
    {{_}} It's the weekend.
    <!-- {% endraw %} -->
```

Soon this will support array and dict patterns.
