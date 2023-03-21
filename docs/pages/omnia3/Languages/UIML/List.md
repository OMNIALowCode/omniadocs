---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLList"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLList.html
folder: omnia3
---

# List
Application list, used to present data from a given Query. A list is little more than a way to see a query displayed in the web app: you select a query, (part or all of) its columns, and how to display those columns.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..64 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | None | The textual explanation of the entities’ purpose. |
| Label | Text | None | 1..1 | None | Label to display in the application. |
| HelpText | Text | None | 0..1 | None | Text/annotation to help the user. |
| Type | ElementType | None | 1..1 | None |  |
| Attributes | ElementAttribute | Composite | 0..* | None |  |
| Behaviours | ElementBehaviour | Composite | 0..* | None |  |
| Elements | InnerElement | Composite | 0..* | None |  |
| Query | Query | Shared | 1..1 | None | Reference a previously created query to use. |
| DataSource | Text | None | 0..1 | None | The Data Source in which the entities are computed and/or persisted |

## Operations

| Name | Type | Description |
| --------- | --------- | --------- |
| Defaults | Initialize |  |

