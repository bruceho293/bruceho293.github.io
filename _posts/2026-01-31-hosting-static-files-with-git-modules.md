---
layout: post
title: "Hosting Static website from another repo with Git Submodules"
date: "2026-01-31 20:07:00"
categories: frontend
tag: [git, web]
---

# Objective
Since with [**Glitch latest updates**](https://blog.glitch.com/), web hosting with static files is not possible anymore. Therefore, I would like to find other alternative to host the static website (containing only plain HTML, CSS and JS) through Jekyll, GitHub Pages and use Git Submodules to pull the codebase of the one-math-game into this website.

# Step to reproduce
1. Since the webgame file are all static, we can store them inside the `assets/one-math-game`
2. We can run the command as followed to pull the repo as a submodule `git submodule add https://github.com/bruceho293/one-math-game.git assets/one-math-game`
3. For pulling the updates we can simply just do a `git pull` inside the submodule repo
```shell
cd assets/one-math-game
git pull
```
4. After the changes are pull, I need to make sure I pushed the changes to make it visible in the GitHub Pages.

# Result
Now you can access the game through GitHub page from here

👉 [Open One-Math-Game](/assets/one-math-game/index.html)