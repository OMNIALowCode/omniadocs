---
title: Text Templates
keywords: lowcode html css web application
summary: "Everything you need to know about our Text Templates feature and how it allows you can build reusable, custom HTML/CSS elements for your web applications."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_texttemplates.html
folder: omnia3
---

## 1. Introduction

OMNIA Platform enables you to model Text Templates that can be rendered using a Templating Language.

These templates can be useful in case you need a way of formatting the data shown to a user. E.g. to send a notification or to present some information without using Form attributes.

OMNIA Text Templates are based on the [Liquid Templating Language](https://shopify.github.io/liquid/){:target="\_blank"}.


## 2. Model Text Templates
Each text template contains an expression, that will be transformed using the parameters, in order to get the result text.

### How to add a new Text Template?
By accessing **_User Interface / Text Templates_** in the sidebar, you will have access to the text templates management screen.

Selecting the option _Add new_ in the list of text templates, you need to fill the following information:
* **Name**: the name of the text template (needs to be unique within the model);
* **Description**: the textual explanation of the text template's purpose (can be used as development documentation).

### How to update the Text Template's expression?
By accessing **_User Interface / Text Templates_** in the sidebar, select one of the text templates of the list.

In the **_Text Template_** page will you have five different sections:
* **Template**: The place to write the Text Template's expression, using the [Liquid Templating Language](https://shopify.github.io/liquid/){:target="\_blank"};
* **Test parameters**: A JSON representation of test data, using the [available parameters](#which-are-the-available-parameters), in order to preview the template's result;
* **Language Texts**: A JSON representation of the current user language texts;
* **Assets**: A JSON representation of the assets available on the model;
* **Result preview**: The result of the template transformation using the test parameters.

### Which are the available parameters?
The following parameters are available to use when writing a text template:
* **Data**: A set of key-value pair entries, that can be sent in the request body;
* **Context**: A representation of the request context (similar to what is used in the C# and Javascript behaviours);
* **Texts**: The set of texts of the language in which the request was made. Example: `Texts.Hello` to use the text "Hello" from the current user language.
* **Assets**: The set of assets available on the current Model. Example: `Assets.CompanyLogo` to use previously defined asset "CompanyLogo"

## 3. Using Text Templates
Text templates can be used in all scenarios where a text content is required, based on different data and/or language (for example, in the body of an e-mail notification). 

### How to render a Text Template in a Behaviour?
Our platform's API provides a specific endpoint for Text Template rendering inside Behaviours.

In the following sample, a template called "MyTemplate" is transformed using an entity's DTO as parameter.

```C# 
var httpClient = _Context.CreateApplicationHttpClient();
 
var requestResult = await httpClient.PostAsync("TextTemplates/MyTemplate", this.ToDto());
 
if (!requestResult.IsSuccessStatusCode)
 throw new Exception("It was not possible to transform the text template.");
 
var myTemplateContent = await requestResult.Content.ReadAsStringAsync();
```
