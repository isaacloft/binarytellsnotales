---
title: Integrate eslint with vscode
date: 2019-05-21 09:56:27
tags: tools
categories: tools
---


### 1. Set up project with eslint

<b>Reference articles</b>
* [set up eslint](https://medium.com/comparethemarket/eslint-visual-studio-code-editor-integration-for-the-win-1bcf38f6ccd4)
* [set up prettier-eslint](https://medium.freecodecamp.org/integrating-prettier-with-eslint-and-stylelint-99e74fede33f)

[Demo code](https://github.com/isaacloft/eslint-integration-vscode) for configuration below

#### Install eslint dependencies
``` bash
npm install --save-dev \
eslint \
babel-eslint \
eslint-config-airbnb \
eslint-config-babel \
eslint-config-prettier \
eslint-plugin-import \
eslint-plugin-react \
prettier \
eslint-plugin-prettier
```
<!--more-->

#### create .eslintrc file in your project root
```json
{
  "extends": ["airbnb", "plugin:prettier/recommended", "plugin:jsx-a11y/recommended"],
  "plugins": ["prettier", "jsx-a11y"],
  "parser": "babel-eslint",
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true,
    "jest": true,
    "node": true
  },
  "rules": {
    "react/prop-types": 0,
    "indent": [0, "tab"],
    "no-unused-expressions": "warn",
    "no-useless-concat": "warn",
    "block-scoped-var": "warn",
    "consistent-return": "warn",
    "no-invalid-this": 0,
    "react/jsx-filename-extension": 0,
    "arrow-body-style": ["warn", "as-needed"],
    "import/no-named-as-default": 0,
    "import/no-named-as-default-member": 0
  }
}

```
#### Create .eslintignore file in your project root
```json
node_modules/
public/
config/
test/

```

-------
### 2. Set up project with prettier-eslint
```bash
npm install --save-dev prettier-eslint prettier-eslint-cli
```

#### Update package.json scripts
```json
    "lint": "eslint --fix src",
    "fix-code": "prettier-eslint --write 'src/**/*.{js,jsx}' "
```

#### Configure vscode to use prettier-eslint
Configure a few VSCode settings:

"prettier.eslintIntegration": true — tells Prettier to use prettier-eslint instead of Prettier

"prettier.stylelintIntegration": true — tells Prettier to use prettier-stylelint instead of Prettier

"eslint.autoFixOnSave": false — we don’t need ESLint to fix our code for us directly, since prettier-eslint will be running eslint --fix for us anyways.

"editor.formatOnSave": true — runs Prettier with the above options on every file save, so you never have to manually invoke VSCode’s format command.

Additionally, you can check-in the above workplace settings to source control so its easier for other team members to set up their editors. You can do so by creating a .vscode folder at the root of your project and putting all of the above rules in a settings.json file.

#### Optionally, set up [.prettierrc](https://prettier.io/docs/en/configuration.html)

```json
{
  "printWidth": 100,
  "singleQuote": true,
  "trailingComma": "all"
}

```

Note: Even with eslint, it cannot fix everything for us.