---
title: Pages
keywords: lowcode user interface page generator
summary: "All the information regarding OMNIA Platform Page generators. Create new pages for your entities with a couple of clicks."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_page_generators.html
folder: omnia3
---

## 1. Introduction

You have full freedom to design your model [Pages](omnia3_modeler_pages.md) as you want.

But sometimes we just need to quicky create a Page, to be used as a starting point or on a Demo.

To ensure this scenario is covered, Omnia Platform includes a page generator. This generator has a couple of templates that can be used to create pages that cover specific use cases.

## 2. Generate a Page

When adding a new page, modelers are prompted to choose a template. The following templates are available:

- **Create an empty blank page**: generate a new empty Page;
- **Create or update an Entity**: generate a Page ready to create or update a given Entity. Can be used instead of the automatically generated Form;
- **List entities returned by a Query**: generate a Page that, based on a given query, is ready to show records on a list. Can be used instead of the automatically generated Dashboard.

When the template is executed, it generates a page that is ready to be used. The result includes a number of Components, Variables and Url Parameters. To generate a page the [Omnia Base Components](https://github.com/OMNIALowCode/omnia-base-components) package must be imported.

When a page is generated using a template, the following variables are created:

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

At last, the following Url Parameters are created when generating a page:

- Create or Update an Entity:

| Url Parameter | Type | Description                                                                |
| ------------- | ---- | -------------------------------------------------------------------------- |
| code          | Text | The code of the entity to be edited. It's not used when creating an entity |

- List entities returned by a Query:

No Url parameters are created when executing this template.
