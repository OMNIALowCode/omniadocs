---
title: Multi System Connector Tutorial
keywords: omnia3
summary: "OMNIA Low-Code Development Platform - Multi System Connector Tutorial"
sidebar: omnia3_sidebar
permalink: omnia3_multisystemconnectortutorial.html
folder: omnia3
---

## 1. Introduction

Based on a Purchase Orders management scenario, this tutorial shows a real scenario of how easily OMNIA can combine information from multiple external data sources, using the OMNIA connector to access data located on-premises.

This tutorial is an advanced implementation of the [data sources tutorial](omnia3_datasourcetutorial.html) in order to understand how data sources work, please read [this section of the documentation](omnia3_modeler_datasources.html).

The tutorial is divided in 4 different areas. On the first area, Create a new connector, we are going to check how a new connector is created and associated to a tenant. Next, on Modeling entities area, we are going to evaluate how to model the core entities for this solution from scratch.
On the third area, we are going to focus on Purchase Order modeling, combining all previously modeled entities and integrating information on ERP Primavera. To end, we will evaluate how to communicate with an external API.

As our custom data source, we are going to use the [PRIMAVERA ERP V10](https://pt.primaverabss.com){:target="\_blank"}. The chosen external API is [Last FM](https://www.last.fm/api){:target="\_blank"}, which provides data related to music.

## 2. Prerequisites

This tutorial assumes that you have created a OMNIA tenant ([click here to see how](omnia3_tenantcreation.html)), and are logged in as a user with modeling privileges to this tenant. You must also have access to the management area to manage the connectors.

This tutorial also requires an access to [Primavera ERP](https://pt.primaverabss.com){:target="\_blank"}, on version 10.

## 3. Create a new connector

1. Start by accessing the management area, by clicking the option "Go to Tenants management".

2. Through the left side menu, create a new connector by accessing the option **_Connectors / Add new_**. Set its Code and Name as "AnalogSoundConnector". 

   Right after creating the connector, a modal with its data should be shown. Copy the **Client Username**, **Client ID** and **Client Secret** to use later when configuring the Connector.

3. Now we are going to grant the connector access privileges for the tenant. Access the option **_Security / Roles_**, and select Administration role for the tenant (composed by the tenant code with prefix "Administration". E.g. AdministrationDemoTenant)

4. Click the button **_Add new_** to grant the connector user access to the tenant. The user can be retrieved on step 2, property "Client Username". If you didn't copy the username in that moment, select the connector on the list to access that information. 

5. Now use these configurations to configure a connector in the machine with the Primavera ERP, following the [installation guide](omnia3_connector_install.html) and [configuration guide](omnia3_connector_configuration.html).

6. Start the configured connector.

## 4. Modeling Entities

1. Access OMNIA homepage, select the tenant where you are going to model and you will be redirected to the modeling area.

2. Through the left side menu, create a new Agent by accessing the option **_Business / Agents_** and clicking the **_Add new_** button on the top right side. Set _"Company"_ as the Agent name.

   ![Modeler create Agent_Company](/images/tutorials/multisystemconnector/Modeler-Create-Agent.PNG)

3. Through the left side menu, create a new Generic Entity by accessing the option **_Business / Generic Entities_**. Set _"Artist"_ as its name.

   ![Modeler create GenericEntity_Artist](/images/tutorials/multisystemconnector/Modeler-Create-GenericEntity.jpg)

4. Build & Deploy model

5. Go to application area and create a new Company (by accessing the option **_Configurations / Company / Create new_**)

6. Create a new Artist

7. Go to modeling area, and through the left side menu, create a new Data Source by accessing the option **_Business / Data Sources_** and clicking the **_Add new_** button on the top right side. Set its Name as "_Primavera_", Behaviour Runtime as _"Internal"_ and Data Access Runtime as _"External"_. Check the flag "Will be executed in a connector?"

   ![Modeler create DataSource_Primavera](/images/tutorials/multisystemconnector/Modeler-Create-DataSource.jpg)

8. Navigate to tab _Behaviour Dependencies_, and create a **_File Dependency_** for each of the following Primavera assemblies:

   1. StdBE100.dll
   2. ErpBS100.dll
   3. IBasBS100.dll
   4. BasBE100.dll
   5. ICmpBS100.dll
   6. CmpBE100.dll

   ![Modeler_Primavera_Add_Dependency](/images/tutorials/multisystemconnector/Modeler-Primavera-Add-Dependency.jpg)

9. Create a new Agent with name _"Supplier"_, and set it as using the external data source _"Primavera"_ that you created earlier.

   ![Modeler create Agent_Supplier](/images/tutorials/multisystemconnector/Modeler-Create-Agent-Supplier.jpg)

10. On Agent _"Supplier"_, navigate to tab _Behaviour Namespaces_, and define a reference for the following namespaces:

    1. StdBE100
    2. ErpBS100
    3. BasBE100

    ![Modeler_Supplier_Add_Namespace](/images/tutorials/multisystemconnector/Modeler-Supplier-Add-ERP-Namespace.jpg)

11. Navigate to tab _"[Data Behaviours](omnia3_modeler_datasources.html)"_, and add a code expression to the _"ReadList"_ behaviour. This behaviour will be used for Query and List requests for this entity.

    Copy and paste the following code (_Remember to **change** the **`"username"`** and **`"password"`** fields to your actual username and password._):

    ```C#
    ErpBS bsERP = new ErpBS();
    try
    {
      List<IDictionary<string, object>> suppliersList = new List<IDictionary<string, object>>();

      string username = "";
      string password = "";

      bsERP.AbreEmpresaTrabalho(StdBETipos.EnumTipoPlataforma.tpEmpresarial, "DEMO", username, password);

      StdBELista queryResults = bsERP.Consulta($"SELECT Suppliers.SuppliersCount, Fornecedor, Nome from Fornecedores CROSS JOIN (SELECT Count(*) AS SuppliersCount FROM Fornecedores) AS Suppliers ORDER BY Fornecedor ASC OFFSET {(page - 1)*pageSize} ROWS FETCH NEXT {pageSize} ROWS ONLY");

      int numberOfRecords = Convert.ToInt32(queryResults.Valor("SuppliersCount").ToString());
      while (!queryResults.NoFim())
      {
         var supplier = new Dictionary<string, object>() {
            { "_code", queryResults.Valor("Fornecedor").ToString()},
            { "_name", queryResults.Valor("Nome").ToString()}
         };

         suppliersList.Add(supplier);
         queryResults.Seguinte();
      }

      return (numberOfRecords, suppliersList);
    }
    catch (Exception e)
    {
      Console.WriteLine(e.Message);
      throw;
    }
    finally
    {
      if (bsERP.Contexto.EmpresaAberta)
         bsERP.FechaEmpresaTrabalho();
    }
    ```

12. Set the code expression for the _“Read”_ Data Behaviour, so that data is retrieved when a **_Primavera_** Supplier is edited on OMNIA.

    Copy and paste the following code (Remember to change the "username" and "password" fields to your actual username and password.):

    ```C#
    SupplierDto dto = new SupplierDto();
    ErpBS bsERP = new ErpBS();
    try
    {
      string username = "";
      string password = "";

      bsERP.AbreEmpresaTrabalho(StdBETipos.EnumTipoPlataforma.tpEmpresarial, "DEMO", username, password);
      StdBELista queryResults = bsERP.Consulta($"SELECT Fornecedor, Nome FROM Fornecedores WHERE Fornecedor = '{identifier}'");

      if (!queryResults.Vazia())
      {
         dto._code = queryResults.Valor("Fornecedor").ToString();
         dto._name = queryResults.Valor("Nome").ToString();
      }
      else
      {
         throw new Exception($"Could not retrieve Supplier with code '{identifier}'");
      }
      return dto;
    }
    catch (Exception e)
    {
      Console.WriteLine(e.Message);
      throw;
    }
    finally
    {
      if (bsERP.Contexto.EmpresaAberta)
         bsERP.FechaEmpresaTrabalho();
    }
    ```

13. Set the code expression for the _“Create”_ Data Behaviour, so that a new Supplier is created on Primavera ERP when it is created on OMNIA.

    Copy and paste the following code (Remember to change the "username" and "password" fields to your actual username and password.):

    ```C#
    ErpBS bsERP = new ErpBS();
    try
    {
      string username = "";
      string password = "";
      bsERP.AbreEmpresaTrabalho(StdBETipos.EnumTipoPlataforma.tpEmpresarial, "DEMO", username, password);

      BasBEFornecedor fornecedor = new BasBEFornecedor
      {
         Fornecedor = dto._code,
         Nome = dto._name,
         Moeda = "EUR",
         NumContribuinte = "999999990"
      };

      bsERP.Base.Fornecedores.Actualiza(fornecedor);

      return dto;
    }
    catch (Exception e)
    {
      Console.WriteLine(e.Message);
      throw;
    }
    finally
    {
      if (bsERP.Contexto.EmpresaAberta)
         bsERP.FechaEmpresaTrabalho();
    }
    ```

14. Build & Deploy model

15. Go to application area, and create new instance of Primavera. The Connector value is the code defined earlier when the connector was created

    ![Modeler create Primavera_Demo](/images/tutorials/multisystemconnector/Application-Create-Primavera.jpg)

16. List Suppliers. If prompted, select the Primavera instance and check that list is filled with ERP database Suppliers

17. Create a new Supplier, and check that it is integrated on ERP Primavera

18. Go to modeling area. Create a new Resource with name _"Product"_, and set it as using the external data source _"Primavera"_ that you created earlier.

    ![Modeler create Resource_Product](/images/tutorials/multisystemconnector/Application-Create-Product.jpg)

19. On Resource _"Product"_, navigate to tab _Behaviour Namespaces_, and define a reference the following namespaces (define _External_ as Execution Location):

    1. StdBE100
    2. ErpBS100

20. Navigate to tab _"[Data Behaviours](omnia3_modeler_datasources.html)"_, and add a code expression to the _"ReadList"_ behaviour. This behaviour will be used for Query and List requests for this entity.

    Copy and paste the following code (_Remember to **change** the **`"username"`** and **`"password"`** fields to your actual username and password._):

    ```C#
    ErpBS bsERP = new ErpBS();
    try
    {
      List<IDictionary<string, object>> productsList = new List<IDictionary<string, object>>();
    	
      string username = "";
      string password = "";

      bsERP.AbreEmpresaTrabalho(StdBETipos.EnumTipoPlataforma.tpEmpresarial, "DEMO", username, password);
    	
      StdBELista queryResults = bsERP.Consulta($"SELECT Products.ProductsCount, Artigo, Descricao from Artigo CROSS JOIN (SELECT Count(*) AS ProductsCount FROM Artigo) AS Products ORDER BY Artigo ASC OFFSET {(page - 1)*pageSize} ROWS FETCH NEXT {pageSize} ROWS ONLY");

      int numberOfRecords = Convert.ToInt32(queryResults.Valor("ProductsCount").ToString());
    	
      while (!queryResults.NoFim())
      {
         var product = new Dictionary<string, object>() {
            { "_code", queryResults.Valor("Artigo").ToString()},
            { "_name", queryResults.Valor("Descricao").ToString()}
         };

         productsList.Add(product);
         queryResults.Seguinte();
      }
      return (numberOfRecords, productsList);
    }
    catch (Exception e)
    {
      Console.WriteLine(e.Message);
      throw;
    }
    finally
    {
      if (bsERP.Contexto.EmpresaAberta)
         bsERP.FechaEmpresaTrabalho();
    }
    ```

21. Build & Deploy model

22. Go to application area, and check that ERP Products can now be listed on OMNIA

## 5. Modeling Purchase Order

1. Go to modeling area and, through the left side menu, create a new Commitment by accessing the option **_Business / Commitments_** and clicking on right top side **_Add new_** button.

   Set its Name as "_GoodsPurchaseRequest_", _"Product"_ as the resource to be exchanged, _"Supplier"_ as provider agent and _"Company"_ as receiver agent. Select _"Primavera"_ as Data Source.

   ![Modeler create Commitment_GoodsPurchaseRequest](/images/tutorials/multisystemconnector/Modeler-Create-Commitment.jpg)

2. Edit the commitment "_GoodsPurchaseRequest_", and create the following **Reference** attributes:

   - Artist (Type: Generic entity, Artist)
   - Primavera (Type: Data source, Primavera)

3. Create a new **Primitive** attribute with _AlbumMBid_ as _Name_ and _Text_ as Type

4. Still on commitment "_GoodsPurchaseRequest_", edit attributes _"\_resource"_ and _"\_provider"_ and set attribute Primavera as the Data Source

   ![Modeler edit Attribute_Resource](/images/tutorials/multisystemconnector/Modeler-Edit-Attribute.jpg)

5. Through the left side menu, create a new Document by accessing the option **_Business / Documents_**. Set its Name as "_PurchaseOrder_", and select _"Primavera"_ as Data Source.

   ![Modeler create Document_PurchaseOrder](/images/tutorials/multisystemconnector/Modeler-Create-Document.jpg)

6. On Document "_PurchaseOrder_", add the following **Reference** attributes:

   - Primavera (Type: Data source, Primavera)
   - Supplier (Type: Agent, Supplier. Uses attribute Primavera as data source)

7. Create a new **Collection** attribute with _OrderLines_ as _Name_ and _Commitment / GoodsPurchaseRequest_ as Type

8. On Document "_PurchaseOrder_", navigate to tab _Behaviour Namespaces_, and define a reference for the following namespaces (define _External_ as Execution Location):

   1. StdBE100
   2. ErpBS100
   3. CmpBE100

9. Navigate to tab _"[Data Behaviours](omnia3_modeler_datasources.html)"_, and set the code expression to be executed on _"ReadList"_. This behaviour will be used for Query and List requests for this entity.

   Copy and paste the following code (_Remember to **change** the **`"username"`** and **`"password"`** fields to your actual username and password._):

   ```C#
   ErpBS bsERP = new ErpBS();
   try
   {
      List<IDictionary<string, object>> ordersList = new List<IDictionary<string, object>>();

      string username = "";
      string password = "";
   	
      bsERP.AbreEmpresaTrabalho(StdBETipos.EnumTipoPlataforma.tpEmpresarial, "DEMO", username, password);

      StdBELista queryResults = bsERP.Consulta($"SELECT Orders.OrderCount, Serie, TipoDoc, NumDoc, Entidade, CONVERT (NVARCHAR(10), DataDoc, 120) AS DataDoc from CabecCompras  CROSS JOIN (SELECT Count(*) AS OrderCount FROM CabecCompras where TipoDoc = 'ECF') AS Orders where TipoDoc = 'ECF' ORDER BY DataDoc DESC OFFSET {(page - 1)*pageSize} ROWS FETCH NEXT {pageSize} ROWS ONLY");

      int numberOfRecords = Convert.ToInt32(queryResults.Valor("OrderCount").ToString());
   	
      while (!queryResults.NoFim())
      {
         var order = new Dictionary<string, object>() {
            { "_code", queryResults.Valor("Serie").ToString()+"/"+queryResults.Valor("NumDoc").ToString()},
            { "_serie", queryResults.Valor("Serie").ToString()},
            { "_number", queryResults.Valor("NumDoc").ToString()},
            { "_date", queryResults.Valor("DataDoc").ToString()}
         };

         ordersList.Add(order);
         queryResults.Seguinte();
      }

      return (numberOfRecords, ordersList);
    }
    catch (Exception e)
    {
      Console.WriteLine(e.Message);
      throw;
    }
    finally
    {
      if (bsERP.Contexto.EmpresaAberta)
         bsERP.FechaEmpresaTrabalho();
    }
   ```

10. Still on tab _"[Data Behaviours](omnia3_modeler_datasources.html)"_, set the code expression to be executed on _"Create"_. This behaviour will be used to create new instances on ERP everytime a new PurchaseOrder is created on Omnia.

    Copy and paste the following code (_Remember to **change** the **`"username"`** and **`"password"`** fields to your actual username and password._):

    ```C#
    ErpBS bsERP = new ErpBS();
    try
    {
      string username = "";
      string password = "";
      bsERP.AbreEmpresaTrabalho(StdBETipos.EnumTipoPlataforma.tpEmpresarial, "DEMO", username, password);

      CmpBEDocumentoCompra purchaseOrder = new CmpBEDocumentoCompra
      {
         Tipodoc = "ECF",
         Serie = "A",
         TipoEntidade = "F",
         Entidade = dto.Supplier,
         NumDocExterno = "0",
         Observacoes = $"Documento gerado no portal OMNIA: Pedido de Encomenda {dto._serie} / {dto._number}",
         DataHoraCarga = DateTime.Now,
         DataHoraDescarga = DateTime.Now
      };

      bsERP.Compras.Documentos.PreencheDadosRelacionados(purchaseOrder);

      foreach (var line in dto.OrderLines)
      {
         double quantity = Convert.ToDouble(line._quantity);
         bsERP.Compras.Documentos.AdicionaLinha(purchaseOrder, line._resource, ref quantity);
      }

      bsERP.Compras.Documentos.Actualiza(purchaseOrder);

      return dto;
    }
    catch (Exception e)
    {
      Console.WriteLine(e.Message);
      throw;
    }
    finally
    {
      if (bsERP.Contexto.EmpresaAberta)
         bsERP.FechaEmpresaTrabalho();
    }
    ```

11. Build & Deploy model

12. Go to the Application area, and validate that ERP Purchase Orders can now be listed.

13. On Modeling area, navigate to _"PurchaseOrder"_ tab _"[Entity Behaviours](omnia3_modeler_datasources.html)"_, and define a behaviour to be executed _"Before Collection Entity is Initialized"_. This behaviour will be used to set default values on Commitment instances.

    Set OrderLines as collection, and then copy and paste the following code:

    ```C#
    entry._provider = Supplier;
    entry._receiver = "AnalogSound";
    entry.Primavera = Primavera;
    ```

14. Edit the _"PurchaseOrderForm"_ to reorganize the user interface, with the following inputs:

    - On document header, remove Code attribute and reorganize remaining attributes
    - On OrderLines attributes, hide attributes Provider, Receiver, Code and Primavera

    A possible final result is the following:

    ![Modeler purchaseOrder UI_Result](/images/tutorials/multisystemconnector/Application-PurchaseOrder-UI.jpg)

15. Build & Deploy model

16. Go to application area. Access the option **_Series / Purchase Order Serie / Add new_**, and create a new number serie for document PurchaseOrder

17. Access the option **_Documents / PurchaseOrder / Add new_**, and create a new Purchase Order. After saving, the Order should be integrated on ERP Primavera

## 5. Communicate with an external API

1. Go to the **Modeler** and click on option **Business / Data sources / System** to add references to this data source. Click on button **Add new** to add a new **Behaviour Dependency** for .NET assembly System.Net.Http. Set _Execution Location_ as Internal.

   ![Modeler Add_Dependency](/images/tutorials/advanced/Modeler-Add-Behaviour-Dependency.jpg)

2. On Commitment "_GoodsPurchaseRequest_", navigate to tab _Behaviour Namespaces_, and define a reference to namespace System.Net.Http

   ![Modeler Add_Namespace](/images/tutorials/multisystemconnector/Modeler-Add-Namespace.jpg)

3. Navigate to tab _"[Entity Behaviours](omnia3_modeler_datasources.html)"_, and define an _"Action"_ behaviour to be executed when attribute \_resource is changed. This behaviour will be used to retrieve from LastFM API a unique album identifier.

   Copy and paste the following code (_Remember to **change** the **`"API_KEY"`** field to your actual LastFM API Key._):

   ```C#
   if (!string.IsNullOrEmpty(newValue) && !string.IsNullOrEmpty(this.Artist))
   {
      var client = new HttpClient();

      string apiEndpoint = $"http://ws.audioscrobbler.com/2.0/?method=album.getinfo&api_key=API_KEY&artist={this.Artist}&album={newValue}&format=json";
   	
      var requestResult = client.GetAsync(apiEndpoint).GetAwaiter().GetResult();
   	
      string responseBody = requestResult.Content.ReadAsStringAsync().GetAwaiter().GetResult();
      if (!requestResult.IsSuccessStatusCode)
         throw new Exception($"Error on retrieving album: {responseBody}");
   	
      var response = JsonConvert.DeserializeObject<Dictionary<string, object>>(responseBody);
   	
      var albumData = JsonConvert.DeserializeObject<Dictionary<string, object>>(response["album"].ToString());

      this.AlbumMBid = albumData["mbid"].ToString();
   }
   ```

4. Build & Deploy model

5. Go to application area, and create a new Purchase Order. Check that, when Artist and Resource are identified and valid, attribute Album MBid is filled with the album unique identifier
