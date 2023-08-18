---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLComponentsPackageConfiguration"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLComponentsPackageConfiguration.html
folder: omnia3
---

# ComponentsPackageConfiguration
Allow defining a component package configuration.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | 1..64 | The name given to the Component Package when added to the model. |
| PackageName | Text | None | 1..1 | None | The name given to the package by its developer. |
| Version | Text | None | 1..1 | None |  |
| ComponentsPackage | ComponentsPackage | Shared | 0..1 | None |  |
| ContractVersion | Text | None | 1..1 | None |  |
| ToolBoxEntries | ToolBoxEntryConfiguration | Composite | 0..* | None |  |
| Components | ComponentConfiguration | Composite | 0..* | None |  |
| Types | TypeConfiguration | Composite | 0..* | None |  |


