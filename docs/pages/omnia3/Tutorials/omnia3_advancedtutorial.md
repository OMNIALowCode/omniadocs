---
title: Native and External API Tutorial
keywords: omnia3
summary: "Learn all about native and external API communications, queries, lists and dashboards"
sidebar: omnia3_sidebar
permalink: omnia3_advancedtutorial.html
folder: omnia3
---

## 1. Introduction

Now that you have completed our [beginner tutorial](omnia3_beginnertutorial.html), whose result is a functional order management application, we'll now focus on advanced behaviour modeling, using native and external APIs, and an introduction to data analysis elements **Lists**, **Queries** and **Dashboards**.

In **3. Advanced Behaviours** area, we will explore how to communicate with **OMNIA's native API**, in order to improve the user experience, and an **External API**. As a external API, [Discogs](https://www.discogs.com/developers/){:target="\_blank"} was chosen for this example.

In point **4. Data analysis**, we will explore how to model new lists and how to create dashboards on OMNIA.

## 2. Prerequisites

This tutorial assumes that you have created a OMNIA tenant and are logged in as a user with modeling privileges to this tenant.

It is necessary to have completed the steps in the [Beginner tutorial](omnia3_beginnertutorial.html), as this tutorial builds upon it.

## 3. Advanced Behaviours

### Native API

1.  Go to the **Modeler** and edit the previously modeled document _PurchaseOrder_. Create a new **Attribute** by clicking the button **_Add new / Primitive_** on the top right side, and setting its **Name** and **Type** to **SupplierName** and **_Text_**, respectively. Set the attribute as **Read Only**.

     <p align="center">
        <img src="/images/tutorials/advanced/native-api-add-attribute.jpg">
    </p>

2.  Create a new **_Action Behaviour_** to fill the new attribute (on the _PurchaseOrder_ document, go to tab **Entity Behaviours** and click on **_Add new / (Action / Change)_**). Now let's use one of our development "Accelerators" to get our **_SupplierName_** from the **Agents** attribute "**\_name**". Set its name **GetSupplierName**, and **Supplier** as the attribute that triggers the behaviour:

    <p align="center">
        <img src="/images/tutorials/advanced/accelerators-selection.jpg">
    </p>

    <p align="center">
        <img src="/images/tutorials/advanced/accelerators-getEntity-example.jpg">
    </p>

    The output of the **_Get Entity C#_** accelerator should be as follow:

    ```C#
    // Code generated by an accelerator (you can change it if you need)
    // The following code invokes the API to retrieve the data of an entity and set the values in the current entity
    if(string.IsNullOrEmpty(this.Supplier?.ToString()))
       return;
    // In order to prevent to invoke the API if the values were sent by the user
    if(
       this._Dto.HasPropertyChanged(nameof(this.SupplierName))
    )
       return;

    var httpClient = this._Context.CreateApplicationHttpClient();
    var dataSource = "Default";

    var requestResult = httpClient.GetAsync($"Supplier/{dataSource}/{this.Supplier}").GetAwaiter().GetResult();

    if (!requestResult.IsSuccessStatusCode)
       throw new Exception($"Can't retrieve the entity '{this.Supplier}'");

    var entity = requestResult.Content.ReadAsAsync<SupplierDto>().GetAwaiter().GetResult();

    this.SupplierName = entity._name;
    ```

3.  Build & Deploy model

4.  Go to **Application** area, and create a new **PurchaseOrder** document. Observe that, when **Supplier** is identified, the **SupplierName** is automatically retrieved.

### External API

1. Go to the **Modeler** and click on option **Business / Data sources / System** to add references to this data source. Click on button **Add new > File Dependency** to add a new **Behaviour Dependency** for .NET assembly System.Net.Http

<p align="center">
    <img src="/images/tutorials/advanced/Modeler-Add-Behaviour-Dependency.jpg">
</p>

