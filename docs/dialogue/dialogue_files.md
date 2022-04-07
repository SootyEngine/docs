---
title: Dialogue files
parent: Dialogue
nav_order: -1
---

# Dialogue Files `.soot`
{: .no_toc .text-delta }

## Table of contents
{: .no_toc .text-delta }

- TOC
  {:toc}


## Basic dialogue
<!-- {% raw %} -->


```
Text without a speaker.

# Speakers.
john: Text spoken by John.
: Text spoken by last speaker, John.

```

## Speakers
Text with a `:` before it will have a speaker tag
```
mary: What year is it?`
```

When no name is given, it will use the last one:
```
jane: As I was saying;
: These things happen for a reason.
```

Multiple speakers can be included with a space:
```
john mary jane paul: We all agree!`
```

You can wrap a name in `"` to have it as is:
```
"Mysterious Stranger": Howdy.
: You don't remember me do you?
: (chuckles)

He removes the mask.

paul: It's me, Paul!
```

If you want a `:` in a speakers name, escape it with a `\:`.

## Name evaluation

The name tag will be used to:
- Look in `State` for name.
- If it finds an object with `get_string` it calls `get_string("caption_name")`.
- If it finds an object without `get_string` it looks for a `name` field.
- If it finds a string, it uses that.
- Otherwise it just output itself.

## Markdown

```
Some *italic*, **bold** and ***bold italic*** text.
```

## BBCode Evolved®

[Learn more](#docs/dialogue/bbcode_evolved.md)
```
Some [b;tomato]bold red text[] and some [i;deep_sky_blue]italic blue text.[]
```

## Inserting state values

BBCode tags starting with `~`.

```
Two plus two equals [~2+2].
Double my score is [~score * 2].

Stylize score [~score;b;red] as bold and red.
```

The values can also be piped into a state function with `|`.
```
jane: I have over [~jane.money|commas] dollars!
```

In GDScript this would look something like:
```
return State.commas(State.jane.money)
```

## Animation control

The caption animation can be paused, sped up, or held till user input. See [BBCode Evolved®](#docs/dialogue/bbcode_evolved.md) for more info.

```
We can pause[wait] the text.
We can hold until the user presses something.[hold] And then show some more text.
We can [pace=2]speed up the speed of the speaker.[pace=0.25] Or slow it down.
```

State functions `$` `~` and node functions `@` can be called at points in the animation by prefacing with a `!`.

```
Actions can be called at a point [!@camera zoom 2.0]. Got it?
Like any other tag [!@camera zoom;!@camera shake;!~score += 20] you can combine multiple in one.
```

## Multiline dialogue
For blocks of text where you want whitespace preserved there is `""""`:
```
""""
You can place *lots* of formatted text in one block.
        *Tabs*
            will
                be
                    preserved.

As will **whitespace**.
""""
```

If it has a speaker, they come first, and a condition can be placed behind.
```
paul: """" {{score > 20}}
I don't care what [b]they[] say, it's not happening.

    (He turned to look at the shore.)

Not now, not ever.
""""
```

If [translating](#docs/lang/lang_files.md), add the `#id=` on the first line.
```
paul: """"  #id=long_intro
Once upon a time, a long time ago
  there lived a king
    in a castle...
""""
```

<!-- {% endraw %} -->

## Meta keys

Files can have meta data for some internal uses.

|Key|Desc|Example|
|---|----|-------|
|`#.IGNORE`|Don't load this dialogue. Useful for debugging.|`#.IGNORE`|
|`#.id`|Manually set an id, instead of using file name.|`#.id: new_name`|
