---
title: Platform Changelog
keywords: omnia3
summary: "OMNIA Platform Changelog"
sidebar: omnia3_sidebar
permalink: omnia3_platformchangelog.html
folder: omnia3
toc: false
---

## [3.5.310](#3.5.310)

Release Date: 2024-04-16

### Implemented enhancements:

- Health Check: SMTP check now waits 15 seconds for a response from the SMTP server before returning a _Degraded_ state
- Modeling: Language Translations can now be selected when defining a translated attribute

### Issues:

- Unable to recreate a deleted tenant


## [3.5.304](#3.5.304)

Release Date: 2024-04-05

### Implemented enhancements:

- Assets are available to be used on Text Templates
- Features Management: Swagger endpoint can now be disabled 
- Tenants: New Role on Tenants to grant connectors adequate privileges
- Modeling area: Alert modelers if they make a _Build & Deploy_ request with unsaved changes
- UI Modeling: new option to navigate to attribute settings, on the attribute context menu
- State Machines: _Enabled operations/attributes_ feature supported on nested collections
- Calendar
  - Performance improvements when adding multiple events on same request
  - Export events to CSV and ICS

### Issues:

- WebApp: When users logs out in a tab, it doesn't reflect on other tabs
- Forms/Dashboards: vertical scroll is always shown
- Modals: _Close_ button label is not translated
- Modeler: on new Tenants, homepage dashboard data is not loaded until the first build is deployed
- Modeler: If user makes changes using _View Json_ option, it is not alerted of changes pending save when navigating
- Queries are not properly executed if there is an attribute named _User_
- Calendar: dates available on metadata and on _Date Range Change_ behaviour are sensitive to the computer timezone
- Management area:  When user clicks to filter a column but does not insert data, filter is applied but not visible


## [3.5.282](#3.5.282)

Release Date: 2024-03-15

### Implemented enhancements:

- New Primitive attribute type: File
- Open and close Containers on Javascript expressions
- Open and close Grid Details area on Javascript expressions

### Issues:

- UI: When Menu is collapsed, on hover an empty area is shown between the menu and the option description
- UI: Favicon is kept in cache after being replaced
- State Machine: When a state is removed, the history panel breaks on entities that passed through it
- API: An error occurs on create entity requests when the code is sent as _null_
- Role Management: Privileges list is not ordered correctly and records are repeated pages
- Lists: When user clicks to filter a column but does not insert data, filter is applied anyway
- Grids: When editing a grid line on mobile devices, if an attribute visibility is changed it is not reflected on the UI
- Calendar: Records are duplicated when added as a range and then edited
- Languages: If a user has selected a language that is later deleted, the template expression is shown instead of the translated texts

**This version contains breaking changes.**
**Upgrade to OMNIA Connector is required.**
**Compatible with Connectors that use the Connector Protocol Version 3.3**

## [3.5.265](#3.5.265)

Release Date: 2024-02-21

### Implemented enhancements:

- Upgrade to .NET 8 runtime
- [Identity Server: Token lifetime settings are now configurable on Platform Settings area](../Management/omnia3_management_settings.md)

### Issues:

- Management Area: 
  - User is unable to access a tenant when it is added to multiple tenants simultaneously
  - When a Tenant is created as Inactive, user is asked for a Platform Restart
  - Connector Management: Connector cannot be accessed if its APIClient is removed
  - Runtime logs list is not ordered by Modified Date
- Tenant Security: Entity Permissions are not removed when the Entity is deleted
- Text Templates: _where_ condition from Liquid template language is not available
- Mobile devices:
  - Theme selection has no effect
  - Cannot export list as CSV

**This version contains breaking changes.**
**Upgrade to OMNIA Connector is required.**
**Compatible with Connectors that use the Connector Protocol Version 3.2**

## [3.5.260](#3.5.260)

Release Date: 2024-01-12

### Implemented enhancements:

- DataSource: Timeout value for _Application Behaviours_ and _After Saves_ is now configurable
- UI Behaviours: Methods to use Browser storage now accessible on _Context_
- Dashboards:
  - Create new Entities using modals
  - New UI Behaviours: _Create_ and _Refresh_
- Lists:
  - Edit Entities using modals
  - Events can be triggered when clicking on any column
- Forms:
  - New UI Behaviour: _After Save_
  - Page navigation after submit is now configurable
- Calendars:
  - New UI Behaviours: _On Form Open_, _On Form Close_ and _On Event Click_

### Issues:

- Calendar: Scheduler view not working when categories have non-alphanumeric characters

## [3.5.251](#3.5.251)

Release Date: 2024-01-03

### Implemented enhancements:

- Improved performance on queries to OMNIA Database
- Swagger: Reorganize endpoints into logical groups
- Management: Add filters and sorting to _API Clients_, _Connectors_ and _Authentication Providers_ Lists
- Modeling: Set a range of valid values (minimum and/or maximum values) on Integer, Decimal and Date attributes

### Issues:

- Language selector not visible on Tenant and Identity pages

## [3.5.243](#3.5.243)

Release Date: 2023-11-27

### Implemented enhancements:

- Management: Add filters and sorting to Language and Tenant lists
- Identity and Tenant selection pages can be translated to platform languages
- UI: When an Exception is thrown on a Entity Behaviour, the temporary is recovered to its previous state
- Platform Settings: new area to customize the platform Images (Background, Logo and Favicon) and page title

