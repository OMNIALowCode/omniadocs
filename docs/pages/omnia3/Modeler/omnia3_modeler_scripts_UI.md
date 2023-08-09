---
title: Scripts
keywords: lowcode user interface scripts javascript
summary: "All the information regarding our User Interface Scripts. Define JavaScript code that can be used on other UI code expressions."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_scripts_UI.html
folder: omnia3
---

## 1. Introduction

This feature allows you to add Javascript code that can be used on other UI code expressions.

On each model you can have multiple Scripts. Each script is composed by a class, named after the script. 


```Javascript
  /** 
 * You can invoke these class methods in the expression and behaviours code. Use the 'helpers' object to do it.
 */
class HelpersScripts {

}

const helpers = new HelpersScripts();
```

## 2. Modeling Scripts

### How to add a new Script?

To add a new script go to the Modeling area, find the **_User Interface / Scripts_** option on the menu and access it. This will take you to your scripts management dashboard.

Now select _Add new_ and fill in the following information:

- **Name**: the name of the script (needs to be unique within the model);
- **Description**: the textual explanation of the script (can be used as development documentation);
- **Order**: the order that the script class will be loaded;
- **Execute the following code**: the code expression of the script.


### How to edit a Script?

By accessing **_User Interface / Scripts_** in the sidebar and selecting one from the list.

You can edit the Description, load order or change the code expression.

## 3. Scripts Usage

The code developed on Scripts is available to be used on any other Javascript code expression, simply by calling the implemented functions.

Considering a Script named _Helpers_, with a function named _showAlert_ that shows a message.

```Javascript
/** 
 * You can invoke these class methods in the expression and behaviours code. Use the 'helpers' object to do it.
 */
class HelpersScripts {
    showAlert(message) {
        alert(message);
    }
}

const helpers = new HelpersScripts();
```

To use this function, we just need to call it:

```Javascript
helpers.showAlert("Hello World!");
```