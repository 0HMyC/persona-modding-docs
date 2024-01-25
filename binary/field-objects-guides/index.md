---
title: 2D Field Objects
layout: page
parent: Binary Files
nav_order: 1
has_children: true
games: ['P3P']
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

{: .todo }
> Write more better words dumbass!!!

This page contains info on Field Objects.

## What are Field Objects?

Field Objects are the interactable points that are on the fields in P3P. They come in two forms: "Hit" Objects, and "NPC" Objects.

Hit Objects are used to define parts of a field that are constant to that field, meaning it will always be presented as interactable in the game. NPC Objects, on the other hand, can be set to only appear on certain in-game calendar dates, and even be hidden if a bitflag is set. As such, they are meant to be a dynamic aspect of a field.

## Where are Field Objects stored?

Field Objects can be located in the given abin file for a 2D Field, and are stored under multiple different files.

{: .todo }
> Should I link to SecreC's PE fork or not here? it's better but not the official source..... snake voice hrgngg

{: .info }
> Field abin files can be located in umd0.cpk\field2d\bg, and the contents extracted using [Amicitia](https://github.com/tge-was-taken/Amicitia) or [PersonaEditor.](https://github.com/Secre-C/PersonaEditor)

| File | Purpose |
|----|----|
| h00_00.dat | Defines the ID and position of Hit Objects. |
| h00_00_name.dat | Defines the text that will appear when hovering over a Hit Object. |
| h00_00_pck.dat | Defines the Hit Object ID to load, [Flowscript Procedure](../../persona-modding-docs/flowscript/) to call, and Icon to display for the Hit Object. |
| n00_00.dat | Defines the ID and position of NPC Objects. |
| n00_00_pck.dat | Defines the NPC Object ID to load position from, which sprite to use, [Flowscript Procedure](../../persona-modding-docs/flowscript/) to call, and a bitflag that if enabled will hide the NPC Object. |
| n00_00_tbl.dat | Defines the "groups" of NPC Objects to load from n00_00_pck.dat, on which in-game date and time. |

## Required Tools

The guides to add custom Hit and NPC Objects below have been written expecting that you will be using the following software:

{: .todo }
> Rewrite the guides to use 010 like the Binary Files page says!!!!!! Don't lock ppl to windows when possible man!!!

| Tool | Usage |
|----|----|
| [Amicitia](https://github.com/tge-was-taken/Amicitia) | Used to extract the files necessary for editing the field Object data. |
| [HxD](https://mh-nexus.de/en/hxd/) | Used to manually make modificiations to the field Object files. |