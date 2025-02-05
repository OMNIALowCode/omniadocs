---
title: User Interface (UI) Behaviours Tutorial
keywords: omnia3
summary: "Learn to apply behaviours to change interface elements"
sidebar: omnia3_sidebar
permalink: omnia3_uiextensibilitytutorial.html
folder: omnia3
---

## 1. Introduction

Now that you have completed the [Beginner Tutorial](omnia3_beginnertutorial.html), whose result is a functional order management application, this UI Extensibility Tutorial will focus on the execution of behaviours on the user interface (client browser).

In this example, we'll add a new boolean attribute to our document, so that we can give the user the option to "Close" a document when its order is fulfilled. After the user declares the order as fulfilled, the entire document becomes "read only" and cannot be changed again.

To know more about how User Interface (UI) Behaviours work, see our [User Interface Behaviour page](omnia3_modeler_uibehaviours.html).

## 2. Prerequisites

This tutorial assumes that you have created a OMNIA tenant, and are logged in as a user with modeling privileges to this tenant.

It is necessary to have completed the steps in the [Beginner tutorial](omnia3_beginnertutorial.html), as this tutorial builds upon it.

## 3. UI Extensibility

1. Go to the modeling area and edit your _PurchaseOrder_ document by accessing the option **_Business / Documents / PurchaseOrder_**

2. Add the following attribute, that will allow the user to identify when an Order is fulfilled, by clicking on button **Add new / Primitive**:

   - _Name_: **OrderReceived**
   - _Type_: **_Boolean_**

3. Edit the _PurchaseOrderForm_ by accessing the option **_User Interface / Forms / PurchaseOrderForm_**, and change the _OrderReceived_ attribute position and size:

   - _Row_: **8**
   - _Column_: **10**
   - _Size_: **2**
   - _Label_: **Order fulfilled?**

4. Now let's select the main document, check the **Properties** tab on the right sidebar, and create a new _Initialize_ behaviour and paste the following code:

   ```JavaScript
   function setAllElementsAsReadOnly(elements, data) {
      for (const element of Object.values(elements)) {
         element.attributes.isReadOnly = true;

         if (element.type.toUpperCase() === "LIST") {
            element.attributes.addEntry = "hidden";
            element.attributes.removeEntry = "hidden";
         }
      }
   }

   function setReadonlyState(metadata, data) {
      setAllElementsAsReadOnly(metadata.elements, data);

      for (const entry of data.orderLines) {
         setAllElementsAsReadOnly(entry._metadata.elements, entry);
      }
   }

   if (this.orderReceived === true) setReadonlyState(this._metadata, this);
   ```

5. Build the model and go to application, create a new **Purchase Order Document**, and check the "**_Order fulfilled?_**" option before submitting it. Now reopen it and verify that all fields are now _read only_.

   ![PurchaseOrderDocument_readOnly](/images/tutorials/advanced/Application-PurchaseOrder-Closed.jpg)
