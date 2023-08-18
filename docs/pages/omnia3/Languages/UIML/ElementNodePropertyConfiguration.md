---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 UIMLElementNodePropertyConfiguration"
sidebar: omnia3_sidebar
permalink: omnia3_languages_UIMLElementNodePropertyConfiguration.html
folder: omnia3
---

# ElementNodePropertyConfiguration
Allow to define a elementnode property configuration
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Key | Text | None | 1..1 | 1..* | The key of the property (unique identifier). |
| IsRequired | Boolean | None | 0..1 | None | Indicates if the property is required. |
| IsCollection | Boolean | None | 0..1 | None | Indicates if the property value is a collection. |
| DataType | ElementNodePropertyDataType | None | 1..1 | None | The data type of the property. |
| Direction | ElementNodePropertyDirection | None | 1..1 | None | Indicates the property binding direction. |
| DefaultValue | Object | None | 0..1 | None | The default value of the property. |
| Options | ElementNodePropertyComplexOption | Composite | 0..* | None | The list of option of the property when data type is 'ComplexOption'. |
| EntityTypes | Text | None | 0..* | None |  |
| TypeName | Text | None | 0..1 | None | The name of the type when the DataType is an 'object'. |


