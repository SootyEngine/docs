---
title: Solutions
has_children: true
nav_order: 1000
---

# Godot crashing on startup
Disable the plugin:
- Open project folder.
- Edit `project.godot`
- Erase lines in `[autoload]` section.
- In `[editor_plugins]` section, empty `enabled`:<br>
    Before
    ```
    enabled=PackedStringArray("res://addons/sooty_engine/plugin.cfg")
    ```
    After
    ```
    enabled=PackedStringArray()
    ```
Now try boot again and re-enable plugin.

# `x` not found
After enabling the plugin, restart Godot.
