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

An attribute can be required, and have a default value to be suggested when modeling. An attribute can be defined with three different _direction_ types:

- **Outbound**: An attribute that is read-only by default. Only the Component can change the value. It cannot be changed when interacting with the page;
- **Inbound**: An attribute whose value can only be changed by page interaction;
- **TwoWay**: An attribute whose value can be changed by the component or as a result of page interaction.

Attributes can have multiple purposes. Let's see some common scenarios:

- Handle a value: When the component is located in a page, it can be bound with a Entity Attribute. We can have an attribute where the value will be available to be rendered
- Change the Component Behaviour: Attributes can change how the Component behaves on a page. As an example, we can have an attribute that sets the Component as readOnly or changes a internal label

An attribute value can be set in multiple ways. See our [Pages](omnia3_modeler_pages.md/#how-to-add-a-element-to-a-page) documentation to learn more.

### Events

On a Component, Events are triggered by user actions. A key press, mouse click or value selection are common events that we execute everyday when interacting with a browser.

When a Component is in a page, it can have a Behaviour associated with the Event. When that happens, the modeled code expression will be executed when the event is triggered.

### Methods

While events are executed automatically as a result of the user interaction with the component, Methods are executed as a explicit call on a code expression.

The Methods have entry parameters, whose values should be sent when calling them. A component can have as many Methods as necessary.

## 2. Internal Components

OMNIA Platform has four internal components:

### forEach

The forEach is a functional Component that iterates a collection, and renders child Components for each record of the collection.

A common scenario for this component is to render lines of a _Collection_ attribute (Commitment, Event, or non-root Generic Entity).

#### Properties

| Property | Direction | Data Type | Description                                                          |
| -------- | --------- | --------- | -------------------------------------------------------------------- |
| binding  | Inbound   | Object    | This property is used to define the collection that will be iterated |

#### Events

This Component doesn't have events.

### runQuery

The runQuery Component executes a previously modeled query and returns the result to be rendered.

A common scenario for this component is to execute a query that feeds a list.

#### Properties

| Property     | Direction | Data Type       |                                                                                       | Description |
| ------------ | --------- | --------------- | ------------------------------------------------------------------------------------- | ----------- |
| query        | Inbound   | Reference/Query | The modeled query to be executed                                                      |
| records      | Outbound  | Object          | The list of records obtained as the result of the query execution                     |
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

#### Events

| Event       | Description                                                          |
| ----------- | -------------------------------------------------------------------- |
| BeforeLoad  | Code executed before making the request to the API                   |
| OnLoad      | Code executed when data is retrieved from API, before being rendered |
| OnLoadError | Code executed when the request to retrieve data returns an error     |

#### Methods

| Method    | Description                                          |
| --------- | ---------------------------------------------------- |
| refresh   | Method that executes the query to retrieve new data  |
| exportCSV | Method that requests to the API a data export to CSV |

### entityForm

The entityForm is a functional Component that can be used to handle a data of a modeled Entity.

It provides properties that handle the read, create, update, delete and destroy operations for a entity instance.

Child components must be included to show data and execute operations.

#### Properties

| Property         | Direction | Data Type             | Description                                                                               |
| ---------------- | --------- | --------------------- | ----------------------------------------------------------------------------------------- |
| definition       | Inbound   | Reference             | The modeled entity the Form is referencing                                                |
| dataSource       | Inbound   | Text                  | The dataSource instance where the entity is being created/edited                          |
| code             | Inbound   | Text                  | The instance of the definition being edited                                               |
| data             | Outbound  | Object                | The instance data contained in the form component                                         |
| hasChanges       | Outbound  | Boolean               | Flag to indicate if the data contained in the form has changed                            |
| useTemporary     | Inbound   | Boolean               | Flag to indicate if the create/edit operation is using a Temporary                        |
| hasErrors        | Outbound  | Boolean               | Flag to indicate if the form has errors                                                   |
| state            | Outbound  | [State](#state)       | The state machine state of the entity                                                     |
| newInstance      | Outbound  | Boolean               | Flag to indicate if a we're creating a new entity                                         |
| hasAfterSave     | Outbound  | Boolean               | Flag to indicate if the entity type has an after save behaviour                           |
| isProcessing     | Outbound  | Boolean               | Flag to indicate if a request is being processed                                          |
| security         | Outbound  | [Security](#security) | Object that has a set of flags with the user privileges to read, write, delete or destroy |
| attributes       | Outbound  | Object                | The set of the attributes of the entity type the form is referencing                      |
| hasSensitiveData | Outbound  | Boolean               | Flag to indicate if the form contains sensitive data                                      |

#### Events

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

#### Methods

| Method               | Description                                                                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| save                 | Method that makes a request to the API to save the form data. It has 2 optional parameters related to the state machine: _decision_ and _comment_ |
| delete               | Method that makes a request to the API to delete the current entity intance                                                                       |
| destroySensitiveData | Method that makes a request to the API to destroy sensitive data for the current entity instance                                                  |

#### Types

##### State

| Property          | Data Type                         | Description                                     |
| ----------------- | --------------------------------- | ----------------------------------------------- |
| decisions         | [StateDecision](#statedecision)   | A list of decisions available on the state      |
| disableAttributes | Boolean                           | Flag to indicate if all attributes are disabled |
| disableOperations | Boolean                           | Flag to indicate if all operations are disabled |
| enabledAttributes | String                            | A list of enabled attributes                    |
| enabledOperations | [StateOperation](#stateoperation) | A list of enabled operations                    |
| name              | String                            | The name of the state                           |

##### StateDecision

| Property    | Data Type | Description                                         |
| ----------- | --------- | --------------------------------------------------- |
| commentType | String    | The type of the comment: None, Optional or Required |
| label       | String    | The label of the decision                           |
| name        | String    | The name of the decision                            |
| order       | Integer   | The order of the decision within the state          |

##### StateOperation

| Property | Data Type | Description                                                                 |
| -------- | --------- | --------------------------------------------------------------------------- |
| path     | String    | The path of the operation. Filled when the operation is inside a collection |
| type     | String    | The type of the operation. Possible values are: Update, Add, Delete         |

##### Security

| Property   | Data Type | Description                                                                     |
| ---------- | --------- | ------------------------------------------------------------------------------- |
| canDelete  | Boolean   | Flag to indicate if the user can delete the current instance                    |
| canDestroy | Boolean   | Flag to indicate if the user can destroy sensitive data of the current instance |
| canRead    | Boolean   | Flag to indicate if the user can read the current instance                      |
| canWrite   | Boolean   | Flag to indicate if the user can create a new instance or make changes          |

### selector

The Selector component retrieves an Enumerator keys and labels translated to the user current language.

This component can be used to obtain Enumerator data to be used by another element or behaviour.

#### Properties

| Property | Direction | Data Type                   | Description                                                                                     |
| -------- | --------- | --------------------------- | ----------------------------------------------------------------------------------------------- |
| selector | Inbound   | Reference                   | This attribute is used to define the Enumeration Selector whose configuration will be retrieved |
| entries  | Outbound  | [SelectorKey](#selectorkey) | A list containing the entries of the Enumeration                                                |

#### Events

| Event  | Description                                                                                                                                          |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| OnLoad | Code executed when Enumerator data is retrieved from API, before being rendered. Can be used to store that data to be rendered on a select Component |

#### Types

##### SelectorKey

| Property | Data Type | Description                     |
| -------- | --------- | ------------------------------- |
| key      | String    | The key of the selector entry   |
| label    | String    | The label of the selector entry |

## 3. Modeling Components

### How to add a new Components package?

To add a new components package go to the Modeling area, find the **_User Interface / Components_** option on the menu and access it. This will take you to your components package management dashboard.

Now select _Add new_ and fill in the following information:

- **Name**: the name of the asset (needs to be unique within the model);
- **Description**: the textual explanation of the theme's purpose (can be used as development documentation);
- **Component file**: the package file (\*.tgz) that contains a set of components.

You can download our Base Components package from the GitHub repository as a source for the property _Component file_ above. In order to do that, click [here](https://github.com/OMNIALowCode/omnia-base-components){:target="\_blank"} to access the repository. Then click on right side option **Releases**,
open the latest version and download the file named **omnia-base-components-vx.x.x.tgz**.

### How to edit a Components package?

By accessing **_User Interface / Components_** in the sidebar and selecting one from the list.

You can upload a new version of the components package.

## 4. Components Usage

Components are available to be used on modeled Pages. See how its done [here](omnia3_modeler_pages.md).

## 5. Create new Components

You can create your own components to ensure the best user experience.

To start, we suggest cloning [OMNIA Base Components](https://github.com/OMNIALowCode/omnia-base-components){:target="\_blank"} repository, check out how the components work and start creating your own Components.
