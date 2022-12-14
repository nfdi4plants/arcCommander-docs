---
layout: docs
title: "General cli structure"
date: 2022-12-13
add toc: true
add sidebar: _sidebars/mainSidebar.md
Article Status: Publishable
---


## General cli structure

The general command line structure is designed as either

```powershell
arc <top-level-command> <top-level-command-args>
```

e.g.

```powershell
arc init
```

or

```powershell
arc <object> <subcommand-verb> <subcommand-verb-args>
```

where `<object>` is one of the following:

 - `assay` 
 - `study`  or its sub-objects 
 - `investigation` or its sub-objects 
 - `configuration`

and `<subcommand-verb>` models what to do with the object, e.g

```powershell
arc study init
```

will initialize a new empty study in the ARC.
