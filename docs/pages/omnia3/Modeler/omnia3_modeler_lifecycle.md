---
title: Model Lifecycle
keywords: lowcode web app development business model
summary: "Get to know OMNIA's web application development lifecycle: Business Model definition. Build and compile; Reuse models at future web application developments."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_lifecycle.html
folder: omnia3
---

## 1. Introduction
The OMNIA Platform was designed around a development lifecycle with the following steps:
* **Model**: create the model definitions;
* **Build**: compile the model; 
* **Test**: create records using the previously created model;

Each operation is recorded, creating this way a full log of everything was made in the platform.

## 2. History tracking
__*Model info / History*__

It's possible to see all the operations made in the model by accessing the platform's log.

Each record contains the description, the date and who realized the operation.

This way it's possible to all modelers to know who made what and track all the model's changes.

## 3. Model Validators

While you are developing your model (or importing one), _OMNIA Platform_ is constantly validating if your changes are valid. If something is wrong, you'll get a message on the validator result list.

The list of validation messages can be opened by clicking the _Alerts_ option on the right side of the top bar.

There are two message levels:

- Error: The most severe one. Your model is not valid, and you must fix the issue before requesting a _Build_.
- Warning: Even though your model is valid, further configuration is recommended. The model can be built with warnings.

### Common Errors and Warnings

#### Errors

- Data Behaviours are not allowed on non-root entities

A non-root entity contains data behaviours, that are expected only on root entities. These data behaviours must be removed.

- Depends on attribute must be filled when referencing the non-System entity "_ExternalType_"

An attribute whose data is located on a external system must have, on its configuration, a reference to an attribute that contains the instance of the external system to be queried. 

- Query with identifier "_MyQuery_" doesn't exist.

The list is based on a query that no longer exists. The list must be edited to reference another query (or removed if not in use).

#### Warnings

- queryTableDefinition attribute is required

Shown when a list does not have defined its entity type. The list must be edited to set the type, that has to be the same as the query that feeds the list.

## 4. Build the model
__*Model info / Builds*__

After every change in the model it's necessary to create a new build in order to the apply the changes and, that way, the end-users can use the application in its last state.

When you create a new build, all the _C#_ code added in the behaviours will be compiled. If any error occurs during the code compilation the build will fail and all the model changes will be maintained as pending.


### How to create a new build?
In the Modeler environment, simply use the "Build & Deploy" button at the top right corner and wait a few moments until it's finished.

## 5. Download the behaviours code
__*Model info / Builds*__

If you want to download the behaviours code the way it will be executed in the _OMNIA Platform_ (either to test it or to correct some problem), you can do it in the _Builds_ list choosing the option _Download build_ to the build version you want to get.
