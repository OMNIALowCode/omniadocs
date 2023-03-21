---
title: API Error Codes
keywords: omnia3, api
summary: "OMNIA Platform's API error codes list"
sidebar: omnia3_sidebar
permalink: omnia3_api_errors.html
folder: omnia3
---

The following errors may be returned by the operations of the OMNIA Platform's API.

| Error code | HTTP status code | Error message |
| ---------|------------|------------|
| BehaviourFailed | 400 | Behaviour execution failed. |
| ConnectorBehaviourFailed | 400 | Behaviour execution failed while running in Connector. |
| ConnectorNotFound | 503 | Connector can't be reached. |
| ConnectorTimeout | 503 | Connector didn't respond in the expected time. |
| EntityAlreadyExists | 409 | An entity with the same identifier already exists. |
| EntityHasBeenChanged | 412 | The entity isn't in the expected version. |
| EntityHasNoSensitiveDataToDestroy | 400 | Can't execute the Destroy Sensitive Data operation because there's no Sensitive attributes. |
| EntityNotFound | 404 | Entity can't be found. |
| InternalError | 500 | Internal system error. |
| InvalidInput | 400 | Invalid request input data. |
| TenantNotFound | 404 | Tenant/Environment can't be found. |
| ValidationFailed | 400 | Request validation failed. This error can have details in the "errors" properties. Error descriptions in the section "Validation Failed - Errors" |
| MissingSystemConfiguration | 424 | Missing system configuration. Example: Redis service must configured in your system to be able to restart. |
| InvalidApplicationVersion | 400 | Application has been updated. It won't be possible to save current work and the page must be refreshed. |
| DataNotFound | 404 | Your request has no data to return. Please verify your filters and try again. |
| FileNotFound | 404 | File not found. |


### Validation Failed - Errors

| Error code | Error message |
| ---------|------------|
| CannotBeRemoved | Entity can't be removed. |
| Duplicated | Duplicated element. |
| InvalidIdentifier | Identifier (code or name) with invalid format. |
| LowerLimitNotRespected | Minimal number of elements in collection not respected. |
| NotFound | Entity/Reference cannot be found. |
| RequiredValue | Attribute value is required. |
| TypeMismatch | Attribute value doesn't match the attribute type. |
| UpperLimitNotRespected | Maximum number of elements in collection not respected. |
| CreateRootUnsupported | Cannot create an instance separately, as it is marked as non-root and must be used in the context of another entity. |
| CreateSystemDataSourceUnsupported | It's not possible to add records to 'System' Data Source. |
| ValueCannotBeChanged | Attribute value cannot be changed. |
| InvalidModelConfiguration | Invalid model definition. |
| InvalidTenantConfiguration | Invalid tenant definition. |
| TextMaxLengthMismatch | Value is too long to the defined length of (defined length). |
| StateConfigurationNotFound | The configuration of the current state was not found. |
| CommentNotAccepted | Comments are not allowed based on the current state configuration. |
| ForbidToAddToCollectionBasedOnStateMachineConfiguration |  is not possible to add to collection based on record's current state configuration. |
| ForbidToChangeAttributeValueBasedOnStateMachineConfiguration | It is not possible to change the value of the attribute based on record's current state configuration. |
| ForbidToDeleteFromCollectionBasedOnStateMachineConfiguration | It is not possible to remove from collection based on record's current state configuration. |
| ForbidToSaveBasedOnStateMachineConfiguration | It is not possible to save the record based on its current state configuration. |
| SmtpServerInvalidConfiguration | The SMTP server configuration is invalid. |
| ErrorSendingEmail | It was not possible to send the email. |
