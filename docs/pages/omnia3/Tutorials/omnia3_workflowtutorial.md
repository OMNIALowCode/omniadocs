---
title: OMNIA 3.0 Workflow Tutorial
keywords: omnia3
summary: "OMNIA Workflow Tutorial"
sidebar: omnia3_sidebar
permalink: omnia3_workflowtutorial.html
folder: omnia3
---

## 1. Introduction

OMNIA's Worflow Tutorial enhances your experience on OMNIA Platform 3.0, combining advanced elements and features from previous Tutorials with your daily workflow tools.

## 2. Prerequisites

This tutorial assumes that you have created a OMNIA tenant, and are logged in as a user with modeling privileges to this tenant.

## 3. Modeling a Workflow apllication

1. Start by selecting the tenant where you are going to model, and you will be redirected to the modeling area.

   ![Homepage_Dashboard](/images/tutorials/beginner/Modeler-Homepage.PNG)

2. Create a new **Agent**, and set its _Code_ to **Company**.
3. Return to **_Agents / Add new_**, and set its _Code_ as **Employee**.

   ![Modeler_Create_Agent](/images/tutorials/workflowtutorial/Modeler-Agent-Employee.PNG)

4. Create a new **Resource**, and set its _Code_ to **Task**.
5. Access the option **_Versioning / Builds / Create new_**.

6. Proceed to the Application area, configure all figures previously defined, by selecting the option **_Configurations / Company / Create new_**, and defining its _Code_ and _Name_.

7. Follow the same process of the previous step to create a new **Employee** and **Task**.

8. Go back to Modeling area and create a new **Event** with _Code_ set as **Executedtask**, **Task** as the _resource_ to be exchanged, **Employee** as provider agent, and **Company** as receiver agent.

   ![Event_Executed task](/images/tutorials/workflowtutorial/Event-TaskList.PNG)

9. Add a new **Generic Entity**, and set the code as _Project_.

10. Create a new **Document**, naming it as **TaskReport**.

11. Go to **_Data Analytics / Queries_** and create a query for your Event. Name it **Executedtask_Query**. Add a single property with alias **Code** for the path **\_code**.

12. Access **_Data Analytics / Lists_** and create a new list. Set **Executedtask_List** as _Code_, the query created on first step (**ExecutedtaskQuery**) as the _source_ of the list and **Task** as _Label_.

    ![Task List Query](/images/tutorials/workflowtutorial/Queries-List-Executedtask.PNG)

13. Add new columns to **List**. Add a column for Query Property _Code_, with Label _Task_, and format as _Text_

    ![Task List Query](/images/tutorials/workflowtutorial/Code-QueryList.PNG)

