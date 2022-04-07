---
title: Dialogue
has_children: true
---

# Basic dialogue

```
Text without a speaker.

// Speakers.
john: Text spoken by John.
: Text spoken by last speaker, John.

// Markdown formatting.
Some *italic*, **bold** and ***bold italic*** text.

// BBCode.
Some [b;tomato]bold red text[] and some [i;deep_sky_blue]italic blue text.[]

// Inserting state values to text.
The current score is [$score;b;cyan].

// Effecting the animation.
We can pause[wait] the text.
We can hold until the user presses something.[hold] And then show some more text.
We can [pace=2]speed up the speed of the speaker.[pace=0.25] Or slow it down.

// Calling actions at points in the animation.
Actions can be called at a point [!@camera zoom 2.0]. Got it?
Like any other tag [!@camera zoom;!@camera shake;!~score += 20] you can combine multiple in one.

// Multiline text.
""""
You can place *lots* of formatted text in one block.
        *Tabs*
            will
                be
                    preserved.

As will **whitespace**.
""""

// Multiline with a speaker and condition.
paul: """" {{score > 20}}
I don't care what [b]they[] say, it's not happening.

    (He turned to look at the shore.)

Not now, not ever.
""""
```

## Speakers
Text with a `:` before it will have a speaker tag: `mary: What year is it?`

Multiple speakers can be included with a space: `john mary jane paul: We all agree!`

Speaker names will be auto styled with state data:
```
# my_state.gd

var john := Character.new({name="John", color=Color.DEEP_SKY_BLUE})
```

But you can wrap a name in `"` to have it as is: `"[b;gray]Mysterious Stranger[]": Howdy.`

If you want a `:` in a users name, escape it with a `\:`.

## Feature overview

To get syntax highligting in Godot, open the file in editor and select `Edit > Syntax Highlighter > Soot`

![](highlighter.png)

|Pattern|About|Example|
|-----|-----|-------|
|`# comment`|These are just for you, and are ignored by the system.|`// TODO: Rewrite these lines.`|
|`=== flow id`|The start of a flow; a series of steps to run through.|`=== chapter_1`|
|`text`|Text to show the user.|`Once upon a time...`|
|`name: text`|Text with a speaker.|`robot: Are you sure about this?`|
|`- option text`|An option for a menu.|`- Yes, take me there.`|
|`=> flow_id`|Goto a flow.|`=> chapter_2`|
|`=> soot_id.flow_id`|Goto a flow in a different file.|`=> day_2.morning`|
|`== flow_id`|Call a flow, then return back to this line.|`== describe_scene`|
|`== soot_id.flow_id`|Call a flow in a different file, then return back to this line.|`== funcs.reset_stats`|
|`><`|End the current flow. If called from a `==`, this returns, otherwise ends the dialogue.|`><`|
|`>><<`|End the dialogue. Optionally you can pass a message that will be signaled.|`>><< end_msg`|
|`__`|Does nothing. Represents an empty step in the flow.|`__`|
|`@node.function`|Call's a node group function.|`@damage player 20 fire:true`|
|`$state.function`|Call's a state function.|`$player.damage 20 fire:true`|
|`~state evaluation`|Evaluates an expression on state data.|`~score += 20 * score_multiplier(player.stats)`
|`{{condition}}`|For only displaying lines that pass.|`mary: Oh wow, you brought it. {{talked_to_mary and player.item_count("spoon") > 1}}`|
