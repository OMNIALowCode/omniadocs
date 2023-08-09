---
title: Platform Changelog
keywords: omnia3
summary: "OMNIA Platform Changelog"
sidebar: omnia3_sidebar
permalink: omnia3_platformchangelog.html
folder: omnia3
toc: false
---

Visit our [Downloads](/omnia3_downloads.html#platform) page to get the latest version.

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