### Issues:

- Remote UI Development option not working
- Select Role/Language lists have multiple options that don't work (sorting, filtering)
- Management: _Open in Application_ button located on Tenants list not visible on mobile devices

## [3.5.233](#3.5.233)

Release Date: 2023-10-27

### Implemented enhancements:

- When there are new platform versions available, users are notified on Management and Modeling areas
- Addition of links to navigate to reference entities on Modeling area lists
- Queries/Lists: New filters on text columns (EndsWith, NotEndsWith, NotEqualTo, StartWith, NotStartsWith)
- Read-only mode on forms: When user has _Read_ privileges only (no _Write_ privilege), the entity is now shown in read-only mode
- Improve User Experience on Calendars:
  - _See all_ label replaced with an icon
  - Mobile devices
    - When a day has events, it is possible to see the list of events on a modal
    - When there are multiple events on a single day, a ellipsis is shown to indicate that there are events not visible
    - On scheduler view, a tooltip is shown when category label is clicked

### Issues:

- UI: Occasionally icons are not loaded correctly
- Error executing a Text Template when there are duplicated translations
- Standardize toasts shown when duplicating a entity on Modeling area
- Unused CRUD privileges are being generated for non-root entities
- On a Dashboard Modeling, if a list does not have a value for _isEditable_ attribute, editable list properties are shown
- Mobile Devices:
  - When creating or editing an entity, the breadcrumb state machine title overlaps the first attribute label
  - On Calendars, the label that contains the visible period changes position according to its size 

**This version contains breaking changes.**
**Upgrade to OMNIA Connector is required.**
**Compatible with Connectors that use the Connector Protocol Version 3.1**

## [3.5.217](#3.5.217)

Release Date: 2023-10-10

### Implemented enhancements:

- Redesign Application Behaviours modeling page
- Duplicate entities on Modeling
  - It is now possible to duplicate Commitments, Events, Queries, Lists, Dashboards, Themes, Text Templates and Pages
- Query Editor: When generating a list automatically, the modeler can now set the new list name
- [Runtime Logs](../Management/omnia3_management_runtime_logs.md) accessible on Management area
- Pages:
  - Improve redirection on Pages generated by a recipe by having the suggested variable value containing the partial path
  - Improve inputs on Pages generated by a recipe, so that the input can easily be replaced by other element

### Issues:

- Modeling: Error on adding a non-root entity with nested collections to another entity
- Modeling: On Advanced Queries, JSON Editor and Preview Editor are not synchronized
- Modeling: Etag error when performing sequential changes to a calendar located on a Dashboard

## [3.5.203](#3.5.203)

Release Date: 2023-09-13

### Implemented enhancements:

- Calendars: Replaced mouse over text with a styled tooltip
- Operation Results: Improve and translate toaster texts
- Modeler: Menu entries are now sorted alphabetically

### Issues:

- Calendar: Switching to another calendar view not working on first attempt
- Javascript files syntax highlight not working on browser console
- Query Modeling: Boolean values are not shown on query result preview

## [3.5.187](#3.5.187)

Release Date: 2023-08-25

### Implemented enhancements:

- New feature: Addition of [Pages](../Modeler/omnia3_modeler_pages.md) concept to the model
- Introduction of the additional modeling concepts, to be used with Pages:
  - [Assets](../Modeler/omnia3_modeler_assets.md)
  - [Components](../Modeler/omnia3_modeler_components.md)
  - [Scripts](../Modeler/omnia3_modeler_scripts_UI.md)
  - [CSS Styles](../Modeler/omnia3_modeler_cssStyles.md)

### Issues:

- On Swagger, the suggested RequestBody for Patch requests is not valid
- Modeler: When external entity is created using API and has Data Behaviours, the expression is replaced with a default value

## [3.5.173](#3.5.173)

Release Date: 2023-07-31

### Implemented enhancements:

- When creating a new Connector, the generated email address is now available on the credentials modal
- Modeling: _Update with JSON_ modal no loger closes when clicking the ESC button

### Issues:

- When editing an entity, URL is case sensitive
- Forgot Password/New User emails are not sent if there are duplicated platform translations
- Removed duplicates from translations

## [3.5.169](#3.5.169)

Release Date: 2023-06-07

### Issues:

- When a list is exported to a CSV, the file is not being downloaded in Macintosh devices
- Columns visible according to the screen size are not being correctly rendered
- Lookups on reference attributes located in collections are returning an error when the entity is accessed using its URL
- Fixed security issues

## [3.5.165](#3.5.165)

Release Date: 2023-03-31

### Implemented enhancements:

- Modeling: Improve _Get Entity_ accelerator to take into account if attributes are required
- Security: Access to Modeling is now controlled in the Management area instead of the Tenant Security area

### Issues:

- Dates are shown on multiple formats
- Error message not clear when entity is destroyed multiple types in a row
- Error on build when a model has an entity named Task
- If ENUS language is deleted from Management area, an error occurs when accessing Modeling, Security or Management area
- Lists: On Modeling area and when a list does not have data, hidden columns still reserve space on header
- Modeling/API: Error when creating a new entity with a Enum attribute
- Modeling: Cannot change an attribute name
