# ESLINT - CHECK JS SYNTAX

## Step 1

npm install -g eslint
npm install --save-dev eslint eslint-config-airbnb eslint-plugin-import eslint-plugin-react eslint-plugin-jsx-a11y babel-eslint

## Step 2

Backup your eslintrc file in case you want to examine it.

## Step 3

eslint --init
Select 'Use a popular style guide'
Select Airbnb
Select JSON
Select your options, pick JSON type (.eslintrc is the old filename based on my research, but it's the same thing)
Allow it to update newer versions and/or install packages if it asks

## Step 4

Restart your editor

## Step 5

Paste this into your .eslintrc.json:
and remove my comments which will cause the JSON to blow up

```json
{
    "env": {
        "node": true,
        "browser": true,
        "es6": true
    },
    "parser": "babel-eslint",
    "extends": [
        "airbnb"
    ],
    "plugins": [
        "react",
        "react-native",
        "babel",
        "flowtype",
        "jsx-a11y"
    ],
    "rules": {
        ...
    }
}
```

---
