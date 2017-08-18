---
layout: post
title: "Git Commit Squash"
date: 2017-09-01
description: Demasiados commits en la rama... squash them!!
tags: 
- git
- squash
categories: 
- Tips
twitter_text: "¿Sabes hacer GIT commits Squash?"
author: fer
---

A menudo se nos van de las manos los commits que hacemos: pequeños cambios que se nos olvidan, fixes que no podemos probar en local... nos queda una rama (y la pull request) con una veintena de commits cada uno con cambios muy pequeños. Para limpiar este caos, podemos unificar los commits haciendo **squash**:

```shell
git rebase -i master

# (use 's' to mark the commits to squash)

# In case of conflicts:
git mergetool
git rebase --continue

# Then finally push (forcing) to remote branch
git push -f origin feature/my-branch-name
```

