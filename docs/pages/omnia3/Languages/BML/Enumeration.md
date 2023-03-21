---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 BMLEnumeration"
sidebar: omnia3_sidebar
permalink: omnia3_languages_BMLEnumeration.html
folder: omnia3
---

# Enumeration
Representation of a collection of values.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..80 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | 0..1024 | The textual explanation of the entities' purpose. |
| Values | EnumerationValue | Composite | 0..* | None | A collection of entries representing an entry of an enumeration. |


