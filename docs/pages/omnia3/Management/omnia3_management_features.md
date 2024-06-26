---
title: Features
keywords: omnia3
summary: "How to manage Platform's features"
sidebar: omnia3_sidebar
permalink: omnia3_management_features.html
folder: omnia3
---


## 1. Introduction

The platform's feature management allows enabling and disabling some of the platform's features.

After changing a feature state a **platform restart is required for the operation to take effect**.


## 2. Supported Features

The following features are currently available:

* **Swagger**: Swagger documentation page.
    * When disabled, the Swagger page is not available to any user;

* **UserPasswordAuthentication**: Authentication using username and password.
    * When disabled, it will be not possible to login with a username and password. If there isn't any Authentication Provider configured, it will not be possible to authenticate in the platform;
    * Make sure you have an Authentication Provider connected to your accounts before disabling this feature.
