---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 BMLStateTransition"
sidebar: omnia3_sidebar
permalink: omnia3_languages_BMLStateTransition.html
folder: omnia3
---

# StateTransition
Possible transition between two states in a State Machine.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..32 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | 0..1024 | The textual explanation of the entities' purpose. |
| Order | Integer | None | 1..1 | None | The evaluation order of transitions. |
| To | State | Shared | 1..1 | None | Target state when the transition happens. |
| Type | StateTransitionType | None | 1..1 | None | Type of transition. |
| Decision | StateDecision | Shared | 0..1 | None | User Decision that will trigger the transition in case of decision based transitions. |
| Expression | Text | None | 0..1 | None | The C# code that will be executed. |


