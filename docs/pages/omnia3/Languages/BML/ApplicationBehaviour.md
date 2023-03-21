---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 BMLApplicationBehaviour"
sidebar: omnia3_sidebar
permalink: omnia3_languages_BMLApplicationBehaviour.html
folder: omnia3
---

# ApplicationBehaviour
Behaviour used to extend the application, which execution can be triggered from another behaviour (entity or data) or directly (using the API).
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..32 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | 0..1024 | The textual explanation of the entities' purpose. |
| Expression | Text | None | 1..1 | None | The C# code that will be executed. |
| BehaviourNamespaces | BehaviourNamespace | Composite | 0..* | None | A collection of entries representing the coding namespaces to be included (as usings) on code generated. |
| DataSource | DataSource | Shared | 1..1 | None | The Data Source where the behaviour is executed. |
| ExecutionLocation | ExecutionLocation | None | 1..1 | None | The location where is executed. |

## Operations

| Name | Type | Description |
| --------- | --------- | --------- |
| Defaults | BeforeSave |  |

