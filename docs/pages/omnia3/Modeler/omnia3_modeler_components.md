---
title: Components
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

OMNIA Platform contains a small number of internal components, and new ones can be added to each model, according to its needs. Multiple packages with different components can be uploaded, and you can develop your own components. To start, we suggest using the package made available by the OMNIA Platform, that you can find <a href="https://github.com/OMNIALowCode/omnia-base-components" target="_blank">here</a>.

## 2. Components Structure

On the modeler perspective, a Component is composed by the following definitions:

### Attributes

The component attributes contain data relevant to define the component and change how it renders and behaves on a page. A component can have multiple attributes, and they can be different between components.

An attribute can be required, and have a default value to be suggested when modeling. Depending on the attribute _direction_ configuration, its value can be only read (Outbound direction) or changed (Inbound direction), or both (TwoWay direction).

Some scenarios where attributes can be applied are setting/getting the component value or if it rendered as readOnly. An attribute value can be set in multiple ways.

### Events

Component Events are code expressions executed on different moments when interacting with the component.

When the event is executed, it receives a list of parameters on object _params_. These parameters can be of multiple types, and contains the values of the _Outbound_ and _TwoWay_ properties.

### Methods

While events are executed automatically as a result of the user interaction with the component, Methods are executed as a explicit call on a code expression.

The Methods have entry parameters, whose values should be sent when calling them. A component can have as many Methods as necessary.

## 2. Internal Components

OMNIA Platform has four internal components:

### forEach

The forEach Component iterates a collection, and renders other Components and data for each record of the collection.

A common scenario for this component is to render lines of a _Collection_ attribute (Commitment, Event, or non-root Generic Entity).

- Properties:

This Component only has a configurable property, named _binding_. This attribute is used to define the collection that will be iterated.

| Property | Direction | Data Type | Description                                                          |
| -------- | --------- | --------- | -------------------------------------------------------------------- |
| query    | Inbound   | Object    | This property is used to define the collection that will be iterated |

- Events:

This Component does not has events.

### runQuery

The runQuery Component executes a previously modeled query and returns the result to be rendered.

A common scenario for this component is to execute a query that feeds a list.

- Properties:

| Property     | Direction | Data Type       |                                                                                       | Description |
| ------------ | --------- | --------------- | ------------------------------------------------------------------------------------- | ----------- |
| query        | Inbound   | Reference/Query | The modeled query to be executed                                                      |
| records      | Outbound  | Object          | The records obtained as the result of the query execution                             |
| columns      | Outbound  | Object          | The structure of the columns returned on each record                                  |
| dataSource   | Inbound   | Text            | The dataSource instance where the query is going to be executed                       |
| parameters   | Inbound   | Object          | Parameters to be applied when executing the query                                     |
| filters      | Inbound   | Object          | The filters to be applied to the query                                                |
| sorting      | Inbound   | Object          | The sorting criteria to be applied                                                    |
| currentPage  | Inbound   | Integer         | The number of the page being retrieved                                                |
| pageSize     | Inbound   | Integer         | The number of records to be returned                                                  |
| totalPages   | Outbound  | Integer         | The total number of pages that can be obtained for the current query and page size    |
| totalRecords | Outbound  | Integer         | The total number of records that can be returned as the result of the query execution |
| isLoading    | Outbound  | Boolean         | Boolean to indicate if the query is being executed and data is still loading          |

- Events:

| Event       | Description                                                          |
| ----------- | -------------------------------------------------------------------- |
| BeforeLoad  | Code executed before making the request to the API                   |
| OnLoad      | Code executed when data is retrieved from API, before being rendered |
| OnLoadError | Code executed when the request to retrieve data returns an error     |

- Methods:

| Method    | Description                                          |
| --------- | ---------------------------------------------------- |
| refresh   | Method that executes the query to retrieve new data  |
| exportCSV | Method that requests to the API a data export to CSV |

### entityForm

The entityForm Component renders a Form composed by other Components inside a page.

A common scenario for this component is to show a Form to create/edit records.

- Properties:

| Property         | Direction | Data Type | Description                                                                               |
| ---------------- | --------- | --------- | ----------------------------------------------------------------------------------------- |
| definition       | Inbound   | Reference | The modeled entity the Form is referencing                                                |
| dataSource       | Inbound   | Text      | The dataSource instance where the entity is being created/edited                          |
| code             | Inbound   | Text      | The instance of the definition being edited                                               |
| data             | Outbound  | Object    | The instance data contained in the form component                                         |
| hasChanges       | Outbound  | Boolean   | Flag to indicate if the data contained in the form has changed                            |
| useTemporary     | Inbound   | Boolean   | Flag to indicate if the create/edit operation is using a Temporary                        |
| hasErrors        | Outbound  | Boolean   | Flag to indicate if the form has errors                                                   |
| state            | Outbound  | Object    | The state machine state of the entity                                                     |
| newInstance      | Outbound  | Boolean   | Flag to indicate if a we're creating a new entity                                         |
| hasAfterSave     | Outbound  | Boolean   | Flag to indicate if the entity type has an after save behaviour                           |
| isProcessing     | Outbound  | Boolean   | Flag to indicate if a request is being processed                                          |
| security         | Outbound  | Object    | Object that has a set of flags with the user privileges to read, write, delete or destroy |
| attributes       | Outbound  | Object    | The set of the attributes of the entity type the form is referencing                      |
| hasSensitiveData | Outbound  | Boolean   | Flag to indicate if the form contains sensitive data                                      |

- Events:

| Event             | Description                                                                                                               |
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

- Methods:

| Method | Description                                                                                                                                       |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| save   | Method that makes a request to the API to save the form data. It has 2 optional parameters related to the state machine: _decision_ and _comment_ |

### selector

The Selector component retrieves an Enumerator keys and labels translated to the user current language.

This component can be used to obtain Enumerator data to be used by another element or behaviour.

- Properties:

| Property | Direction | Data Type | Description                                                                                     |
| -------- | --------- | --------- | ----------------------------------------------------------------------------------------------- |
| selector | Inbound   | Reference | This attribute is used to define the Enumeration Selector whose configuration will be retrieved |
| entries  | Outbound  | Object    | A list containing the entries of the Enumeration                                                |

- Events:

| Event  | Description                                                                                                                                          |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| OnLoad | Code executed when Enumerator data is retrieved from API, before being rendered. Can be used to store that data to be rendered on a select Component |

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

Components are available to be used on modeled Pages. See how its done [here](omnia3_modeler_pages.md).