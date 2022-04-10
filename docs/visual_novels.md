---
title: Visual novels
has_children: true
nav_order: 100
---

# Visual novels

## Projects

- [Visual novel template](https://github.com/teebarjunk/sooty-visual_novel)
- [Visual novel example](https://github.com/teebarjunk/sooty-visual_novel-example)

## Built in MAIN flows

If there is a `res://dialogue/MAIN.soot`, these flows will be called automatically when certain things happen.

|Flow id|Called when:|Potential uses:|
|:-----:|-------|------------|
|`started`|New game first starts.|Goto whatever scene you want to start with.
|`dialogue_ended`|The dialogue ended.|End game or start a new dialogue.

## Built in scene flows

If there is a `.soot` with the same `id` as the current scene, these will be called automatically when certain things happen.

|::|Flow id|Called when:|Potential uses:|
|:-----:|:--:|------------|---------|
|:o:|`SCENE_INIT`|Scene entered.|Showing/hiding objects based on State.|
|:o:|`CHANGED-*`|State property changed.|Changing scene nodes based on State.|
|:o:|`FLOW_STARTED-*`||
|:o:|`FLOW_ENDED-*`||
||`scene_started`|Scene entered, and no other flow is running.||

:o: = No text in this flow will be displayed. It's meant for calling functions based on State conditions.

## Node actions
See [here](./dialogue/node_actions.md)

|Action|Desc|Examples|
|------|----|--------|
|`@VN` |The `VisualNovel` autoload.|`@VN.version`|
