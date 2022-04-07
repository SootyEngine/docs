---
title: Mods
parent: States
nav_order: 1
---

# Mods
Everything is treated as a mod. `res://` is loaded as if it were a mod.  
The system was designed with modding/expansions/patches/translations in mind.  

## Directories

|Folder|File type(s)|Desc|
|:-----|-----------:|:---|
|`dialogue/`| `.soot`|Dialogue files.|
|`lang/`|`.sola`|Translation files.|
|`states/`| `.gd` `.soda`|Node scripts or data files.|
|`persistent/`| `.gd` `.soda`|Node scripts or data files.|
|`scenes/`| `.tscn` `.scn`|Main scenes, with unique names.|
|`audio/music/`| `.wav` `.mp3`, `.ogg`|Music.|
|`audio/sfx/`| `.wav` `.mp3`, `.ogg`|Sound effects.|

User mods can have their own folder in `user://mods`.  
Notice the [Visual Novel](https://github.com/teebarjunk/sooty-visual_novel-example) system treats itself as a "mod".
