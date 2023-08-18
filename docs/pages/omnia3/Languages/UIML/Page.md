---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLPage"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLPage.html
folder: omnia3
---

# Page
Handsome web pages
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Type | ElementType | None | 1..1 | None |  |
| Name | Text | None | 1..1 | 1..32 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | None | Page description. |
| Behaviours | ElementNodeBehaviour | Composite | 0..* | None |  |
| Elements | ElementNode | Composite | 0..* | None |  |
| Styles | Text | None | 0..1 | None | CSS styles. |
| ClassesStyles | UiAttributeValue | Composite | 0..1 | None | CSS classes styles. |
| Variables | Variable | Composite | 0..* | None | A collection of entries that allows to define page variables. |
| UrlParameters | UrlParameter | Composite | 0..* | None | List of expected URL parameters. |
| Scripts | Text | None | 0..1 | None |  |

## Operations

| Name | Type | Description |
| --------- | --------- | --------- |
| Defaults | Initialize |  |

