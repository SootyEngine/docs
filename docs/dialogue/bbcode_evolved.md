---
title: BBCode Evolved
parent: Dialogue
---

# BBCode Evolved

## Common Tags
Any number of tags can be chained together with `;` in the same brackets: `[b;tomato]Bold Red Text[]`

Calling `[]` closes the last tag chain. `[/]` closes all open tags chains.

Some tags are self closing.

|Tag|Description|Options|
|---|----|-------|
|*color_name*|Use any built in Godot color name: `[deep_sky_blue]Blue Text[]` ||
|(n,n,n,n)|RGBA color. For use with format: `"[%s]text[]" % Color.TEAL`||
|*float*|Multiply current font size: `Speak [i;0.8]very quietly[].`||
|*int*|Add to current font size: `Speak [i;4]very loudly[].`||
|`dim`|Dims color by 33%.||
|`lit`|Lightens color by 33%.||
|`hue` `sat` `val`|Modify hue/sat/val of color.||
|`:emoji_name:` `:)`|Tags wrapped in `::` will use the emoji.<br>Some old fashioned emojis are supported. `[:)]`,||
|`\|pipe`|Will pipe text through a function.||
|`@group call` `$state call` `~expression`|Inserts returned value at this position.<br>Will auto close any style it's wrapped with:<br>`The [$stranger;b;red] looks at you.`<br>Can be piped to a function. `[$player.coins\|commas]`||
|`lb` `rb`|Insert brackets *[]*||
||||
|`cuss`|||
|`heart`|||
|`jit` `jit2`|||
|`jump` `jump2`|||
|`l33t`|||
|`off`|||
|`rain`|||
|`sin`|||
|`sparkle`|||
|`uwu`|||
|`wave`|||
|`woo`|||

Along with typical: `b` `i` `bi` `u`

## Animation control tags

|Tag|Description|Options|
|---|----|-------|
|`wait`|Pause the animation.|`[w]` `[wait]` `[w=2]`|
|`hold`|Hold animation till user action.|`[h]` `[hold]`|
|`jump`|Jump animation forward. So entire word or phrase can pop in.<br>`I already told you [jump]NO[][w] [jump]MORE[][w] [jump]LEAVING MY THINGS OUT![][w]`
|`pace`|Change pace of animation.|`[p]` `[pace]` `[p=2]`|
|`!@group call` `!$state call` `!~expression`|Call any [action](#actions) at that point in the animation.||

## Animation styles

Instead of simply fading in text, maybe you want to bounce it in, or show it as a computer console being typed out.

|Tag|Description|Options|
|`back`|||
|`console`|||
|`fader`|||
|`focus`|||
|`prickle`|||
|`redact`|||
|`wfc`|||

##Custom text effects

Try combining emojis and animations: `Press the [2.0;sin;:arrow_up:;] key!`<br>
This will double the scale, play the sin wave animation, show the up arrow emoji, and then close.

## Pipes
Values can be piped through functions that you've defined in any `res://states` class: `You have [$apples|commas] apples.` -> `You have 1,234,567 apples.`

So can text: `I have [|commas]1234567[] apples.` -> `I have 1,234,567,apples.`

You can spread functions across multiple scripts/nodes, but if there are multiple with the same name, only the first will be used.

## Defining Shortcuts
In `config.cfg` you can set shortcuts for complex actions and custom colors:

```cfg
[rich_text_shortcuts]
cam1="!@camera shake 2.0;!@camera zoom 2.0;wait=0.5"
cam_reset="!@camera shake 0.0;!@camera zoom 1.0
highlight="cherry;b;u"
pscore="$player.score|commas;b;greeny

[rich_text_colors]
cherry="#FF9053"
greeny="#BBEE32"
```

Now use them like any other BBCode.

```
My score\: [pscore] points.
john: These [cherry]cherries[] sure look good. [cam1]Wait, these aren't cherries.[cam_reset] They're blueberries.
```
