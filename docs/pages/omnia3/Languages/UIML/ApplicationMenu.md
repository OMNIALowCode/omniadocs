---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLApplicationMenu"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLApplicationMenu.html
folder: omnia3
---

# ApplicationMenu
Application Menu. Describe the application navigation structure.
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

## Operations

| Name | Type | Description |
| --------- | --------- | --------- |
| Defaults | Initialize |  |

