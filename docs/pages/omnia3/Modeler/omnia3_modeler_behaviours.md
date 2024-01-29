---
title: Behaviours
keywords: low code web application development C# JS behaviours
summary: "All you need to know regarding C# and JS behaviours and how they'll enhance your web application development."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_behaviours.html
folder: omnia3
---

## 1. Introduction

In the **OMNIA Platform**, the primary way to customize the way the application works is by using Behaviours.

Behaviours are code that allow you to **extend** the way the application processes user input.

There are three kinds of business logic behaviours, that are applied at an API level (i.e. whether you use the OMNIA platform directly via its API or via our web app), all written in C#:

- **entity behaviours**, which extend the behaviour of the instances of that entity (for example, default values or specific validations);
- **data behaviours**, which only exist for entities with an external data source, and replace the platform's create/read/update/delete (CRUD) code with user-written code to perform those operations on the external data source;
- **application behaviours**, which are similar to methods in object-oriented programming, and are used in the other behaviours.

This document explains the Entity behaviours (here normally mentioned as 'behaviours' only) and application behaviours; for more information on data behaviours please see [this page](omnia3_modeler_datasources.html).

There are also user interface-specific behaviours, which have a similar logic to C# behaviours. They are written in JavaScript, and are described in [this page](omnia3_modeler_uibehaviours.html).

A behaviour is defined by:

- its **type**, or the moment in which it will execute;
- (optionally) its **attribute**, or which attribute of the model it is dependent on;
- its **expression**, the aforementioned C# code.

Behaviours are executed by the API of the platform - creating, updating or saving an entity will execute the appropriate behaviours.

