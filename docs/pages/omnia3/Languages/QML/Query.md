---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 QMLQuery"
sidebar: omnia3_sidebar
permalink: omnia3_languages_QMLQuery.html
folder: omnia3
---

# Query
Query over a given Data Source.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | None | The name of the entity (unique identifier). |
| Description | Text | None | 0..1 | None | The textual explanation of the entities’ purpose. |
| DataSource | Text | None | 0..1 | None | The Data Source in which the entities are computed and / or persisted. |
| Table | QueryTable | Composite | 1..1 | None | Table to query data. Also used to define the this query is related to the definition stored in this Table. |
| Joins | QueryJoin | Composite | 0..* | None | List of the relations with other tables. |
| Expression | Text | None | 0..1 | None | Query based on expression. Content of the Advanced Query. When the expression has value, the rest of the Query definition will be ignored. |


