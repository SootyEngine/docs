---
title: Data files
parent: States
---

# `.soda` files
Inspired by YAML, but designed for Godot, Sooty Data Files, or `.soda`, are a way to more easily define data.

Store the files in `states/` or `persistent/` to have them auto install.  

They can be accessed:
- In Godot, with `State`: `State.characters.paul.name`.
- In `.soot` script with `$`: `$characters.paul.name`

## Auto type conversion
Data is auto converted to whatever type is at the path destination.  
If the property has no explicit type, it will be assumed.
```
#your_script.gd
class_name Guy
var name := ""
var coin := 0
var tint := Color.WHITE


#your_data.soda
guy1=Guy:
	name: Mr. Man		# converts to String: "Mr. Man"
	coin: 80		# converts to int: 80
	tint: #ff0000		# converts to Color("#ff0000")
guy2=Guy:
	name: 1			# converts to String: "1"
	coin: 9_000_000  	# converts to int: 9000000
	tint: TOMATO		# converts to Color.TOMATO
```

## Shortcuts
To make nested properties shorter, there are shortcuts.  
They begin with `~~` followed by an address.
```
#data.soda
~~p: characters.player
~~coins: characters.player.inventory.coins

characters:
	player:
		name: Mary
		inventory:
			coins: 13

#dialogue.soot
p: My name is [~p.name] and I have [~coins] coins.
~coins += 20
p: Now I have [~coins].
```

## Flagged alternatives
To ease with testing, if a flag is inside `Global.flags` an alternative key can be used:
```
my_data:
	name: Coolman
	coin: 0

	# If "dbg" in Global.flags, these properties will be used.
	name?dbg: Coolman Debug
	coin?dbg: 1_000

	# If "dbg" and "cheat" in Global.flags, coin will be 1,000,000.
	coin?dbg?cheat: 1_000_000
```
