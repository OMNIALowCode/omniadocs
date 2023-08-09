---
title: Themes
keywords: lowcode user interface components
summary: "All the information regarding our User Interface Components. Use your own Components on OMNIA Pages"
sidebar: omnia3_sidebar
permalink: omnia3_modeler_components.html
folder: omnia3
---

## 1. Introduction

On OMNIA Platform models, you can add your own Components to be used on [Pages](omnia3_modeler_pages.md).

These components have the same purpose as the ones available on Forms and Dashboards but, unlike those, they can be fully controlled by the modeler.

Components can be visual (e.g. inputs) or functional. Users can interact with the visual components directly, while functional components are used to execute multiple processes behind the screen (e.g. fetch data, act as container to render other elements).

OMNIA Platform contains a small number of base components, and new ones can be added to each model, according to its needs. Multiple packages with different components can be uploaded, and you can develop your own components. To start, we suggest using the package made available by the OMNIA Platform, that you can find [here](https://github.com/OMNIALowCode/omnia-base-components).

## 2. Base Components

OMNIA Platform has four base components:

### forEach

The forEach Component iterates a collection, and renders other Components and data for each record of the collection.

A common scenario for this component is to render lines of a _Collection_ attribute (Commitment, Event, or non-root Generic Entity).

- Component Attributes:

This Component only has a configurable attribute, named _binding_. This attribute is used to define the collection that will be iterated.

### runQuery

The runQuery Component executes a previously modeled query and returns the result to be rendered.

A common scenario for this component is to execute a query that feeds a list.

- Component Attributes:

| Attribute   | Description                                                     |
| ----------- | --------------------------------------------------------------- |
| query       | The modeled query to be executed                                |
| dataSource  | The dataSource instance where the query is going to be executed |
| parameters  | Parameters to be applied when executing the query               |
| filters     | The filters to be applied to the query                          |
| sorting     | The sorting criteria to be applied                              |
| currentPage | The number of the page being retrieved                          |
| pageSize    | The number of records to be returned                            |

- Component Behaviours:

| Behaviour   | Description                                                          |
| ----------- | -------------------------------------------------------------------- |
| BeforeLoad  | Code executed before making the request to the API                   |
| OnLoad      | Code executed when data is retrieved from API, before being rendered |
| OnLoadError | Code executed when the request to retrieve data returns an error     |

### entityForm

The entityForm Component renders a Form composed by other Components inside a page.

A common scenario for this component is to show a Form to create/edit records.

Component Attributes:

| Attribute    | Description                                                           |
| ------------ | --------------------------------------------------------------------- |
| definition   | The modeled entity the Form is referencing                            |
| dataSource   | The dataSource instance where the entity is being created/edited      |
| code         | The instance of the definition being edited                           |
| useTemporary | Boolean to indicate if the create/edit operation is using a Temporary |

Component Behaviours:

| Behaviour         | Description                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------- |
| OnSave            | Executed when the Save operation is finished with success. Can be used to show a success message and redirect the user    |
| OnSaveError       | Executed when the Save operation is finished with error. Can be used to show the error to the user                        |
| OnDelete          | Executed when the Delete operation is finished with success. Can be used to show a success message and redirect the user  |
| OnDeleteError     | Executed when the Delete operation is finished with error. Can be used to show the error to the user                      |
| OnDestroy         | Executed when the Destroy operation is finished with success. Can be used to show a success message and redirect the user |
| OnDestroyError    | Executed when the Destroy operation is finished with error. Can be used to show the error to the user                     |
| OnLoad            | Executed when the data Load operation is finished with success. Can be used to remove a loader                            |
| OnLoadError       | Executed when the data Load operation is finished with error. Can be used to show the error to the user                   |
| OnUpdateData      | Executed when the Update operation is finished with success                                                               |
| OnUpdateDataError | Executed when the Update operation is finished with error. Can be used to show the error to the user                      |

### selector

The Selector component retrieves an Enumerator keys and labels translated to the user current language.

This component can be used to obtain Enumerator data to be used by another element or behaviour.

Component Attributes:

This Component only has a configurable attribute, named _selector_. This attribute is used to define the Enumeration Selector whose configuration will be retrieved.

Component Behaviours:

This Component only has a Behaviour type, named _onLoad_. This behaviour is executed after Enumerator data was retrieved, and can be used to store that data to be rendered on a select Component.

## 3. Modeling Components

### How to add a new Components package?

To add a new components package go to the Modeling area, find the **_User Interface / Components_** option on the menu and access it. This will take you to your components package management dashboard.

Now select _Add new_ and fill in the following information:

- **Name**: the name of the asset (needs to be unique within the model);
- **Description**: the textual explanation of the theme's purpose (can be used as development documentation).
- **Component file**: the package file (\*.tgz) that contains a set of components.

### How to edit a Components package?

By accessing **_User Interface / Components_** in the sidebar and selecting one from the list.

You can upload a new version of the components package.

## 4. Components Usage

Components are available to be used on modeled Pages.

After a Components Package is imported, components are listed on the Page _Drag to Add_ option, along with Base Components:

<p align="center">
  <img src="/images/modeler/Modeler-Components-List.jpg">
</p>

You can drag them to the Page preview area and change their Attributes, Behaviours and Styles. Each Component exposes a different set of Attributes, Behaviours and Styles that you can configure while modeling.

Focusing on Attributes and Styles, its value can be set in different ways:

| Value Source | Description                                                      |
| ------------ | ---------------------------------------------------------------- |
| Direct       | Value is set directly, with a static value                       |
| Binding      | The dataSource instance where the entity is being created/edited |
| Expression   | Value is computed using a Javascript code expresion              |
| Asset        | Value is selected from the list of model Assets                  |
| Translation  | Value is selected from the list of model Translations            |

As for Behaviours, its value is always a Javascript code expression.