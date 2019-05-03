---
title: 'Code Challenge: Conway''s Game of Life'
date: 2019-05-03 09:20:58
tags: [frontend, typescript, react, react hooks]
categories: frontend
---


#### Complete code challenge: Conway's game of life, aka cell simulator, using react hooks and typescript

[Demo on Heroku](https://cell-simulator.herokuapp.com/)
[Github](https://github.com/isaacloft/Cell-Simulator)

Recently I've been given this code challenge, I feel this is one of the best code challenges I've ever come across, as it needs the challenger to have a good overall frontend knowledge and practical problem solving skills. 
<!--more-->

If requirements include which frontend framework to use, which scss convention to follow, it can take good hours to complete.

A brief requirement of [Conway's game of life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)
``` bash
The "game" is a zero-player game, meaning that its evolution is determined by its initial state, 
requiring no further input. One interacts with the Cell Simulator by creating an initial configuration 
and observing how it evolves.

How cells evolve:
Each cell can have two state, live or dead. 
- When the game is running:
  - A Cell with <2 live neighbours is set to dead
  - A Cell with 2 or 3 live neighbours lives
  - A Cell with >3 live neighbours is set to dead
  - A dead Cell with exactly 3 live neighbours is set to live
  - A Cell who "comes to life" outside the board should wrap at the other side of the board.
    (Just like the Snake, the cell can travel from left edge to right edge)

- Once the next generation is done, User can trigger "next generation" again.

ACs
- At initial state, User should see an empty board.
- User can make Cells "alive".
- User can make Cells "dead".
- User can trigger "next generation".
- User can trigger a "reset" to the initial state.

```

My solution uses: 
- React
- React hooks
- Typescript
- Create My React App with Typescript
- SCSS and [Chainable BEM Modifier](https://binarytellsnotales.com/2019/04/15/chainable-bem-modifier/)
- Inlcude TSLint and StyleLint

#### One thing to be careful with: Data mutation
When writing the algorithm to update the state of cells, we have to understand all existing cells,
either dead or live, should check number of neighbors at the same time. 

My javascript translation is that our code should be able to keep a copy of cell array to check against with. I did it wrong at first place because in side the loop, cells are being updated one by one, which means the following cells are checking against <b>"updated predecessor"</b>, while what we really should have is that every single cell checking against the original cell states. If its state needs update, we dont mutate directly, but save it somewhere else.
```javascript
const cellEvolve = (cell: ICell) => {
    // We make a new copy of original cell using spread operator
    const newCell = { ...cell };
    if (cell.isActivated) {
      if (countNeighbours(cell.x, cell.y, cell.id) < 2) {
        newCell.isActivated = false;
      }
      if (countNeighbours(cell.x, cell.y, cell.id) === 2 || countNeighbours(cell.x, cell.y, cell.id) === 3) {
        newCell.isActivated = true;
      }
      if (countNeighbours(cell.x, cell.y, cell.id) > 3) {
        newCell.isActivated = false;
      }
    } else {
      if (countNeighbours(cell.x, cell.y, cell.id) === 3) {
        newCell.isActivated = true;
      }
    }
    // When we done checking against rules, we return the newCell.
    return newCell;
  };

```

Rest of the coding are pretty straightforward, we can even add some fancy effects to the change of the cell states.

Cheers,

