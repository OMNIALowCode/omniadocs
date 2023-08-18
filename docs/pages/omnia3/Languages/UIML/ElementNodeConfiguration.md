---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLElementNodeConfiguration"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLElementNodeConfiguration.html
folder: omnia3
---

# ElementNodeConfiguration
Allow to define a element node configuration
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Type | Text | None | 1..1 | 1..* | The type of the element node. |
| Properties | ElementNodePropertyConfiguration | Composite | 0..* | None | The properties of the element node. |
| Events | ElementNodeEventConfiguration | Composite | 0..* | None | The list of element node events. |
| Methods | ElementNodeMethodConfiguration | Composite | 0..* | None | The list of elementnode methods. |
| IsContainer | Boolean | None | 1..1 | None | Indicates if the element node is a container. |
| AllowedInnerElements | Text | None | 0..* | None | List of inner elements allowed by the element node. |
| AllowedParentElements | Text | None | 0..* | None | List of parents elements allowed by the element node. |
| ClassesStylesDefaultValue | Text | None | 0..1 | None | The default element node classes styles. |


