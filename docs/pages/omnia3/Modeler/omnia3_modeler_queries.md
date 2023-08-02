---
title: Queries
keywords: data visualization query
summary: "Here's all you need to know regarding the queries in OMNIA Platform."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_queries.html
folder: omnia3
---

## 1. Introduction

**Queries** are the tool provided to modelers by OMNIA Platform to determine the data structure to be exposed to users.

## 2. Queries

**_Query / Queries_**

A **query**, in OMNIA, represents a way to define a series of properties whose values you want to obtain, from an entity or a series of entities. If you have ever worked with a query-based languages such as SQL, you will be familiar with this concept - in fact, the queries we model in OMNIA are later turned into SQL, in the [build](omnia3_modeler_lifecycle) process.

A query is automatically created when an entity is created. This automatic query will obtain a series of system attributes, by default.

### How to create a new query?

Selecting the option _Add new_ in the list of queries, you need to fill the following information:

- **Name**: The name of the query (needs to be unique);
- **Description**: The textual explanation of the query's purpose (can be used as development documentation);
- **Type**: The type of the entity this query targets;

### How to add properties to a query?

Selecting the option _Add new_ when editing a query, you need to fill the following information:

- **Alias**: The Alias of the property, i.e. the name you want to see it show up with;
- **Path**: The Path to that property. If the attribute belongs to the entity, it can be selected. Else:
  - If you want to get properties from a collection inside the entity, use '>', i.e. `OrderLines>_amount`;
  - If you want to get properties from a reference inside the entity, use '.', i.e. `VATSummary._amount`;

### How to create an advanced query?

The platform allows you to write your own query using SQL. This feature enables you to execute your own SQL in over the database.

_The SQL will be used to generate a View in the PostgreSQL database, so the query needs to be compliant with the pgSQL Views syntax._

_Note: The query will be executed with Read Only privileges over the application data of that Tenant._

To do that, edit a query and, in **More options**, select **Show advanced editor** and you will see a text box to write in your SQL statement.

### _Naming conventions_

Each entity you add to the model have a SQL view to allow you to easily access the data. Also, each attribute whose _Maximum number of records_ is more than 1, will have a different SQL view.

So, the name of the SQL views respects the following rules:

- SQL views of entities (the name of the entity with the _vw\__ prefix): **vw_MyEntityName**
- SQL views of attributes with _Maximum number of records_ > 1: **vw_MyEntityName_MyAttributeName**
  - To join this views with the parent entity, you can use the column _identifier_ from both views.

Each SQL view will be composed with as many columns as attributes of the entity. The column name is the same as the attribute name.

### _Examples_

_Get the records from an entity_

```SQL
    SELECT document._code, document._date, document.Customer FROM vw_MyDocument document
```

_Get the records from a collection attribute_

```SQL
    SELECT document._code, lines._resource, lines._amount
    FROM vw_MyDocument document
    JOIN vw_MyDocument_Lines lines on lines.identifier = document.identifier
```

_Get a sum of the value of an attribute_

```SQL
    SELECT document._code, lines._resource, SUM(lines._amount) as total
    FROM vw_MyDocument document
    JOIN vw_MyDocument_Lines lines on lines.identifier = document.identifier
    GROUP BY document._code, lines._resource
```

### _Test changes_

It's possible to test changes to an advanced query by clicking the _Execute_ button.

The test is only available to queries that execute on the local _System_ datasource, and it has two possible results: Error or Success.

When a test executes successfully, the following information is returned:

- Execution Time: The time the query takes to be executed on the database, in milliseconds
- Total response time: The total execution time (in milliseconds), from the moment when the test request is sent to Omnia API until the response is received
- Data: The first 50 records returned by the query execution

When a test executes with error, the following information is returned:

- Message: The error message returned by the query execution
- Hints: Hints to fix the error returned by the database server. E.g. a typo on a column name

_NOTE: Since the query executes on the tenant database schema, it's important to have a model built with all changes that have an impact on the database structure. Important changes include the addition of new Entities and new Attributes_

### _Views Tree_

On the right of the _SQL Query_ there's a sidebar containing all the compiled **view's** of the model and respective **columns** and **types**. You can also **type search** for a view and column identifier.

<p align="center">
  <img src="/images/modeler/ViewsTree.png">
</p>

It's possible to **drag** (hold the mouse click on) each _view_ or _column's_ _name_ and **drop** it (release the mouse click) on the _SQL Query_ on left. There's also an option to generate a `SELECT` script for each _view_. Check each example below:

- When **dropping** a _view_ of an entity named _company_ the following information is returned:

```SQL
    vw_company
```

- When **dropping** a _column_ of an attribute named _sales_ from an entity named _company_ the following information is returned:
  - Notice the `,` in the end of the _column_ drop result. We've added it to ease the sequential addition of _columns_.

```SQL
    vw_company.sales,
```

- When **dropping** the generated `SELECT` script a view _vw_company_ with a column _sales_ and the 3 other **default** _columns_ (`identifier`, `_create_at`, `_updated_at`) the following information is returned:

```SQL
    SELECT
        vw_company.identifier,
        vw_company._created_at,
        vw_company._updated_at,
        vw_company.sales
    FROM vw_company
```

### _Output Structure_

On Advanced Queries, it's possible to define the output structure. This structure can be used later when creating a new list, to define the columns.

To set the query output structure, on the advanced query editor navigate to Columns tab and click on the _Auto-fill_ button:

<p align="center">
  <img src="/images/modeler/Modeler_Query_Autofill.jpg">
</p>

The query will be validated, executed and the structure will be suggested.

<p align="center">
  <img src="/images/modeler/Modeler_Query_Autofill_Result.jpg">
</p>

This suggestion can be edited and new columns can be added manually.

### Filtering data with the current user

You can access a SQL parameter (**@\_username**) with the current username. You can use that to filter data.

```SQL
    SELECT document._code, document._date, document.Customer FROM vw_MyDocument document
    WHERE document.authorUsername = @_username
```

### Filtering data with the user roles

You can access a SQL parameter (**@\_userRoles**) with the roles of the current user.
The parameter has the multiple roles comma separated.
If you want to validate if the user has one specific role, you can use the _user_is_in_role_ function.

```SQL
    SELECT document._code, document._date, document.Customer FROM vw_MyDocument document
    WHERE user_is_in_role(@_userRoles, 'Approver')
```

### Filtering data with the user language

You can access a SQL parameter (**@\_userLanguage**) with the active language of the current user.

### Access to created date and updated date

You can access the created date using _\_created_at_ and updated date using _\_updated_at_.
These columns are only available on root entity views.

### Recommendations

- When joining two views, use the _identifier_ instead of the _\_code_ for performance improvements.

```SQL
    SELECT document._code, lines._resource, lines._amount, employee._name
    FROM vw_MyDocument document
    JOIN vw_MyDocument_Lines lines on lines.identifier = document.identifier
    LEFT JOIN vw_Employee employee on employee.identifier = document.employee
```

- When concatenating columns, the result must be converted to **citext** so that the filters are evaluated in a **case insensitive** way.

```SQL
    SELECT document._code, lines._resource, lines._amount, (employee._code || ' ' || employee._name)::citext employee
    FROM vw_MyDocument document
    JOIN vw_MyDocument_Lines lines on lines.identifier = document.identifier
    LEFT JOIN vw_Employee employee on employee.identifier = document.employee
```