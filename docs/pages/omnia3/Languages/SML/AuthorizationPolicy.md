---
title: OMNIA 3
keywords: omnia3
summary: "OMNIA 3 SMLAuthorizationPolicy"
sidebar: omnia3_sidebar
permalink: omnia3_languages_SMLAuthorizationPolicy.html
folder: omnia3
---

# AuthorizationPolicy
Authorization Policy is a group of Permissions for that are required in a given context.
## Properties

| Name | Type | Aggregation Kind | Multiplicity | Length | Description |
| --------- | --------- | --------- | --------- | --------- | --------- |
| Name | Text | None | 1..1 | None | The name of the policy (unique identifier). |
| Description | Text | None | 0..1 | None | The textual explanation of the policy purpose. |
| Permissions | AuthorizationPolicyPermission | Composite | 0..* | None | List of permissions. |
| Policies | AuthorizationPolicy | Composite | 0..* | None | Child authorization policies. |


