---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLVariable"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLVariable.html
folder: omnia3
---

# Variable
Allow to define a variable
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..64 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | None | The textual explanation of the variable purpose. |
| Type | VariableType | Composite | 1..1 | None | The data type: can be a Primitive, an Enumeration or a reference to class. |
| Multiplicity | UiMultiplicity | Composite | 1..1 | None | The representation of the minimum and maximum number of records. |
| InitialValue | Object | None | 0..1 | None | The initial value of the variable |


