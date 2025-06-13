---
title: Authorization Management
keywords: omnia3
summary: "Authorization"
sidebar: omnia3_sidebar
permalink: omnia3_authorizationmanagement.html
folder: omnia3
---

## 1. Introduction

On OMNIA Platform, authorization is managed on two distinct areas, one for the Platform and another for the tenant.

### 1.1 Platform

In the platform authorization area (option **Management / Security**) you can manage all the _Policies_ and _Roles_.

### Roles

By default, OMNIA Platform has one role, named _Administration_. This role cannot be removed and it has, by default, associated the user identified on platform setup as the _Platform Administrator_. Other users can be added to this _Role_.

Additionally, when a tenant is created, three new roles are automatically created:

- Administration[TenantCode]: administration role for the tenant. The user responsible for the tenant creation is automatically added to this role. Users with this role can access the Modeling area.
- Users[TenantCode]: general users role for the tenant. Other tenant users should be added to this role, so that they have access to the tenant.
- Connector[TenantCode]: connector users role for the tenant. The users associated with all Connectors used on the tenant must be associated to this role.

If needed, new Roles can be created to grant a set of policies to a group of users.

### Policies

By default, OMNIA Platform has one policy, named _PlatformSecurity_, that controls the access to the following security permissions:

- Tenants
- Users
- Roles
- Privileges

_Administration_ role has access to all this permissions by default.

When a new tenant is created, a new policy is created whose name is the tenant code with the Tenant suffix (e.g. TenantAnalogSound). These policies have the following permissions:

| Permission  | Description                                                    | Default Roles         |
| ----------- | -------------------------------------------------------------- | --------------------- |
| Application | Grants access to the Application area                          | Administration, Users |
| Model       | Grants access to the Modeling area                             | Administration        |
| Build       | Grants access to download builds                               | Connector             |
| Maintenance | Grants access to the Application area when on Maintenance mode | Administration        |

Since policies and permissions are limited and managed by the platform, they cannot be created manually or removed.

If needed, the permissions above can be granted to other roles.

### Users

User accounts grant access to the OMNIA Platform. By default, OMNIA has one User with the Role of Administration.

You can add new users to the Platform on its Management Area, by adding a new username and its roles.
Existent users can be listed and added/removed from roles.

When a new user is created an email notification is sent to confirm the account. The user must confirm the account by setting its credentials on the 24 hours that follow the email reception. After that period, a password reset request must be made, using the option "Forgot your password" on the Login page.

User passwords must obey the following requirements:

- At least 8 characters long
- One uppercase and one lowercase letter (A-z)
- One special character (e.g. @, #, $)
- One unique character (e.g. a letter that is not repeated within the password)

When logging in, if a user fails to provide the correct password in 10 subsequent attempts, the account will be locked for 30 minutes.

### 1.2 Tenant

In the tenant authorization area (option **Security** on right side of top navbar) you can manage all _Policies_ and _Roles_ inside a tenant. Access to this option is limited by the Platform Roles.

### Roles

By default, every tenant has only one Role, named _Administration_. This role cannot be removed and it has, by default, associated the user responsible for the tenant creation. Other users can be added to this _Role_.

If needed, new Roles can be created to grant a set of policies to a group of users.

### Policies

By default, each tenant has two policies:

- **Application**: controls the access to the modeled entities CRUD operations.
- **Security**: controls the access to the tenant security features (Users, Privileges and Roles);

_Administration_ role has access granted to all this permissions. If new roles are added, access to the permissions can be granted.

Since policies and permissions are limited and managed by the platform, they cannot be created manually or removed.

### Users

By default, each tenant has one user that is automatically associated to the Administration role on the moment the tenant is created.

Other users can be added to the tenant, by introducing the username and defining its roles. Existent users can be listed and added/removed from roles.

When a new user is created, it is automatically associated to the tenant Users[TenantCode] role and receives an email notification to set its credentials.
