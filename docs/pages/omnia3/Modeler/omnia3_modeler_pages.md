---
title: Themes
keywords: lowcode user interface pages
summary: "All the information regarding OMNIA Platform Pages. Design your application screens as you want."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_pages.html
folder: omnia3
---

## 1. Introduction

In OMNIA Platform Pages you can manage entity instances, list records, or do something completely different.

This feature allows you to model as many pages as you want in your applications. Unlike Forms, Pages are not necessarily associated to an entity.

The elements that compose a Page, from Inputs to Buttons, are named Components. [Click here](omnia3_modeler_components.html) to learn more about them.

## 2. Modeling Pages

### How to add a new Page?

To add a new page go to the Modeling area, find the **_User Interface / Pages_** option on the menu and access it. This will take you to your Pages management dashboard.

Now select _Add new_ and fill in the following information:

- **Name**: the name of the asset (needs to be unique within the model);
- **Description**: the textual explanation of the theme's purpose (can be used as development documentation).
- **Select a template**: the template to be used as base when generating the page. There are three possibilities:
  - **Create an empty blank page**: generate a new empty Page;
  - **Create or update an Entity**: generate a Page ready to create or update a given Entity. Can be used instead of the automatically generated Form;
  - **List entities returned by a Query**: generate a Page that, based on a given query, is ready to show records on a list. Can be used instead of the automatically generated Dashboard.

### How to edit a Page?

By accessing **_User Interface / Pages_** in the sidebar and selecting one from the list.

You can not only change your Page design, but also generate the page again, based on a template.

### Variables

Each page can have its own set of Variables. The purpose of the Variables is to temporarily store data relevant to the page usage.

As an example, variables can be used to store the Url to redirect when exiting the page, or to set a flag that controls a loader to be shown when something is processing and users must wait for it to end.

When we create a new Page based on a template, the following Variables are created:

- Create or Update an Entity:

| Variable                 | Type    | Description                                                                                  |
| ------------------------ | ------- | -------------------------------------------------------------------------------------------- |
| RedirectTo               | Text    | The OMNIA page address to redirect the user                                                  |
| ShowErrors               | Boolean | Boolean to indicate if page errors should be visible                                         |
| IsLoading                | Boolean | Boolean to indicate if the page is loading. A loader is shown if true                        |
| openCodes                | Text    | A list of collection records whose details are opened                                        |
| decisions                | Object  | A list of state machine decisions to be rendered                                             |
| mainDecision             | Object  | The main state machine decision                                                              |
| stateMachineDropDownOpen | Boolean | Boolean to control if the state machine dropdown is opened                                   |
| optionsDropDownOpen      | Boolean | Boolean to control if the options button dropdown is opened                                  |
| canDelete                | Boolean | Boolean to control if the user has privileges to request a entity deletion                   |
| canDestroy               | Boolean | Boolean to control if the user has privileges to request a entity sensitive data destruction |

- List entities returned by a Query:

| Variable         | Type    | Description                                                                          |
| ---------------- | ------- | ------------------------------------------------------------------------------------ |
| CurrentPage      | Integer | The number of the page being currently shown in the list                             |
| PageSize         | Integer | The number of records being requested when executing the query                       |
| detailsPage      | Text    | The code of the Page modeled to be opened when navigating to create or edit a record |
| listSorting      | Object  | The list of columns where sorting are applied                                        |
| listFilters      | Object  | The list of columns where filters are applied                                        |
| filterPanelState | Text    | The state of the list filter panel visibility. It can be either 'closed' or 'opened' |
| listErrors       | Text    | The list of errors of the rendered data list                                         |

#### How to add a variable?

On modeler, navigate to a page and on the right side menu open option **_Variables / Add variable_**.

Fill the following parameters:

- **Name**: the name of the Variable (needs to be unique within the Page);
- **Description**: the textual explanation of the Variable purpose (can be used as development documentation).
- **Kind**: the kind of the variable. Can be of type Primitive, an OMNIA definition (Agent, Resource, ...) or a Component Type. These types are exposed by the component packages;
- **Type**: the type of the variable
- **Is required value?**: define if the variable must have a value;
- **Is a list of records?**: define if the variable contains more than one record of the given type;
- **The initial value of the variable**: the value the variable is initialized with.

#### How to use a variable?

Variables can be used on Code Expressions within the page. They are available on _variables_ object.

```Javascript
function companyFormPage_Initialize({ context, variables, urlParameters, refs }, params) {
    variables.myFirstVariable = "My variable value";
    alert(variables.myFirstVariable);
}
```

### Url Parameters

A Url Parameter is the definition of data that will be sent to the Page as a part of its URL.

As an example, given the following Url:

```
    https://www.example.com/widgets?color=blue&size=large
```

We have two URL parameters to define in our page: color and size.

When we create a new Page based on a template, the following Url Parameters are created:

- Create or Update an Entity:

| Url Parameter | Type | Description                                                                |
| ------------- | ---- | -------------------------------------------------------------------------- |
| code          | Text | The code of the entity to be edited. It's not used when creating an entity |

- List entities returned by a Query:

No Url parameters are created when executing this template.

#### How to add a Url Parameter?

On modeler, navigate to a page and on the right side menu open option **_Url Parameters / Add parameter_**.

Fill the following parameters:

- **Name**: the name of the Url Parameter (needs to be unique within the Page);
- **Description**: the textual explanation of the Url Parameter purpose (can be used as development documentation);
- **Type**: the type of the Url Parameter. It can be a Primitive type or an Object;
- **Is a list of records?**: define if the Url Parameter contains more than one record of the given type;

#### How to use a Url Parameter?

Variables can be used on Code Expressions within the page. They are available on _variables_ object.

```Javascript
function companyFormPage_Initialize({ context, variables, urlParameters, refs }, params) {
    const codevalue = urlParameters.code;
}
```

### Behaviours

OMNIA Platform Pages only have one behaviour available: Initialize.

As on other modeling features like Forms or Dashboards, this Behaviour will be executed when accessing the page.

Other Behaviours that are usually available (e.g. Formula, On Change, Before Save) should now be implemented on [Components](omnia3_modeler_components.md).

### Scripts

Each page has a _Scripts_ code area that can be used to define JavaScript functions to be used on multiple code expressions within the page.

The script is composed by a class named after the page. The custom code must be added inside this class.

```Javascript
class CompanyFormPageScripts {

//add your code here

}

const companyFormPage = new CompanyFormPageScripts();
```

The developed functions can be called from any page code expression as follows:

```Javascript
companyFormPage.showAlert("Hello World!");
```

### Styles

To add CSS Styles to a page, you can use the global CSS Styles described [here](omnia3_modeler_cssStyles.md), or add styles specific to the page being modeled.

#### How to use a global style?

On modeler, navigate to a page and on the right side menu open option **_Properties_**, and _Styles_ area will be available.

To use a global style, simply introduce the CSS classes on property _classesStyles_.

#### How to add a page style?

On modeler, navigate to a page and on the right side menu open option **_Properties_**, and _Styles_ area will be available.

You can add page specific styles by introducing them on property _styles_.These styles can then be used in the page or page components.

### Components

#### How to add a component to a page?

On modeler, navigate to a page and on the right side menu open option **_Drag to add_**.

The list of components available on the model will be available, and you can drag them to the page preview area.

After adding the component to the page, their Attributes, Behaviours and Styles should be defined.