---
title: Languages
keywords: webapplicationdevelopment languages lowcode
summary: "All the information on how to make your web apps available in any language you wish."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_languages.html
folder: omnia3
---

## 1. Introduction

The model's language management allow to change which languages are available in the model to the application's end-users.

It's only possible to add a language to the model if the language exists in the platform.
In the **Management** area it's possible to add new languages to the platform ([click here](omnia3_modeler_languagetranslator.html) to see how to do it).

## 2. Language Management

A language is defined by:

- Name: A reference to the Platform's language;
- Description: The description of the language (e.g.: to American English can be English (US)). If not written, the Platform's language's description will be used;
- Texts: A collection in which entry is composed by a name and a value, representing the identifier of the text and the translation in the language.

By accessing **_Languages_** in the sidebar, you will have access to the languages management screen.

Here you can **Add new** languages, identifying their **Name** and **Description**.

After you create a new language ([see how](omnia3_modeler_languagetranslator.html)), you will be able to change the language's texts.

## 2. Regional Preferences

The regional preferences applied on the application _Numeric_ and _Date_ inputs are inferred from the language selected by the user.

If the user does not select any language, the default platform language is used (the default can be changed on **Management** area).

On the following cultures the expected formats are:

| Language/Culture              | Date format | Decimal separator | Decimal separator |
| ----------------------------- | ----------- | ----------------- | ----------------- |
| English (US) / en-US          | M/d/yyyy    | Comma (,)         | Full stop (.)     |
| Portuguese (Portugal) / pt-PT | dd/MM/yyyy  | Blank space       | Comma (,)         |
