---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 BMLDataSource"
sidebar: omnia3_sidebar
permalink: omnia3_languages_BMLDataSource.html
folder: omnia3
---

# DataSource
Representation of a system that allows to store entities and/or execute behaviours.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..24 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | 0..1024 | The textual explanation of the entities' purpose. |
| Attributes | Attribute | Composite | 0..* | None | A collection of entries that allows to define entity' structure. |
| EntityBehaviours | EntityBehaviour | Composite | 0..* | None | A collection of entries representing how the entity behaves. |
| DataBehaviours | DataBehaviour | Composite | 0..* | None | A collection of entries representing how the entity' data is stored and retrieved. |
| BehaviourNamespaces | BehaviourNamespace | Composite | 0..* | None | A collection of entries representing the coding namespaces to be included (as usings) on code generated with your data and entity behaviours. |
| BehaviourRuntime | RuntimeLocation | None | 1..1 | None | The location where the entitys' behaviours are executed. |
| DataAccessRuntime | RuntimeLocation | None | 1..1 | None | The location where the data behaviours are executed. |
| ExecutesInConnector | Boolean | None | 1..1 | None | Indicates if the Data Source is executed using the platform's connector. |
| BehaviourDependencies | BehaviourDependency | Composite | 0..* | None | A collection of entries that allows to define which dependencies are loaded in the Data Source. |

## Operations

| Name | Type | Description |
| --------- | --------- | --------- |
| Defaults | Initialize |  |

