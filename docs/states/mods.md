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
|`dialogue/`| `.soot`|[Dialogue files](/sooty-docs/docs/dialogue.md)|
|`lang/`|`.sola`|[Translation files](/sooty-docs/docs/translations/lang_files.md)|
|`states/`| `.gd` `.soda`|Node scripts or [data files](/sooty-docs/docs/states/data_files.md)|
|`persistent/`| `.gd` `.soda`|Node scripts or [data files](/sooty-docs/docs/states/data_files.md)|
|`scenes/`| `.tscn` `.scn`|[Scenes](/sooty-docs/docs/resources/scenes.md)|
|`audio/music/`| `.wav` `.mp3`, `.ogg`|[Music](/sooty-docs/docs/resources/music.md)|
|`audio/sfx/`| `.wav` `.mp3`, `.ogg`|[Sound](/sooty-docs/docs/resources/sfx.md) effects|

## User mods
*TO WRITE UP*

User mods will be looked for at `user://mods/user_mod_name/`.  

## Addon mods
*TO WRITE UP*

Godot addons can be mods.

Notice the [Visual Novel](https://github.com/teebarjunk/sooty-visual_novel-example) system treats itself as a "mod".
