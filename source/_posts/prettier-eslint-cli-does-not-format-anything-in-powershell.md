---
title: prettier-eslint-cli does not format anything in powershell
date: 2019-05-01 14:25:35
tags: [eslint, prettier, vscode, powershell]
categories: frontend
---

#### prettier-eslint and prettier-stylelint work inside bash and zsh, not in powershell or cmd

Long story short, I've set up eslint and stylelint for one project weeks back and everything ran perfectly on MACs, until we ran it inside powershell and cmd, it output nothing. It almost felt like no file is to be formatted.


Scripts we had inside package.json
``` json
"scripts": {
    "fix-style": "prettier-stylelint --write 'src/**/*.{css,scss}' ",
    "fix-code": "prettier-eslint --write 'src/**/*.{js,jsx}' "
}
```
<!--more-->


After a couple hours of research, I accidentally saw this code on [prettier-eslint-cli](https://github.com/prettier/prettier-eslint-cli), and I gave it a go. It worked..
```json
 "scripts": {
    "format": "prettier-eslint \"src/**/*.js\""
  }
```
Turns out, nothing wrong with dependencies, neither plugins in vscode. It just in powershell, double quote and single quote have different functions. Still not 100% sure, but it is very likely to relate to this [topic](https://devblogs.microsoft.com/scripting/weekend-scripter-understanding-quotation-marks-in-powershell/)

To fix this issue, we simply updated the script to
```bash
"fix-style": "prettier-stylelint --write \"src/**/*.{css,scss}\" ",
"fix-code": "prettier-eslint --write \"src/**/*.{js,jsx}\" "
```




