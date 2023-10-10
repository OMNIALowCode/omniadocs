---
title: Runtime Logs
keywords: omnia3
summary: "How to view Runtime Logs"
sidebar: omnia3_sidebar
permalink: omnia3_management_runtime_logs.html
folder: omnia3
---


## 1. Introduction

To ensure you can are in control of what is happening on OMNIA Platform Tenants, you can access the Runtime Logs.

Using this feature you can view the log files to detect errors the users had while using a OMNIA Model.

## 2. View Runtime Logs

By accessing **_Runtime Logs_** in the sidebar, you will have access to a list of log files.

There are two different log files: one for the WebApi, and another for the Behaviours Server. In the WebApi log files are registered all errors that happened on API requests, and on the Behaviours Server log files are registered errors that occurred while executing server-side behaviours.  

This log is limited to a maximum of 10 files for each process (WebApi and Behaviours Server), and to the last 10 days. Each file has a maximum size of 5MB.

## 3. Write to Runtime Logs

As indicated above, errors are automatically registered on logs.

However, you can also add your own logs to these files. Click [here](omnia3_modeler_behaviours.html#9-logging) to see how to write logs on behaviours.