14. On **_Data Analytics / Dashboards_**, create a new dashboard and set **Home** as _Code_, so the dashboard will be visible on application’s homepage.

    ![Modeler_Create_Dashboard](/images/tutorials/workflowtutorial//Modeler-Create-Dashboard.PNG)

15. Add lists to **Dashboard**. Set **Executedtask** as _Code_, its List as **Executedtask_List** (created previously) and position it in the first Row and Column, with Size six. Set its label as **Executed Tasks**.

16. Perform a new Build (by accessing the option **_Versioning / Builds / Create new_**). Access the application and verify the homepage dashboard shows up.

17. Go back to the modeler and edit the **TaskReport** Document, by accessing **_Documents / TaskReport_**.

    - Add an new Attribute to your Document. Set its _Code_ as **Project**, _Type_ as **_Generic Entity / Project_**.

    - Add a new Attribute to your Document. Set its _Code_ as **Company**, _Type_ as **_Agent / Company_** , and as required by checking option _Is required?_.

    - Add a new Attribute to your Document. Set its _Code_ as **Employee**, Type as **_Agent / Employee_**, and as required by checking option _Is required?_.

    - Add a new Attribute to your Document. Set its _Code_ as **EmployeeName**, Type as **_Primitive / Text_**, and as read-only by checking option _Is Read Only?_.

    - Add a new Attribute to your Document. Set its _Code_ as **SheetID**, Type as **_Primitive / Text_**, and as read-only by checking option _Is Read Only?_.

    - Add a new Attribute to your Document. Set its _Code_ as **ReportLines** and Type as **_Event / ExecutedTask_**.

    ![Modeler_Create_Dashboard](/images/tutorials/workflowtutorial/Attribute-EmployeeName.PNG)

18. Go back to **Generic Entity**, and add a new **Attribute** to **Project**. Set its _Code_ as **_SheetID_**, and its type as **_Primitive / Text_**.

19. Go to **Events**, and add a new **Attribute** to **Executedtask**. Set its _Code_ as _TaskDate_, and its type as **_Primitive / Date_**.

20. Add another **Attribute** to **Executedtask**, setting its _Code_ as **_Description_**, and its type as **_ Primitive / Text_**.

21. Go to **Google Sheets** and create a new file. [Generate an API key to access it](https://developers.google.com/sheets/api/guides/authorizing). Make a note of the file's ID, which you can obtain from the URL; for example, for the URL https://docs.google.com/spreadsheets/d/omniaID1234/edit#gid=0, the ID would be **omniaID1234**.

Copy the data from [this file](/images/tutorials/workflowtutorial/Task-Project-01.xlsx) to the sheet you just created.

23. In the **TaskReport** document, go to tab _Behaviours_ and click on **_Add new / Action_**. Set **GetReportData** as _Code_, **SheetID** as the attribute that triggers the behaviour, and paste the following code, taking care to replace the "INSERT YOUR KEY HERE" with the key obtained in the last step:

    ```
    if (!string.IsNullOrEmpty(SheetID))
    {
        var client = new System.Net.Http.HttpClient()
        {};
        string googleApiKey = "INSERT YOUR KEY HERE";
        string apiEndpoint = $"https://sheets.googleapis.com/v4/spreadsheets/{SheetID}/values/Sheet1?key={googleApiKey}";
        var requestResult = client.GetAsync(apiEndpoint).GetAwaiter().GetResult();
        string responseBody = requestResult.Content.ReadAsStringAsync().GetAwaiter().GetResult();
        if (!requestResult.IsSuccessStatusCode)
            throw new Exception("Error on retrieving Google sheet: " + responseBody);
        var sheet = JsonConvert.DeserializeObject<Dictionary<string, object>>(responseBody);
        var values = JsonConvert.DeserializeObject<List<List<string>>>(sheet["values"].ToString());

        for (int i = 2; i < values.Count; i++) //first two lines are headers
        {
            ExecutedTask taskLine = new ExecutedTask(_context, null);
            taskLine._resource = values[i].ElementAt(0);
            taskLine.TaskDate = Convert.ToDateTime(values[i].ElementAt(1));
            taskLine.Description = values[i].ElementAt(2);
            taskLine._quantity = Convert.ToInt32(values[i].ElementAt(3));
            ReportLines.Add(taskLine);
        }
    }
    ```

24. In the **TaskReport** document, go to tab _Behaviours_ and click on **_Add new / Action_**. Set **GetSheetID** as _Code_, **Project** as the attribute that triggers the behaviour, and paste the following code:

    ```
    var project = ApiClient.Get(this.Context, "Project", newValue);
    SheetID = project["sheetID"].ToString();
    ```

25. In the **TaskReport** document, go to tab _Behaviours_ and click on **_Add new / Action_**. Set **GetEmployeeName** as _Code_, **Employee** as the attribute that triggers the behaviour, and paste the following code:

    ```
    var employee = ApiClient.Get(this.Context, "Employee", newValue);
    EmployeeName = employee["_name"].ToString();
    ```

26. Perform a new Build (by accessing the option **_Versioning / Builds / Create new_**).

27. Go to **_Application / Configurations_** area, and create a new **Project**. Set its **SheetID** attribute to the value we obtained earlier when setting up the Google Sheet.

28. Return to **Application** area, and create a new _Taskreport_ **Document**. If **Project** has an associated and valid **Google Sheet**, your **TaskReport** lines will be automatically loaded.
