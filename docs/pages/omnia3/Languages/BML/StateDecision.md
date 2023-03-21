---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 BMLStateDecision"
sidebar: omnia3_sidebar
permalink: omnia3_languages_BMLStateDecision.html
folder: omnia3
---

# StateDecision
Decision that a user can take to condition a given state machine transition.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..32 | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | 0..1024 | The textual explanation of the entities' purpose. |
| Order | Integer | None | 1..1 | None | Represent the relevance of the decision. Use the Order to sort the decisions. |
| CommentType | StateDecisionCommentType | None | 1..1 | None | Define if a comment is required to take the decision. |


