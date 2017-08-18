---
layout: post
title: "Git Commit Squash"
date: 2017-09-01
description: Demasiados commits en la rama... squash them!!
tags: 
- git
- squash
- tips
categories: 
- tips
twitter_text: "¿Sabes hacer GIT commits Squash?"
author: fer
---

A menudo trabajando se nos van de las manos los commits: pequeños cambios que se nos olvidan, fixes que no podemos probar en local... al final nos queda una rama (y la pull request) con **una veintena de commits con cambios muy pequeños**. Para limpiar este caos, podemos unificar los commits haciendo **squash**:

```shell
git rebase -i master

```
Esto nos abrirá el editor en consola (el que tengamos configurado, normalmente *nano* o *vim*) mostrando algo parecido a esto:

```
pick 2231360 some old commit
pick ee2adc2 Adds new feature



# Rebase 2cf755d..ee2adc2 onto 2cf755d (9 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```

Los commits que queramos "fusionar con el anterior" los marcamos con `s` o  `squash`. En el ejemplo, el commit *ee2adc2* se fusionará con *2231360*:

```
pick 2231360 some old commit
s ee2adc2 Adds new feature



# Rebase 2cf755d..ee2adc2 onto 2cf755d (9 commands)
#
# [....]
```


En caso de conflictos durante la operación de rebase, podemos usar `git mergetool` para resolverlos:

```shell
# (use 's' to mark the commits to squash)

# In case of conflicts:
git mergetool
git rebase --continue
```

Finalmente, hacemos `push` a la rama con la opción `-f` para sobrescribir los commits:

```shell
# Then finally push (forcing) to remote branch
git push -f origin feature/my-branch-name
```


Espero que os sirva, es bueno acostumbrarse a hacer este tipo de pequeñas acciones que nos dejarán más limpio el historial de commits ;).

**Enjoy!**
