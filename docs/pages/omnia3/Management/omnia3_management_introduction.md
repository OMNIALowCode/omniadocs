---
title: Management
keywords: omnia3
summary: "Summary of the Management area of the platform"
sidebar: omnia3_sidebar
permalink: omnia3_management_introduction.html
folder: omnia3
---

## 1. Introduction

The Management area of the platform is where administrative tasks are performed, such as tenant and security management.

## 2. Tenant Management

A Tenant is the primary organizational level of the platform. You can think of a tenant as an instance of an application for a given company - for example, you might have an AnalogSound_ExpensesManagement and an AnalogSound_Purchases tenant, to separate those two applications. You could also have a CompanyB_ExpensesManagement tenant that represents the same application, but for a different company.

Tenants may be categorized as **production**, in which case they require fiscal information.

A tenant may be set as being on Maintenance Mode. On this mode user access to the tenant is limited.

By accessing **_Tenants_** in the sidebar, you will have access to the tenant management screen.

Here you can **Add new** tenants, manage the existing ones, and reset credentials for the default tenant database user.

### 2.1. Add a new Tenant

To add a new Tenant, we must identify their **Code** (shown in URLs), define a human-readable **Name**, and their production information.

Upon creating a tenant, some security information will automatically be created:

- Three roles, that ensure the proper accesses to Administrators, Connectors and users. Additional details about these roles [here](omnia3_authorizationmanagement.html#roles);
- A policy, with a set of permissions. Additional details about the policy and its permissions [here](omnia3_authorizationmanagement.html#policies);
- Inside the tenant, the default application roles and policies.

### 2.2. Set tenant Maintenance Mode

The _Maintenance Mode_ purpose is to ensure the tenant can be set as inaccessible while maintenance operations are being executed.

Access to a tenant when this mode is active is ensured by the _Maintenance_ permission. By default, users with the Administration[TenantCode] role have access.

Access may be granted to other users. To ensure the access, we suggest the creation of a new Role, that has the _Maintenance_ permission.

Users that do not have access to a tenant on _Maintenance Mode_ will not be able to access. On the tenant selection page, the tenant will be shown but disabled, with a message explaining the reason.

## 3. Roles and Policies

In the management section, it is possible to configure Roles and Policies. For more details on these, please see [the description of how authorization works](omnia3_authorization.html), as well as [the language definitions](omnia3_languages_SML.html).

For users to be able to perform administration operations on a given tenant, they must be in the automatically created Administration[TenantCode] role.

## 4. Connectors

To allow to establish a communication between the OMNIA Platform and a system in another machine, it is required to register a **Connector**.

By accessing **Connectors**, you will have access to the Connectors management screen.

Here you can **Add new** connectors, identifying their Code and Name.

Upon creating a connector, a new API Client and a new User for the connector will be automatically created.

### 4.1. Get the Connector's username

In the **Connectors** list, selecting one of the records will open a new window containing the **Client Username**.

### 4.2. Get the API Client credentials

In the **Connectors** list, selecting one of the records will open a new window containing the required credentials to accessing the OMNIA API: the **Client ID** and the **Client Secret**.
