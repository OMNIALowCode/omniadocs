---
title: Connector Tutorial
keywords: omnia3
summary: "Create and configure a new connector to use an on-premise CSV File as a data source"
sidebar: omnia3_sidebar
permalink: omnia3_connectortutorial.html
folder: omnia3
---

## 1. Introduction

This tutorial will demonstrate how to add a transportation selection option, whose data will originate from an on-premise .csv, to our pre existing Purchase Order Document. To achieve this connection, a new Connector will be created and properly configured.

The purpose of this example is to simulate a real world scenario, where the option for the user to select the means of transportation of the order he is about to submit will be added as an upgrade to the current application.

This tutorial is an advanced implementation of the [data sources tutorial](omnia3_datasourcetutorial.html). In order to understand how data sources work, please read [this section of the documentation](omnia3_modeler_datasources.html).

For this CRUD Operations tutorial, we are going to show how to interact with an external data source, by reading and manipulating its data.

As our custom data source, we are going to use a CSV file with a list of companies that provide Transportation services.

## 2. Prerequisites

This tutorial assumes that you have created a OMNIA tenant ([click here to see how](omnia3_tenantcreation.html)), and are logged in as a user with modeling privileges to this tenant. You must also have access to the management area to manage the connectors.

Please download this [TransportationServices.csv](/images/tutorials/connector/TransportationServices.csv), we'll be using it as a data source in this tutorial.

## 3. Create a new connector

1. Start by accessing the management area, by clicking the option "Go to Tenants management" on the tenant selection page or, by selecting the "Management" option on the right side of a tenant top bar.

2. Through the left side menu, create a new connector by accessing the option **_Connectors / Add new_**. Set its Code and Name as "CSVConnector".

    Right after creating the connector, a modal with its data should be shown. Copy the **Client Username**, **Client ID** and **Client Secret** to use later when configuring the Connector.

    <p align="center">
        <img src="/images/tutorials/connector/CSVConnector.jpg">
    </p>

3. Now we are going to grant the connector access privileges for the tenant. Access the option **_Security / Roles_**, and select Administration role for the tenant (composed by the tenant code with prefix "Administration". E.g. AdministrationDemoTenant)

4. Click the button **_Add new_** to grant the connector user access to the tenant. The user can be retrieved on step 2, property "Client Username". If you didn't copy the username in that moment, select the connector on the list to access that information. 

5. Now use these configurations to configure a connector on your local machine (or a Windows VM), following the [installation guide](omnia3_connector_install.html) and [configuration guide](omnia3_connector_configuration.html).

6. Start the configured connector.

## 4. CRUD operations

1. Access OMNIA homepage, select the tenant where you are going to model and you will be redirected to the modeling area.

2. Through the left side menu, create a new Data Source by accessing the option **_Business / Data Sources_** then, **_Add new_** (button on the top right side). Set its Name as "_CSVSource_", Behaviour Runtime and Data Access Runtime as _"External"_.

   ![Modeler create DataSource](/images/tutorials/connector/modeler-create-datasource.jpg)

3. Create a new **Agent** with name **_Transportation_**, and set it as using the external data source **_CSVSource_**, created on the previous step.

   ![Modeler create Agent](/images/tutorials/connector/modeler-create-agent.jpg)

4. Navigate to tab _"[Data Behaviours](omnia3_modeler_datasources.html)"_, and define the behaviour code to be executed on _"ReadList"_. This behaviour will be used for Query and List requests for this entity.

    Remember to **change** the variable **`filePath`** and **`csvSplitChar`** with your csv file full path and the character configured as the CSV column delimiter.

    Copy and paste the following code:

    ```C#

    List<IDictionary<string, object>> listData = new List<IDictionary<string, object>>();

    string filePath = @"filePath\TransportationServices.csv";
    char csvSplitChar = ';';

    int numberOfRecords = 0;
    using (var reader = new System.IO.StreamReader(filePath))
    {
    	while (!reader.EndOfStream)
    	{
    		var line = reader.ReadLine();
    		var values = line.Split(csvSplitChar);
    		Dictionary<string, object> transportationData = new Dictionary<string, object>();
    		if (values.Length > 1)
    		{
    			transportationData.Add("_code", values[0]);
    			transportationData.Add("_name", values[1]);
    			numberOfRecords++;
    			listData.Add(transportationData);
    		}
    	}
    }

    return (numberOfRecords, listData);
    ```

5. Set the code for the _"Read"_ **Data Behaviour**, so that data is retrieved when you wish to select a Transportation Service for your order.

    Remember to **change** the variable **`filePath`** and **`csvSplitChar`** with your csv file full path and the character configured as the CSV column delimiter.

    Copy and paste the following code:

    ```C#
    string filePath = @"filePath\TransportationServices.csv";
    char csvSplitChar = ';';

    TransportationDto transportation = new TransportationDto();
    using (var reader = new System.IO.StreamReader(filePath))
    {
    	while (!reader.EndOfStream)
    	{
    		var line = reader.ReadLine();
    		var values = line.Split(csvSplitChar);
    		var valuesLen = values.Length;
    		if (values[0].Equals(identifier, System.StringComparison.InvariantCultureIgnoreCase))
    		{
    			transportation._code = values[0];
    			transportation._name = values[1];
    		}
    	}
    }

    return transportation;
    ```

