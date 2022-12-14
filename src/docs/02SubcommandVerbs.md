---
layout: docs
title: "Subcommand verbs"
date: 2022-12-13
add toc: true
add sidebar: _sidebars/mainSidebar.md
Article Status: Publishable
---

## Subcommand verbs

while not all object subcommands support all verbs, here is a list of the verbs and what to expect when they are applicable for an `<object>`:

- arc `<object>` **init** : will initialize a new empty `<object>` in the ARC.
- arc `<object>` **create** will create a new `<object>` with the passed arguments in the ARC.
- arc `<object>` **update** will update the registration of an existing `<object>` with the passed arguments.
- arc `<object>` **edit** will open an existing `<object>` with a text editor, allowing editing the registration of the `<object>`. 
- arc `<object>` **register** will register an existing `<object>` in the ARC with the passed arguments.
- arc `<object>` **add** is the combination of create/init+update and register, meaning it will create a new `<object>` in the ARC and subsequently register it with the passed arguments
- arc `<object>` **delete** will delete the `<object>` from the arc file structure.
- arc `<object>` **unregister** will remove the `<object>` from the ARC's register.
- arc `<object>` **remove** is the combination of delete and unregister, meaning it will delete the `<object>` from the ARC file structure and the ARC's registry
- arc `<object>` **move** will move the `<object>` from source to target register.
- arc `<object>` **list** will print all `<object>s` registered in the ARC.
- arc `<object>` **set** will set a single value in the `<object>`.
- arc `<object>` **unset** will remove a single value from the `<object>`.
