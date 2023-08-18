---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLElementNode"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLElementNode.html
folder: omnia3
---

# ElementNode
Element Node
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..128 | The name of the entity (unique identifier). |
| Type | Text | None | 1..1 | None |  |
| Package | Text | None | 0..1 | None |  |
| Attributes | UiAttribute | Composite | 0..* | None |  |
| Behaviours | ElementNodeBehaviour | Composite | 0..* | None |  |
| ClassesStyles | UiAttributeValue | Composite | 1..1 | None | CSS classes styles |
| CSSStyle | UiAttributeValue | Composite | 1..1 | None | CSS style |
| IsHidden | UiAttributeValue | Composite | 1..1 | None | The visibility of the element (hidden or visible). |
| GroupElements | Boolean | None | 1..1 | None | Specify if the element group inner elements |
| Elements | ElementNode | Composite | 0..* | None |  |