![The behaviours' execution path](images\modeler\BehavioursCommunication.png)

During the behaviour lifecycle, the platform stores the current state of the document in a cache, allowing for fast response times.

## 2. Types of Behaviours

There are currently six different execution moments for behaviours, which follow a logical flow:

- **Initialize**: Executes when an entity is initiated in the behaviour engine to perform an update or create;
- **Before Change**: Executes immediately before an update is received for that entity;
- **Formula**: Executes during updates, requires an attribute, and **calculates** the value of that attribute. Must return a value of the correct type;
- **Action/Change**: Executes during updates, requires an attribute, and, given the new and old values of that attribute, performs an operation;
- **After Change**: Executes immediately after the update with the user's changes is done;
- **Before Save**: Executes when an entity is saved.

Other than these, there are two special entity behaviours:

- **Before Collection Entity Initialize**: Executes when a new entity is added to a collection, before its **Initialize** behaviour;

  - **_Example of usage_**: Allocate the value of a Parent's _(this)_ property to a collection's Child _(entry)_ property:

    ```
    entry.company = this.name;
    ```

  - **_Observations_**:

    1. When it's intended to change a collection's Child _(entry)_ property depending on a Parent's _(this)_ property, it's important to keep using **Action/Change Behaviours**;
    2. Since it's possible to have [3 levels of Nested Collection between entities](omnia3_modeler_entities.html#how-many-levels-is-possible-to-have), it's important to understand that Parent _(this)_ and Child _(entry)_ change depending on the level.

- **After Save**: Executes after an entity is saved, asynchronously, by being put in an **outbox** and processed separately.

  After Save behaviours are _async_, and have a custom return type, which will be used like:

  ```csharp
  return new AfterSaveMessage("Integration was successful, but could not send email to all users. Please check if their emails are valid.", AfterSaveMessageType.Warning);
  ```

  There are two helpers in AfterSaveMessage, _.Empty_ and _.Default_, which you should use when you aren't interested in the contents of the message. Empty shows no notification; default shows a success notification/operation.

  Valid AfterSaveMessageTypes are **Information**, **Success**, **Warning**, **Error** and **SuccessNoNotification**. _Error_ will mark the after save as having failed, _SuccessNoNotification_ sends no notification to the end-user, while the other three are used only to customize the look of the notification they send.

  **Note**: After Save behaviours are not called immediately after saving, but go into a queue. More information [here](omnia3_application_notifications_and_operations.html). _**No changes to the status of the entity will be saved! If you want to change an entity on an After Save, you must do it via our API.**_

![The behaviour execution lifecycle](images\modeler\BehaviourLifecycle.png)

### 2.1. C# method naming

| Type                                | Method                                   | Observations  |
|-------------------------------------|------------------------------------------|---------------|
| Initialize                          | OnInitialize                             |               |
| Before Change                       | OnBeforeUpdate                           |               |
| Formula                             | Get{ATTRIBUTE NAME}                      |               |
| Action/Change                       | On{ATTRIBUTE NAME}PropertyChange         |               |
| After Change                        | OnAfterUpdate                            |               |
| Before Save                         | OnBeforeSave                             |               |
| After Save                          | OnAfterSave                              | Async method. |
| Before Collection Entity Initialize | OnBefore{ATTRIBUTE NAME}EntityInitialize |               |

## 3. Usage

There are many possible usage scenarios for these behaviours, as C# coding will allow you to execute whatever you want. This section gives some guiding examples.

### 3.1. Usage of the behaviours in the platform languages

Internally, in the development of the platform, these behaviours are used with the same structure. For example, when you create an Agent, you will see that, even though you didn't specify any attributes, a set of default attributes are present. This creation is handled by an **Initialize** behaviour. They also can't be deleted; this is ensured by having a **Before Save** behaviour that ensures that an exception is thrown if the user attempts to remove any _system_ attribute.

A similar **Initialize** logic is used to ensure default values in documents: for example, the initial date is set to today's date instead of 01/01/0001, the C# default for that date.

### 3.2. Usage Scenarios

Following from the scenarios described in 3.1., you may have realized some possible scenarios that behaviours can help in. Our [tutorials](omnia3_beginnertutorial.html) also have a series of different examples.

Here are some usage suggestions for each type of behaviour - though, of course, the only limit is your imagination!

- **Initialize**:
  - Default values for fields;
- **Before Collection Entity Initialize**:
  - Set Parent values on fields located on a collection;
- **Before Change**:
  - Performing operations that depend on the previous state of the document;
- **Formula**:
  - Summary/total fields;
  - Auxiliary fields (i.e. displaying an amount of days based on two dates);
- **Action**:
  - Looking up data from an external API;
  - Changing information in the lines of a grid based on a change in the header;
  - Performing validations on an attribute;
- **After Change**:
  - Performing calculations that require information from commitments/events in the header;
  - Performing document-wide validations;
  - Calculating summary lines;
- **Before Save**:
  - Performing final document-wide validations;
  - Integrating with external APIs;
- **After Save**:
  - Performing integrations with external systems that depend on the OMNIA-side document already being saved.
  - Triggering e-mail notifications.

Keep in mind that all OMNIA entities are independent, and therefore an entity behaviour should not depend on another entity.
As an example, a Commitment behaviour code should not be dependent of a specific Document, because a Commitment can be available on more than one Document. On these scenarios, the behaviour should be defined on the Document.

## 3.3 How to know if an Attribute has been changed?

If you want to validate if a property/attribute has been changed by the user, for example, if you want to ensure that a given attribute can't be changed by a given user, you can do one of two things.

1. Validate if one property has changed:

To do that, use the method `bool HasPropertyChanged(string propertyName)` from the DTO.

Example:

```c#
if(_Dto.HasPropertyChanged("State"))
    throw new Exception("State can't be changed");
```

2. Use the list of changed properties:

The DTO has a collection of changed properties `IReadOnlyCollection<string> _ChangedProperties`.

Example:

```c#
if(this.State == 'COMPLETED' && _Dto._ChangedProperties.Count>0)
    throw new Exception("Changes can't be done in a completed document.");
```

The `HasPropertyChanged` method validates if a given attribute is in the list of `_ChangedProperties`. The `_ChangedProperties` list contains all those properties for which the user sent a value in a given interaction. If the user changes the attribute _"A"_ and attribute _"B"_ in two different steps, you will never see both _"A"_ and _"B"_ at the same time in the list. For that reason, the `_ChangedProperties` is empty in _AfterSave_ behaviours.

## 4. Referencing external libraries in Behaviours

The way to use references to .NET assemblies is explained in a [separate article](omnia3_modeler_dependencies.html), as it is shared for both Entity and Data Behaviours.

## 5. Application Behaviours

Application behaviours are created in the Modeler's **Extensibility** area. Their main difference compared to the other behaviours is that they are available on a per-data source basis; i.e. instead of picking an Attribute and Type, you define the data source where it will be available.

Every system that has application behaviours will have them under the base namespace of that tenant, for example, `Omnia.Behaviours.Tenant001.Application`, with a partial class logic: every application behaviour is in its own file, but they are all in the same class. If you want to use an application behaviour with the code `ValidateAPIAccess` in the **System** data source's **Initialize** behaviour, you will do so by writing `SystemApplicationBehaviours.ValidateAPIAccessAsync()` in your code.

The application behaviours are `static`. They all receive an (optional) `IDictionary<string,object> args`, which can be used to send any necessary information when calling them from other places, and also must return a dictionary.

## 6. User value preservation

Setting the value of a Domain entity attribute will be ignored in case the User/Client has sent to the API a change to that specific property in the current request. This is being done to make sure that the in integration scenarios, for example, the user intent is respected.

In case you want to force an attribute to change, you can do it in the **Before Save** moment.

## 7. Invoking the OMNIA API

To facilitate an API invocation, you have some methods in the context to setup the [HTTP Client](https://docs.microsoft.com/en-us/dotnet/api/system.net.http.httpclient?redirectedfrom=MSDN&view=netframework-4.7.2){:target="\_blank"} with the required Headers and Tokens.

Methods:

- **CreateApplicationHttpClient:** Create an HttpClient to invoke the API for the Application area of the current Tenant.
- **CreateModelHttpClient:** Create an HttpClient to invoke the API for the Model area of the current Tenant.
- **CreateSecurityHttpClient:** Create an HttpClient to invoke the API for the Tenant Security area of the current Tenant.
- **CreateManagementHttpClient:** Create an HttpClient to invoke the API for the platform management area.

```C#
var httpClient = this._Context.CreateApplicationHttpClient();
```

## 8. Caching in behaviours

A cache can improve the performance of an OMNIA application, especially when your application is loading data from other systems.

Depending on the setup of your OMNIA subscription, your cache can be at: 
- Redis: distributed cache that is shared by multiple app servers and survives server restarts and app deployments. 
- Memory: local memory of the server.

If the "RedisConnectionString" is defined in the subscription config, you will be using the Redis Cache.

### Accessing to cache

To access the cache, you have a method in the _Context_ to create a cache client.

The cache client exposes 3 methods:

1.  **SetAsync:** Set a key with a value of any object type;
1.  **GetAsync:** Get an entry of a given object type from the cache;
1.  **RemoveAsync:** Remove a key from the cache.

Example:

```
// Create cache client
var cache = _Context.CreateCacheClient();

// Write data to cache
await cache.SetAsync("MyKeyName", "Hello!");

// Read data from cache
var value = await cache.GetAsync<string>("MyKeyName");

// Remove data from cache
await cache.RemoveAsync("MyKeyName");

```

### Notes:

- All the keys in Cache have a 24 hours lifetime after the last access to the key.

## 9. Logging

You can access the behaviour server logger using:

```C#
var logger = _Context.Services.GetService<ILogger<Customer>>();

logger.LogInformation("My first log entry!");
```

_Replace "Customer" by the name of your Class._

To use ILogger register the namespace `Microsoft.Extensions.Logging`.

## 10. .NET Versions

The compiled C# code, targets the following platforms:

- **Behaviours that are executed in Connector:** Framework .net 4.7.2
- **Behaviours that are executed in OMNIA:** Framework .net standard 2.0

## 11. Developing and testing behaviours

The way to develop and test behaviours is explained in a [separate article](omnia3_modeler_developingbehaviours.html), as it is shared for both Entity and Data Behaviours.
