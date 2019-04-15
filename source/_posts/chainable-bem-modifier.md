---
title: chainable bem modifier
date: 2019-04-15 21:48:43
tags: SCSS
categories: frontend
---


## Chainable BEM Modifier for SCSS

Disclaimer: All following information is coming from Jordan Lewis's [post](https://webuild.envato.com/blog/chainable-bem-modifiers/)
I just happened to use this style of writting scss code to make my life little bit easier.

### Some information about BEM syntax
[BEM](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
``` bash
block__element--modifier
```

<!--more-->

for example: 
``` bash
.site-search {} /* Block */
.site-search__field {} /* Element */
.site-search--full {} /* Modifier */
```
### With Chainable BEM Modifier, it's just easier and prettier to write and understand

The general format of C-BEM-Modifier is:
```bash
js-hook block__element--variation -modifier h-helper is-state
```
<b>JS Hooks</b> are prefixed with js- and do not have any styles. Their whole purpose is to be used in JavaScript to target elements in the DOM.

One example out of the code block below is:
```bash
.game-pane__cell-container--green-cell -is-activated
```
```bash
// `&` below is 'game-pane'
  &__cell-container {
        border: 1px #d1c1c1 solid;
        height: 20px;
        width: 20px;
        box-sizing: border-box;
        background-color: #fff;
        cursor: pointer;
        &.--green-cell {
            background-color: rgb(50, 119, 68);

            &.-is-activated {
                 animation: cellActivating 0.25s;           
            }
        } 
  }
```
