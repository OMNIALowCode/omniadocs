---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 BMLStateBehaviour"
sidebar: omnia3_sidebar
permalink: omnia3_languages_BMLStateBehaviour.html
folder: omnia3
---

# StateBehaviour
Behaviour representing how the entity should behave during a state change.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..32 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | 0..1024 | The textual explanation of the entities' purpose. |
| Type | StateBehaviourTypeEnum | None | 1..1 | None | The execution moment of the behaviour. |
| Expression | Text | None | 1..1 | None | The C# code that will be executed. |


