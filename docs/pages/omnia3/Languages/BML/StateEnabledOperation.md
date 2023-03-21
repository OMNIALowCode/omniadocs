---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 BMLStateEnabledOperation"
sidebar: omnia3_sidebar
permalink: omnia3_languages_BMLStateEnabledOperation.html
folder: omnia3
---

# StateEnabledOperation
Operation enabled in a given State.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..32 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | 0..1024 | The textual explanation of the entities' purpose. |
| Path | Text | None | 0..1 | None | Path to the operation to enable. When accessing to a composite collection, use the '.' to navigate. |
| Type | StateEnabledOperationTypeEnum | None | 1..1 | None | The operation type to enable. |


