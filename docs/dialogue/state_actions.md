---
title: State Actions
parent: Dialogue
nav_order: 30
---

## Adding state actions
Create a script in `res://states/` extending a `Node`, and define your functions and variables.

```gd
#my_state.gd

signal my_signal(id: String, amount: int)

var _tick := 0 # var names begining with _ will not be saved.
var score := 0 # all other vars defined in script will be.

func ticker(amount := 1) -> int:
  _tick += amount
  return _tick

func double_score():
  score *= 2

# here we can return a bbcode wrapped version.
func score_styled(color = Color.GREEN) -> String:
  return "[%s;b]%s[]" % [color, score]

func do_signal(id: String, amount: int):
  my_signal.emit(id, amount)
```

Now in a `.soot` script, these can be called in one of two ways.

```
#the_story.sooty

=== scene_start
  # The shortcut way:
  My score is [$score], or stylized is [$score_styled] and with an argument [$score_styled RED].
  
  # Or the evaluation way:
  My score is [~score], or stylized is [~score_styled()] and with an argument [~score_styled("RED")].
```
