---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLApplicationMenuEntry"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLApplicationMenuEntry.html
folder: omnia3
---

# ApplicationMenuEntry
Menu entry
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | None | The name of the entity (unique identifier). |
| Label | Text | None | 1..1 | None | Label to display. |
| IsFolder | Boolean | None | 1..1 | None | Folder entry. Group of other Menu entries. |
| Icon | Text | None | 0..1 | None | Icon to present with the entry. |
| Color | Text | None | 0..1 | None | Color related to entry. |
| Action | ApplicationMenuEntryAction | Composite | 0..1 | None | Will define how the system should behave. |
| Entries | ApplicationMenuEntry | Composite | 0..* | None | Child entries. Used in case of folders. |


