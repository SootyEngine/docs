---
title: Options
parent: Dialogue
nav_order: 3
---

# Options
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Writing
To add options to dialogue, tab lines below, starting with a `-`.

```
Are you sure about that?
    - Yes.
    - No.
    - Maybe.
```

You can write dialogue underneath these lines, so long as it's tabbed.

```
journey_man: Where to, traveler?
    - East.
        We go eastward.
        @sfx wind_002
        => east
    - West.
        We go westward.
        @sfx dust_storm
        => west
    - North.
        journey_man: The cost north is extra. Will you pay?
            - Yes, here you go. {% raw %}{{money >= 5}}{% endraw %}
                $money -= 5
            - I don't have money, but I need to get there. {% raw %}{{money < 5}}{% endraw %}
                journey_man: Meh, all right, let's go.
                => north
            - Hmm, nevermind.
                journey_man: Suit yourself.

```

## Conditions
Options can have [`{% raw %}{{Conditions}}{% endraw %}`](/docs/dialogue/conditions.md).

```
guard: Sorry, can't let you in without the password.
    - Doop a doop. {% raw %}{{has_password}}{% endraw %}
        guard: Hmm.
        @sfx door_clanking_open
        => enter_the_club
    - Uhm... err... quack-quack?
        guard: Get the hell out of here.
        => back_to_street
    - Oh, well, I don't know it.
        => back_to_street
```

## Single line shortcuts

You can place a `=>` on the same line, for convenience.  
If there are tabbed lines, the `=>` will be called last.

```
Where to?
    - East => east
    - West => west
    - North => north
        All right, north we go.
```

While not advisable, as it's hard to read, you can use `(())` and `;;` to write tabbed lines on the same line.

```
Where to?
    - East. ((man: All right, east we go. ;; @sfx east ;; $dir = "east" )) => east
    - North. ((man: Okay, north it is. ;; @sfx north ;; $dir = "north")) => north
```
