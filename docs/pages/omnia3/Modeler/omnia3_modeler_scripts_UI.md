---
title: Scripts
keywords: lowcode user interface scripts javascript
summary: "All the information regarding our User Interface Scripts. Define JavaScript code that can be used on other UI code expressions."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_scripts_UI.html
folder: omnia3
---

## 1. Introduction

This feature allows you to add JavaScript code that can be used on other UI code expressions.

The Scripts can be used to:

- Improve code maintainability, by writing only once code that is reused on multiple features of your model;
- Improve code organization, by creating multiple scripts with a clear name, each with its set of functions. 

Each Script generates a class, where you can write your code. The class name is composed by the name you defined with the suffix _Scripts_. Below we can see a example of the class generated for _MyLib_ script: 

```Javascript
  /** 
 * You can invoke these class methods in the expression and behaviours code. Use the 'myLib' object to do it.
 */
class MyLibScripts {

}

const myLib = new MyLibScripts();
```

## 2. Modeling Scripts

### How to add a new Script?

To add a new script go to the Modeling area, find the **_User Interface / Scripts_** option on the menu and access it. This will take you to your scripts management dashboard.

Now select _Add new_ and fill in the following information:

- **Name**: the name of the script (needs to be unique within the model);
- **Description**: the textual explanation of the script (can be used as development documentation);
- **Execute the following code**: the code expression of the script.

### How to edit a Script?

By accessing **_User Interface / Scripts_** in the sidebar and selecting one from the list.

You can edit the Description, load order or change the code expression.

## 3. Scripts Usage

The code developed on Scripts is available to be used on any other Javascript code expression, simply by calling the implemented functions.

Considering a Script named _Helpers_, with a function named _showAlert_ that shows a message.

```Javascript
/** 
 * You can invoke these class methods in the expression and behaviours code. Use the 'notification' object to do it.
 */
class NotificationScripts {
    showAlert(message) {
        alert(message);
    }
}

const notification = new NotificationScripts();
```

To use this function, we just need to call it:

```Javascript
notification.showAlert("Hello World!");
```