---
title: Save system
parent: States
nav_order: 2
---

# Save system
{: .no_toc .text-delta }

Sooty aims to handle the entire save system with nothing on your part. But here is how it works.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## What is saved?
Any kind of property can be saved, including built in Godot types like Vector2 and Color, and even complex Objects and Resources.  
For each Object/Resource, a dictionary of properties (only those that have changed) will be saved.  

*TO WRITE*

## Save screen UI (Visual novel)
If you add a property `var save_caption := "Save Name"` it will be shown on the save screen. This could be used to indicate to the player what location, mission, or progress, the slot's data contains. It could contain BBCode.

![](/save_screen.png)
