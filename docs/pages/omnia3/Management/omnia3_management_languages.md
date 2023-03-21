---
title: Languages (Management)
keywords: omnia3
summary: "How to manage Platform's languages"
sidebar: omnia3_sidebar
permalink: omnia3_management_languages.html
folder: omnia3
---


## 1. Introduction

The platform's language management allow to change which languages are available.

By default, the language American English is loaded to the platform, when the subscription in created.

The texts of each language will only be used to translate the applications to the end-users. The __Modeler__ and __Management__ areas will be presented always in English.


## 2. Language Management

A language is defined by:
* Name: The unique identifier of the language (e.g.: to American English is ENUS);
* Culture: The language tag (e.g.: to American English is en-US). Use the shortest ISO 639 code to identify the language. Optionally, you can define the region with the ISO 3166-1 code after a dash;
* Default: Boolean that indicates if the current language is the default platform language;
* Description: The description of the language (e.g.: to American English can be English (US));
* Texts: A collection in which entry is composed by a name and a value, representing the identifier of the text and the translation in the language.
 
By accessing **_Languages_** in the sidebar, you will have access to the languages management screen.

Here you can **Add new** languages, identifying their **Name**, **Culture** and **Description**. The new language can also be set as **Default**.

After you create a new language, you will be able to change the language's texts. 

*Notes*: 

* By default, when a new language is created, the American English texts are copied. This way, to translate the applications to a new language is only necessary to change the values of each text;
* When a new language is set as _Default_, the flag must be set as _false_ on the previous default language;
* The emails sent when a new user is created or uses the _Forgot Password_ option are always written on the language selected as default.
