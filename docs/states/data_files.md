---
title: Data files
parent: States
nav_order: 0
---

# Data files `*.soda`
{: .no_toc }

Inspired by YAML, but designed for Godot, Sooty Data Files, or `.soda`, are a way to more easily define data.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Auto type conversion
Data is auto converted to whatever type is at the path destination.  
If the property has no explicit type, it will be assumed.

```gd
#your_script.gd

class_name Guy
var name := ""
var coin := 0
var tint := Color.WHITE
```

```yaml
#your_data.soda

guy1=Guy:
	name: Mr. Man		# String: "Mr. Man"
	coin: 80		# int: 80
	tint: #ff0000		# Color("#ff0000")

guy2=Guy:
	name: 1			# String: "1"
	coin: 9_000_000  	# int: 9000000
	tint: TOMATO		# Color.TOMATO
```

## Shortcuts
To make accessing nested properties easier, there are shortcuts.  
They begin with `~~` followed by an address.

```yaml
#my_data.soda

~~p: characters.player
~~coins: characters.player.inventory.coins

characters:
	player:
		name: Mary
		inventory:
			coins: 13
```
Now dialogue can look neater.
```
#my_dialogue.sooty

p: My name is [~p.name] and I have [~coins] coins.

~coins += 20

p: Now I have [~coins].
```

## Flagged alternatives
To ease with testing, if a flag is inside `Global.flags` an alternative key can be used:
```yaml
my_data:
	name: Coolman
	coin: 0

	# If "dbg" in Global.flags, these properties will be used.
	name?dbg: Coolman Debug
	coin?dbg: 1_000

	# If "dbg" and "cheat" in Global.flags, coin will be 1,000,000.
	coin?dbg?cheat: 1_000_000
```

## Install address
If you want to add a lot of items to a nested object, you can use the meta key `#.to: address.of.data`

```yaml
#.to: characters.player.items

sword: 1
shield: 1
coin: 20_300
```
Is the same as doing:
```yaml
characters:
	player:
		item:
			sword: 1
			shield: 1
			coin: 20_300
```