6. Set the code for the _"Update"_ **Data Behaviour** (when a Transportation Service is updated on OMNIA).

    Remember to **change** the variable **`filePath`** and **`csvSplitChar`** with your csv file full path and the character configured as the CSV column delimiter.

    Copy and paste the following code:

    ```C#
    TransportationDto transportation = new TransportationDto();
    string fileContent = "";
    string filePath = @"filePath\TransportationServices.csv";
    char csvSplitChar = ';';
    string transportationDetails = $"{dto._code}{csvSplitChar}{dto._name}{csvSplitChar}";

    using (var reader = new System.IO.StreamReader(filePath))
    {
    	while (!reader.EndOfStream)
    	{
    		var line = reader.ReadLine();
    		var values = line.Split(csvSplitChar);
    		var valuesLen = values.Length;
    		if (!values[0].Equals(identifier, System.StringComparison.InvariantCultureIgnoreCase))
    			fileContent+= "\n"+line;
    		else
    			fileContent+= "\n"+transportationDetails;
    	}
    }

    System.IO.File.WriteAllText(filePath, fileContent);

    return transportation;
    ```

7. Set the code for the _"Create"_ **Data Behaviour** (when a new Transportation Service is created on OMNIA).

    Remember to **change** the variable **`filePath`** and **`csvSplitChar`** with your csv file full path and the character configured as the CSV column delimiter.

    Copy and paste the following code:

    ```C#
    string filePath = @"filePath\TransportationServices.csv";
    char csvSplitChar = ';';
    string transportationDetails = $"\n{dto._code}{csvSplitChar}{dto._name}{csvSplitChar}";

    if (System.IO.File.Exists(filePath))
    	System.IO.File.AppendAllText(filePath, transportationDetails);

    return dto;
    ```

8. Set the code for the _"Delete"_ **Data Behaviour** (when a Transportation Service is deleted on OMNIA).

    Remember to **change** the variable **`filePath`** and **`csvSplitChar`** with your csv file full path and the character configured as the CSV column delimiter.

    Copy and paste the following code:

    ```C#
    TransportationDto transportation = new TransportationDto();
    string fileContent = "";
    string filePath = @"filePath\TransportationServices.csv";
    char csvSplitChar = ';';

    using (var reader = new System.IO.StreamReader(filePath))
    {
    	while (!reader.EndOfStream)
    	{
    		var line = reader.ReadLine();
    		var values = line.Split(csvSplitChar);
    		var valuesLen = values.Length;
    		if (!values[0].Equals(identifier, System.StringComparison.InvariantCultureIgnoreCase))
    			fileContent+= "\n"+line;
    	}
    }

    System.IO.File.WriteAllText(filePath, fileContent);

    return true;
    ```

9. Build & Deploy model

10. Go to the Application area.

11. Create a new instance of the CSVSource data source, with code _"LOCAL"_ and with the Code of the Connector (CSVConnector) that you have created.

12. On left side menu, navigate to _Configurations / Transportation_, identify the CSVSource data source instance (LOCAL) and check that the list is filled with data retrieved from CSVSource.

13. Now you can list and update your transportation services directly on your on-premise system, providing your connector is correctly configured and running.

## 5. Add Transportation option to Purchase Document

1. Go to your Purchase Order Document and add two new **_Reference_** attributes:
   1.1 One reference to which (transportation) list we are going to read from:

   - Name: "**TransportationList**"
   - Type: _Data Source > CSVSource_

   1.2 One reference to the elements of the selected list:

   - Name: "**Transportation**"
   - Type: "_Agent > Transportation_"
   - _Uses data source from attribute_: TransportationList

2. Let's adjust the UI of our newly created elements, so that they fit visually in our Purchase Order Document. Edit the **PurchaseOrderForm** using the option **_User Interface / Forms_**, select the element and change it's UI values to:

Element: "**Transportation List**"

- **Row**: 3
- **Column**: 9
- **Size**: 2

    <p align="center">
        <img src="/images/tutorials/connector/ConnectorTutorial_Element_UI.PNG">
    </p>

Element: "**Transportation**"

- **Row**: 3
- **Column**: 4
- **Size**: 2

  ![ConnectorTutorial_PurchaseDocumentEndOfTutorial](/images/tutorials/connector/tutorial_result.jpg) (if your UI doesn't match this one, don't worry, you've just skipped one or more tutorials along the way)

That's it! Your Purchase Document now reads directly from a specific Data Source, and simulates the integration of a delivery system selection option alongside your order.

Go to [**Advanced Connector Tutorial**](omnia3_multisystemconnectortutorial.html).
