---
title: Application Menu
keywords: lowcode web app development menu
summary: "All the details about our Application Menu feature and how you can build custom menus for your web applications."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_menu.html
folder: omnia3
---

## 1. Introduction

Each model has an Application Menu definition that will be available in the Application, exposing its options to the user.
The menu can be customized or you can leave to the Platform the responsibility of generating a proposal at Build time.

In case of a customized Application Menu, a new menu entry will be automatically added to the menu root when a new Entity or Dashboard is created.

It's only possible to have one menu in the Application.

## 2. How to customize a Menu?

_Before you start, make sure that you have at least one successful build of your model. The customization is based on the menu proposed at build time._

By accessing **_User Interface / Menu_** in the sidebar, you will have access to the Menu modeling screen.

A Menu is a hierarchical structure composed by nested menu entries. Each Menu Entry is defined by:

- **name**: the entry name (should be unique in a menu);
- **label**: the element caption;
- **row**: the layout row in which the element will be placed;
- **column**: the layout column in which the element will be placed;
- **size**: the element size on a scale of 1 (the smaller size) to 12 (the bigger size);
- **actionType/actionLocation**: the menu entry type. The type defines which action should happen when the user clicks;
- **Icon**: You can consult the available icons at [Font Awesome version 4.7.0](https://fontawesome.com/v4.7.0/){:target="\_blank"};
- **color**: color to display when hovering the menu entry;
- **isHidden**: the visibility of the element (hidden or visible);

The menu can be configured to start collapsed or expanded, by changing the value of the _isCollapsed_ attribute. By default the menu starts expanded.

By default, each menu entry that is not a container can be set as a _Favorite_ by the users. The _Favorites_ feature can be disabled by changing the value of the _disableFavorites_ attribute.

## 3. User Interface Behaviours

**_User Interface / Menu / User Interface Behaviours_**

In order to extend your application's user interface you can add new behaviours to your menu's user interface.

Click [here](omnia3_modeler_uibehaviours.html), to know more about user interface behaviours.

## 4. Breadcrumb

The application will use the menu definition to calculate breadcrumb labels. The Rules to calculate the label are:

1.  Use the menu entry label if the definition is a member of the Menu.
2.  Use the Dashboard label if the definition is a Dashboard and not a member of the Menu.
3.  Use the Form label if the definition is a Form and not a member of the Menu.
