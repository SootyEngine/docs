---
title: Mods
parent: States
nav_order: 1
---

# Mods
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Directories
Everything is treated as a mod.

`res://` is loaded as if it were a mod.

|Folder|File type(s)|Desc|
|:-----|-----------:|:---|
|`dialogue/`| `.soot`|[Dialogue files](../dialogue/dialogue_files.md)|
|`lang/`|`.sola`|[Translation files](../translations/lang_files.md)|
|`states/`| `.gd` `.soda`|Node scripts or [data files](./data_files.md)|
|`persistent/`| `.gd` `.soda`|Node scripts or [data files](./data_files.md)|
|`scenes/`| `.tscn` `.scn`|[Scenes](../resources/scenes.md)|
|`audio/music/`| `.wav` `.mp3`, `.ogg`|[Music](../resources/music.md)|
|`audio/sfx/`| `.wav` `.mp3`, `.ogg`|[Sound](../resources/sfx.md) effects|

## User mods
*TO WRITE UP*

User mods will be looked for at `user://mods/user_mod_name/`.  

## Addon mods
*TO WRITE UP*

Godot addons can be mods.

Notice the [Visual Novel](https://github.com/teebarjunk/sooty-visual_novel-example) system treats itself as a "mod".
