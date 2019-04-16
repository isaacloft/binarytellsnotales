---
title: Integrate prettier with stylelint in VSCode
date: 2019-04-16 11:04:36
tags: tools
categories: tooling
---

## With VSCode, intergrate stylelint is super easy, just follow steps below and you're all set.


### Install vscode extensions
There are two required vscode extensions:
1. prettier
2. stylelint

### Install packages
Choose your favorite package manager and install dependecies like below
[stylelint-config-standard](https://www.npmjs.com/package/stylelint-config-standard)
[prettier-stylelint](https://www.npmjs.com/package/prettier-stylelint)

```bash
yarn add prettier-stylelint stylelint-config-standard --dev
```

stylelint-config-standard is just one of many stylint configurations, you can use any ones you prefer. 

<!--more-->

### Create .stylelintrc and .prettierrc files at the root of your project

.stylelintrc file should look at least like this
```bash
{
   "extends":"stylelint-config-standard",
    // extends is the configuration package we installed,
    // you can choose your own configuration package and update here
}
```

.prettierrc file looks like this
```bash
{
   // "printWidth": 100,
   // "singleQuote": true,
   // "trailingComma": "all"
}
```
You can leave as an empty object or define more personal settings in here, your vscode prettier extension is going to pick those
up and use with stylelint configurations.

### Update your vscode extension settings 

1. Go to your vscode setting and navigate to text-editor section and click on formatting, then tick format on save option.
{% asset_img format-on-save.jpg This is an example image %}

2. Go to vscode setting and navigate to extension section, find your prettier tab and click on it.
Scroll down the settings and find this option and tick.
{% asset_img use-stylelint.jpg This is an example image %}

This should be it! Go mess up one css or scss file and save it, you should see the file being formatted on saving.

### Before wrap it up
It would be nice for us to setup a script to format all existing files.

Add script to your package.json
```bash
 "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "fix-styles": "prettier-stylelint --write 'src/**/*.{css,scss}' "
    //You can update your directory if it needs to
  },
```
Now if open your project terminal and run below
```bash
$ yarn fix-styles // or npm fix-styles 
```

You should have all your css and scss files formatted.


### Optional but useful
It's likely that you have third party styling files inside your project, and you may not need to format these.
We can set up rules to ignore them. There are two options:
1. In your .stylelintrc add ignoreFiles
```bash
{
   "extends":"stylelint-config-standard",
   "ignoreFiles": "./src/static/**",
}
```
2. Create .stylelintignore file in the root directory and then add routes you'd like to ignore (just like .gitignore)
```bash
./src/static/**
```

More information on how to configure your stylelint rules, [here](https://github.com/stylelint/stylelint/blob/master/docs/user-guide/configuration.md)


