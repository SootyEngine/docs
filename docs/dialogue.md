---
title: Dialogue
has_children: true
nav_order: 10
---

# Dialogue
{: .no_toc }

![](highlighter.png)

## Table of contents

{: .no_toc .text-delta }

1. TOC
{:toc}

## Symbol overview

<!-- {% raw %} -->
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
<!-- {% endraw %} -->
