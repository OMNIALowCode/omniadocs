---
title: Settings
keywords: omnia3
summary: "How to manage Platform's settings"
sidebar: omnia3_sidebar
permalink: omnia3_management_settings.html
folder: omnia3
---


## 1. Introduction

The platform's settings allow the configuration of platform parameters.

After changing a parameter value a **platform restart is required for the operation to take effect**.


## 2. Page Settings

In Page Settings we can control some parameters that impact the platform User Interface, namely:

* **Title**: The text to be shown as the page title. It is usually visible on browser tabs.
* **Background File**: The image to be shown as background on platform pages, such as User Profile pages, Login and Tenant Selection
* **Favicon File**: The image to be used as Favicon Usually visible on browser tabs.
* **Logo File**: The image to be used as Logo. It is applied in the same pages as the Background image.

**_Note: When uploading a image file, its resolution should be adequate for its purpose. We suggest 32x32 for Favicon, 200*130 for Logo and 1920*1024 for Background (size in pixels)_**

## 2. Identity Settings

In Identity Settings we can control Identity Server Parameters, namely:

* **Access Token Lifetime**: The lifetime of an access token (in seconds). The minimum value allowed is 300 seconds.
* **Absolute Refresh Token Lifetime**: Maximum lifetime of the absolute refresh token (in seconds). The minimum allowed value is 300 seconds, and it must be equal or bigger than the access token lifetime.
* **Refresh Token Type**: The type of the refresh token. If set to sliding, the sliding refresh token lifetime must be configured.
* **Sliding Refresh Token Lifetime**: Maximum lifetime of the sliding refresh token (in seconds). The minimum allowed value is 300 seconds, and it must be equal or smaller than the refresh token lifetime.

In addition to the Identity Server settings above, the following WebApp setting can be configured:

* **Inactivity Time**: The maximum number of seconds a user can be idle on OMNIA WebApp before it is automatically signed out. The minimum allowed value is 30 seconds.

**_Note: We suggest reading the [Identity Server 4 documentation](https://identityserver4.readthedocs.io/en/latest/topics/refresh_tokens.html) about Refresh Tokens to learn more about the configuration of these parameters_**