2. Edit the previously modeled resource _Product_. Create a new **Attribute** by clicking the button **Add new / Primitive** on the top right side, and setting its **Name** and **Type** to **Artist** and **_Text_**, respectively. Set the attribute as **Read Only**.

3. Navigate to tab **Behaviour Namespaces** and add namespace System.Net.Http

<p align="center">
    <img src="/images/tutorials/advanced/Modeler-Add-Behaviour-Namespace.jpg">
</p>

4. Create a new **Action Behaviour** to fill the new attribute (go to tab **_Entity Behaviours_** and click on **_Add new / Action_**). Set **_GetRecordData_** as **Name**, **_\_code_** as the attribute that triggers the behaviour, and paste the following code:

   ```C#
   var client = new HttpClient() {DefaultRequestHeaders = {}};
   client.DefaultRequestHeaders.Add("User-Agent", "OMNIA");

   string apiEndpoint = $"https://api.discogs.com/masters/{_code}";
   var requestResult = client.GetAsync(apiEndpoint).GetAwaiter().GetResult();

   string responseBody = requestResult.Content.ReadAsStringAsync().GetAwaiter().GetResult();

   Dictionary<string, object> responseDictionary = JsonConvert.DeserializeObject<Dictionary<string, object>>(responseBody);

   if (!requestResult.IsSuccessStatusCode)
      throw new Exception($"Error on retrieving data from Discogs API: {responseDictionary["message"].ToString()} {apiEndpoint}");

   _name = responseDictionary["title"].ToString();

   if (responseDictionary.ContainsKey("artists")) {
       Newtonsoft.Json.Linq.JArray artists = (Newtonsoft.Json.Linq.JArray)responseDictionary["artists"];

       if (artists != null && artists.Count > 0) {
           Artist = artists[0]["name"].ToString();
       }
   }
   ```

5. Build & Deploy model

6. Go to **Application** area, and create a new **Product** resource. Observe that, when **Code** is identified (e.g. try with value 8540), the **Name** and **Artist** is automatically retrieved.

<p align="center">
    <img src="/images/tutorials/advanced/Application-Create-Product.jpg">
</p>

## 4. Data Analysis

### Queries and Lists

1. On your **Modeler** area, go to **_Query / Queries_** and click on button **_Add New_** to create a new query. Set **ProductsArtists_Query** as _Name_ and **_Resource / Product_** as _Type_.

<p align="center">
    <img src="/images/tutorials/advanced/Modeler-Create-Query.jpg">
</p>

2. Now open your query and click on **Add New** to add columns to it. Add a column with Alias **Code** and Path **\_code**.
3. Repeat previous step to add columns with alias **Name** and **Artist**, whose Path is **\_name** and **artist**, respectively.

4. On top right side, click on button **_More options / Generate list_** to create a new list based on the given query.

<p align="center">
    <img src="/images/tutorials/advanced/Modeler-Generate-List.jpg">
</p>

### Dashboards

1. On your **Modeler** area, go to **_User Interface / Dashboards_** and click on button **Add New** to create a new dashboard. Set **Home** as Name, so that the dashboard is visible on application's homepage.

<p align="center">
    <img src="/images/tutorials/advanced/Modeler-Create-Dashboard.jpg">
</p>

2. On the right sidebar select the third tab, identifiable by the **+** sign, and then select the first tab below. Verify there is a **ProductsArtists_QueryList** option listed. Press and hold down the list then drop it into the **Home** Dashboard.

<p align="center">
    <img src="/images/tutorials/advanced/Modeler-Drag-List-Dashboard.jpg">
</p>

3. Click on the list and change its Label to **Products List** and Size to **6**. Don't forget to save your changes.

<p align="center">
    <img src="/images/tutorials/advanced/Modeler-Resize-List-Dashboard.jpg">
</p>

4. **Build & Deploy** the model.

5. Go to the application and check the homepage dashboard. Data for the products you have created will be visible.
