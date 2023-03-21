---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 SMLAuthorizationPolicyPermission"
sidebar: omnia3_sidebar
permalink: omnia3_languages_SMLAuthorizationPolicyPermission.html
folder: omnia3
---

# AuthorizationPolicyPermission
Permission and the Roles that have that permission.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | None | The name of the permission (unique identifier). |
| Description | Text | None | 0..1 | None | The textual explanation of the permission purpose. |
| Roles | Text | Shared | 0..* | None | List of roles that have the permission. |


