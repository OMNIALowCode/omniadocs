---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 QMLBinaryQueryFilter"
sidebar: omnia3_sidebar
permalink: omnia3_languages_QMLBinaryQueryFilter.html
folder: omnia3
---

# BinaryQueryFilter
Binary condition that is composed by two logical conditions.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Left | QueryFilter | Composite | 1..1 | None | Left part of the condition. |
| Operator | QueryLogicalOperator | None | 1..1 | None | Logical operator over the left and right condition result. |
| Right | QueryFilter | Composite | 1..1 | None | Right part of the condition. |


