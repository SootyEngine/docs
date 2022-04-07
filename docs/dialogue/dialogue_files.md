---
title: Dialogue files
parent: Dialogue
nav_order: -1
---

# Dialogue files `.soot`
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Basic dialogue

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
john mary jane paul: We all agree!
```

You can wrap a name in `"` to have it as is:
```
"Mysterious Stranger": Howdy.
: You don't remember me do you?
: (chuckles)

He removes the mask.

paul: It's me, Paul!
```

To use a `:` without a speaker, escape it like `\:`
```
My score\: [~score].
```

## Name evaluation

The speaker tag(s) will be used to:
- Look in `State`:
- If it finds an object with `get_string` it calls `get_string("caption_name")`.
- If it finds an object without `get_string` it looks for a `name` field.
- If it finds a string, it uses that.
- Otherwise it just output itself.

## Markdown

```
Some *italic*, **bold** and ***bold italic*** text.
```

## BBCode Evolved®

Sooty's BBCode works different, in that multiple tags can go inside a set of brackets. There are also a lot of new tags.

[Learn more](/sooty-docs/docs/dialogue/bbcode_evolved.md)
```
Some [b;tomato]bold red text[] and some [i;deep_sky_blue]italic blue text.[]
```

## Inserting state values

BBCode tags starting with `~` will display an evaluation.

```
Two plus two equals [~2+2].
Double my score is [~score * 2].

Stylize score as bold and red [~score;b;red].
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

The caption animation can be paused, sped up, or held till user input. See [BBCode Evolved®](/sooty-docs/docs/dialogue/bbcode_evolved.md) for more info.

```
We can pause[wait] the text.
We can hold until the user presses something.[hold] And then show some more text.
We can [pace=2]speed up the speed of the speaker.[pace=0.25] Or slow it down.
```

## Calling functions during text animation
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
paul: """" {% raw %}{{score > 20}}{% endraw %}
I don't care what [b]they[] say, it's not happening.

    (He turned to look at the shore.)

Not now, not ever.
""""
```

If [translating](/sooty-docs/docs/lang/lang_files.md), add the `#id=` on the first line.
```
paul: """"  #id=long_intro
Once upon a time, a long time ago
  there lived a king
    in a castle...
""""
```


## Meta keys

Files can have meta data for some internal uses.

|Key|Desc|Example|
|---|----|-------|
|`#.IGNORE`|Don't load this dialogue. Useful for debugging.|`#.IGNORE`|
|`#.id`|Manually set an id, instead of using file name.|`#.id: new_name`|

## Symbol cheat sheet

|Pattern|About|Example|
|-----|-----|-------|
|`# comment`|These are just for you, and are ignored by the system.|`# TODO: Rewrite these lines.`|
|`=== flow id`|The start of a flow; a series of steps to run through.|`=== chapter_1`|
|`text`|Text to show the user.|`Once upon a time...`|
|`name: text`|Text with a speaker.|`robot: Are you sure about this?`|
|`- option text`|An option for a menu.|`- Yes, take me there.`|
|`=> flow_id`|Goto a flow.|`=> chapter_2`|
|`=> soot_id/flow_id`|Goto a flow in a different file.|`=> day_2/morning`|
|`== flow_id`|Call a flow, then return back to this line.|`== describe_scene`|
|`== soot_id/flow_id`|Call a flow in a different file, then return back to this line.|`== funcs/reset_stats`|
|`><`|End the current flow. If called from a `==`, this returns, otherwise ends the dialogue.|`><`|
|`>><<`|End the dialogue. Optionally you can pass a message that will be signaled.|`>><< end_msg`|
|`__`|Does nothing. Represents an empty step in the flow.|`__`|
|`@node.function`|Call's a node group function.|`@damage player 20 fire:true`|
|`$state.function`|Call's a state function.|`$player.damage 20 fire:true`|
|`~state evaluation`|Evaluates an expression on state data.|`~score += 20 * score_multiplier(player.stats)`
|`{% raw %}{{condition}}{% endraw %}`|For only displaying lines that pass.|`mary: Oh wow, you brought it. {% raw  %}{{talked_to_mary and player.item_count("spoon") > 1}}{% endraw  %}`|
