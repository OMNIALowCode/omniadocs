---
title: Connector Changelog
keywords: omnia3
summary: "OMNIA Connector Changelog"
sidebar: omnia3_sidebar
permalink: omnia3_connectorchangelog.html
folder: omnia3
toc: false
---

Visit our [Downloads](/omnia3_downloads.html#connector) page to get the latest version.

## [3.5.15](#3.5.15)
Release Date: 2025-01-08

### Implemented enhancements:

- Upgraded packages

## [3.5.14](#3.5.14)
Release Date: 2024-03-15

### Implemented enhancements:

- Upgraded packages

**This version contains breaking changes.**
**Upgrade to OMNIA Platform is required.**
**Compatible with Platform versions that use the Connector Protocol Version 3.3**

## [3.5.13](#3.5.13)
Release Date: 2024-02-16

### Implemented enhancements:

- Upgraded packages

**This version contains breaking changes.**
**Upgrade to OMNIA Platform is required.**
**Compatible with Platform versions that use the Connector Protocol Version 3.2**

## [3.5.11](#3.5.11)
Release Date: 2024-01-12

### Implemented enhancements:

- The execution of _Application Behaviours_ and _After Saves_ use the timeout value configured on the data source


## [3.5.10](#3.5.10)
Release Date: 2023-10-27

### Implemented enhancements:

- Upgraded packages to support new filter types

**This version contains breaking changes.**
**Upgrade to OMNIA Platform is required.**
**Compatible with Platform versions that use the Connector Protocol Version 3.1**


## [3.5.8](#3.5.8)
Release Date: 2023-08-22

### Implemented enhancements:

- Conector is now released in x86 (32-bit) and x64 (64-bit) versions

## [3.5.5](#3.5.5)
Release Date: 2023-02-08

### Implemented enhancements:
  - [Max reconnection retry time is now configurable](omnia3_connector_install.html#2-configure-connector)
    - When it is not configured, the default value is 24 hours

### Bugs:
  - When the _OmniaConnectorPath_ environment variable does not exist and is created on connector start, models that depend on it do not compile without a restart
  - When exceptions returned on behaviours are too large, a generic message is shown

