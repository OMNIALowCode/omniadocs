---
title: Modeling Entities (UI)
keywords: user interface lowcode web application development
summary: "Find out how to Structure your application's user interface by Modeling its Entities with the OMNIA Platform's User Interface Modeler."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_entities_ui.html
folder: omnia3
---

## 1. User Interface

**_Entity / User Interface_**

In **OMNIA Platform** you can customize how the fields are shown in the form to create or edit of your entity.

Automatically, the platform adds and removes user interface elements when a new attribute is added or an existing one is deleted from an entity.

The form layout is organized with _Rows_ and _Columns_. Each row is divided horizontally in 12 columns.

### How to add a new element?

To add a new element check the right sidebar in the **User Interface**, where you'll find the **"Drag to add"** section with two options:

**Related Entity Attributes** - Attributes of the current entity

![Related Entity Attributes](/images/modeler/AddUIRelatedEntityAttribute.png)

**Add new Element** - Elements types available to add to the current entity

![Add new Element](/images/modeler/AddUINewElement.png)

Simply select the opinion you desire, and drag and drop the attribute or element type in the entity's User Interface Dashboard.

When adding a new element to the layout, you also may fill the following information:

- **Name**: the entity attribute this element will represent in the layout (will allow you to read and write in this attribute);
- **Label**: the element caption;
- **Help text**: the detailed description of the element;
- **Row**: the layout row in which the element will be placed;
- **Column**: the layout column in which the element will be placed;
- **Size**: the element size on a scale of 1 (the smaller size) to 12 (the bigger size). Click [here](omnia3_modeler_userinterface.html#lists-and-grid-columns), to know more about elements size and columns;
- **Is the element hidden?**: the visibility of the element (hidden or visible);
- **Minimal visible screen size**: the visibility of the element, related to the user's device screen size (at sizes smaller than the one selected, the element will be hidden);

After the element configuration, it's important to save your changes to persist it.

### How to add a new container element?

To add a new container check the right sidebar in the **User Interface**, where you'll find the **"Drag to add"** section. Select the **Add new Element** option.

Now select and hold the **Container** option, drag and drop it in the entity's User Interface Dashboard. You also may fill the following information:

- **Name**: the element's unique identifier attribute;
- **Label**: the element caption;
- **Help text**: the detailed description of the element;
- **Row**: the layout row in which the element will be placed;
- **Column**: the layout column in which the element will be placed;
- **Size**: the element size on a scale of 1 (the smaller size) to 12 (the bigger size). Click [here](omnia3_modeler_userinterface.html#lists-and-grid-columns), to know more about elements size and columns;
- **Is the element hidden?**: the visibility of the element (hidden or visible);
- **Minimal visible screen size**: the visibility of the element, related to the user's device screen size (at sizes smaller than the one selected, the element will be hidden);

### How to add a new panel element?

By selecting the option _Add new panel_ you will be able to add new panels to your layout, after filling the following information:

- **Name**: the element's unique identifier attribute;
- **Label**: the element caption;
- **Help text**: the detailed description of the element;
- **Row**: the layout row in which the element will be placed;
- **Column**: the layout column in which the element will be placed;
- **Size**: the element size on a scale of 1 (the smaller size) to 12 (the bigger size). Click [here](omnia3_modeler_userinterface.html#lists-and-grid-columns), to know more about elements size and columns;
- **Is the element hidden?**: the visibility of the element (hidden or visible);
- **Minimal visible screen size**: the visibility of the element, related to the user's device screen size (at sizes smaller than the one selected, the element will be hidden);

### How to add a new calendar element?

To add a new calendar check the right sidebar in the **User Interface**, where you'll find the **"Drag to add"** section. Select the **Add new Element** option.

Now select and hold the **Calendar** option, drag and drop it in the entity's User Interface preview. You also need to fill the following information:

- **Name**: the element's unique identifier attribute;
- **Mapping**: the element, of type collection, that will be used as a data source;
  (In case of a single date event, use the Date Mapping option, if you require a date interval, use Start and Finish Date Mapping instead)
- **Date Mapping**: the collection element that will represent the calendar's event date;
- **Start Date Mapping**: start date of the date mapping;
- **Finish Date Mapping**: end date of the date mapping;
- **Title Mapping**: the element that will be used to define the title property;
- **Category Mapping**: the element that will be used to define the category property;
- **Label**: the element caption;
- **Help text**: the detailed description of the element;
- **Row**: the layout row in which the element will be placed;
- **Column**: the layout column in which the element will be placed;
- **Size**: the element size on a scale of 1 (the smaller size) to 12 (the bigger size). Click [here](omnia3_modeler_userinterface.html#lists-and-grid-columns), to know more about elements size and columns;
- **Is the element hidden?**: the visibility of the element (hidden or visible);
- **Minimal visible screen size**: the visibility of the element, related to the user's device screen size (at sizes smaller than the one selected, the element will be hidden);

### How to change the positioning of an element?

In the User Interface tab, select the element you want to change and, in the _Row_ and/or _Column_ fields, set the new positioning values.

### How to change the size of an element?

In the User Interface tab, select the element you want to change and, in the _Size_ field, select the new size. Click [here](omnia3_modeler_userinterface.html#lists-and-grid-columns), to know more about elements size and columns.

### How to remove an element?

Picking the element you want to remove, select the option _Delete_ and confirm your option in the confirmation window.

## 2. User Interface Behaviours

**_Entity / User Interface Behaviours_**

In order to extend your application user interface you can add new behaviours to your entities' user interface.

Click [here](omnia3_modeler_uibehaviours.html), to know more about user interface behaviours.

### Accelerators

![UI Accelerator](https://raw.githubusercontent.com/OMNIALowCode/omnia3/master/docs/images/modeler/UIaccelerator.png)

- **Hide an Element**
  The accelerator will allow you to easily select an interface element you wish to hide and add the conditions (value or role) that will trigger that behaviour
  Example: A user selects his payment option and that action will hide the unnecessary elements.

- **Set Element Read Only**
  Easily select an interface element you wish to define as Read Only and add the conditions (value or role) that will trigger that behaviour
  Example: Depending on the user role, allow your Supplier to edit the field "Unit Price", while the custumer only sees it as read only.

- **Add Validation Message**
  Quickly add validation messages to your interface elements, add the trigger conditions (value or role) and define the content of your message
  Example: If a user tries to add an invalid email on a field, an error message is returned indicating that.

### Casing

Because OMNIA WebApp is following the JavaScript best practices, the elements' names are in camelCase.

In the following sample, to access the value representing the attribute _TotalAmount_, is used the _totalAmount_ property.

```JavaScript
    this.totalAmount
```

### How to hide an element?

In this sample, base element _\_code_ is set as hidden:

```JavaScript
    this._metadata.elements._code.isHidden = true;
```

### How make an element read-only?

In this sample, base element _\_code_ is set as read only:

```JavaScript
    this._metadata.elements._code.attributes.isReadOnly = true;
```

### How make an element required in the UI?

In this sample, element _email_ is set as required:

```JavaScript
    this._metadata.elements.email.attributes.min = "1";
```

### How to change the size of an element?

In this sample, custom element _supplier_ size is changed:

```JavaScript
    this._metadata.elements.supplier.size = 1;
```

Click [here](omnia3_modeler_userinterface.html#lists-and-grid-columns), to know more about elements size and columns.

### How to set an element value?

In this sample, custom element _supplier_ value is changed:

```JavaScript
    this.supplier = "S001";
```

### How to add or remove a message?

In this sample a message is removed, and added, to the base element _\_code_:

```JavaScript
    this._metadata.elements._code.removeMessage('validation');
    if(this._code === '')
        this._metadata.elements._code.addMessage('My error message', 'error', 'validation');
    else
        this._metadata.elements._code.addMessage('My success message', 'success', 'validation');
```

_Note_: There are only two types of messages available, as shown in the previous sample: **error** and **success**.

### How to manage the state of the entities default options?

In this sample, the default entity options _Save_, _Show history_, _Delete record_ and _Destroy sensitive data_ are set as hidden:

```JavaScript
    // Hide History option
    this._metadata.attributes.showHistoryOption = "hidden";
    // or Disable History option
    this._metadata.attributes.showHistoryOption = "disabled";

    // Hide Delete option
    this._metadata.attributes.deleteOption = "hidden";
    // or Disable Delete option
    this._metadata.attributes.deleteOption = "disabled";

    // Hide Destroy option
    this._metadata.attributes.destroyOption = "hidden";
    // or Disable Destroy option
    this._metadata.attributes.destroyOption = "disabled";

    // Hide Save option
    this._metadata.attributes.saveOption = "hidden";
    // or Disable Save option
    this._metadata.attributes.saveOption = "disabled";
```

### How to redirect to another application page?

In this sample, the user will be redirected to another page of the application, using an existing function of the Form/Dashboard _context_:

```JavaScript
    // The application will be redirected to the dashboard of the entity Employee
    this._context.redirectToApplicationAddress('Employee');
```

### How to have asynchronous behaviours?

In this sample, the behaviour returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), that will allow the behaviour to execute asynchronously:

```JavaScript
    return new Promise(
        (resolve) => {
            // your code here
            resolve();
        }
    );
```

### How to start with a container opened?

Changing the default behaviour of a container can only be done on `Initialize`.

In this sample, the container _myContainer_ is set as opened:

```JavaScript
    this._metadata.elements.myContainer.attributes.isOpen = true;
```

### How to inform the user that an element is loading data?

Inputs give you an attribute to control an internal loader. This is particularly useful when a triggered C# behaviour will change the value of other elements and we want to inform the user that something is happening relative to that element.
You will be responsible to enable and disable the loader. Example: enable, or disable, it when a given element changes its value [in the UI After Change behaviour](omnia3_modeler_uibehaviours.html#2-types-of-behaviours).

```JavaScript
    this._metadata.elements._description.attributes.isLoading = true;
```

### How to block the whole form while loading data?

As a part of the Form metadata, you have an attribute to control an internal loader, and show a context message. This is particularly useful in scenarios where data is being loaded to the UI, and we want to ensure that the user cannot interact with the attributes.
You will be responsible to enable and disable the loader.

Example: enable it when a given element changes its value and a HTTP request is made to retrieve additional data. Disable it when the HTTP request is processed and its data applied to the attributes

```JavaScript

    //Enable loader
    this._metadata.attributes.isLoading = true;

    //Show context message with the loader
    this._metadata.attributes.loadingMessage = "Loading... Please wait";

    //Disable loader
    this._metadata.attributes.isLoading = false;
```

### **Decimal Attributes**

### How to change the number of decimal places of the element?

In this sample, the number of decimal places of the element _decimalField_ is set to a custom value _(3)_.

```JavaScript
    this._metadata.elements.decimalField.attributes.precision = 3;
```

_Note 1: This is only possible in elements that represent decimal attributes. In the other data types, even this attribute is setted, the value will be ignored._

_Note 2: This only changes the number of decimal places in the interface. In order to apply decimal places to the server-side data, you need to develop that logic using C# behaviours._

### **Date Attributes**

### How to set an date element value?

In this sample, custom element _createdDate_ value is changed:

```JavaScript
    this.createdDate = this._context.createMoment('2022-12-31');
```

_Note: For other ways of setting a date, please check [momentjs documentation](https://momentjs.com/docs/#/parsing/)_

### How to get a date on a specific format?

In this sample, the date value of the attribute _dateField_ is retrieved on format _YYYY-MM-DD_.

```JavaScript
    const formattedDate = this.dateField.format("YYYY-MM-DD");
```

_Note 1: This is only possible in elements that represent date attributes._

_Note 2: This only retrieves the value on that format to be used on Javascript behaviours. It does not change the format of the date visible to the user_

### **Shared Attributes**

### How to change the shared attribute's lookup list?

In this sample, the lookup list of the attribute _employee_ is changed to a custom list:

```JavaScript
    this._metadata.elements.employee.attributes.list = 'MyCustomEmployeeList';
```

### How to filter a shared attribute's lookup list?

In this sample, the lookup list of the attribute _employee_ is filtered using the data (in the case, the value of _company_) of the current entity:

```JavaScript
    this._metadata.elements.employee.attributes.listParameters = {
        company: this.company
    };
```

### **Calendar**

### How to set the entries of a calendar?

To each entry is neccessary to define the _date_ and the _title_.
The _category_ can also be defined, in order to group the entries.

In this sample, the entries of the element _calendar_ are setted:

```JavaScript
    this._metadata.elements.calendar.attributes.entries = [
        { date: '2022-12-25', title: 'Christmas', category: 'Holidays' },
        { date: '2022-12-23', title: 'Vacations: Mary Smith', category: 'EmployeeVacations' },
        ...
    ]
```

### How to set the categories of a calendar?

To each category is possible to define the _name_ (used as the unique identifier), a _title_ and a _color_. Is also possible to set the category as inactive by default.

In this sample, the categories of the element _calendar_ are setted:

```JavaScript
    this._metadata.elements.calendar.attributes.categories = [
        { name: 'Category01', title: 'Le 1st category', color: '#d90dea', startAsInactive: true },
        { name: 'A', title: 'Le "A" category', color: '#259fb4', startAsInactive: false }
    ]
```

### How to change the initial date of a calendar?

In this sample, the date where the calendar will be positioned when is initialized is setted:

```JavaScript
    this._metadata.elements.calendar.attributes.initialDate = '2020-01-06';
```

### How to change the initial view of a calendar?

In this sample, the view in which the calendar is initialized is setted:

```JavaScript
    this._metadata.elements.calendar.attributes.initialView = 'year';
```

The following views are available:

| Value            | Description                |
| ---------------- | -------------------------- |
| 'week'           | One week view as calendar  |
| 'month'          | One month view as calendar |
| 'year'           | One year view as calendar  |
| 'week_schedule'  | One week view as schedule  |
| 'month_schedule' | One month view as schedule |
| 'year_schedule'  | One year view as schedule  |

### How to set the calendar start and finish date?

In this sample, the start and finish date is setted. Dates outside the range are blocked

```JavaScript
    this._metadata.elements.calendar.attributes.startsAt = '2021-01-01';

    this._metadata.elements.calendar.attributes.finishesAt = '2021-12-31';
```

### How to execute an action when the view is changed?

In this sample, a function is added to the calendar metadata, in order to be executed every time the calendar's view is changed:

```JavaScript
    this._metadata.elements.calendar.onDataRangeChange = (startDate, finishDate, view) => {
        // your code here
    }
```

### How to execute an action when a category is toggled?

In this sample, a function is added to the calendar metadata, in order to be executed every time a category is activated or deactivated:

```JavaScript
    this._metadata.elements.calendar.onCategoryToggle = (category, isActive) => {
        // your code here
    }
```

### How to execute an action when the calendar modal form is opened?

In this sample, a function is added to the calendar metadata, in order to be executed every time a calendar event is clicked:

```JavaScript
    this._metadata.elements.calendar.onFormOpen = (line) => {
        // your code here    
    }
```

_Note: This function is only available when the Calendar is mapped and located on a form._

### **Web Components**

The Web Component instance will be available to interact with in the JS object and is identified by the name of the element. Due to the array of [supported browsers](https://docs.omnialowcode.com/omnia3_webapprequirements.html), the Javascript should be written in ES6 format.

### How to set a value of a Web Component's property?

In this sample, a custom property's value of a Web Component is setted:

```JavaScript
    this.myWebComponent.theProperty = "The new value";
```

### How to call a function of a Web Component?

In this sample, a custom function of a Web Component is executed:

```JavaScript
    this.myWebComponent.theFunction(parameter1, parameterN);
```

### **Grids**

### How to add new lines to a collection?

In this sample, we're adding a new line to the collection named _myCollection_ and setting some data:

```JavaScript
    this.addTo_myCollection(this._context.cloneObject(this._metadata.elements.myCollection), true).then((newRecord) => {
        newRecord._resource = "P001";
        newRecord._provider = "S001";
        newRecord._receiver = "C001";
        newRecord._quantity = 10;
    });
```

### How to manage the state of the add and remove options in a grid?

In this sample, the options to remove or add records of custom element _collection_ are changed based on a condition:

```JavaScript
    // Disable options
    this._metadata.elements.collection.attributes.addEntry = "disabled";
    this._metadata.elements.collection.attributes.removeEntry = "disabled";

    // Hide options
    this._metadata.elements.collection.attributes.addEntry = "hidden";
    this._metadata.elements.collection.attributes.removeEntry = "hidden";

    // Enable and show options
    this._metadata.elements.collection.attributes.addEntry = "enabled";
    this._metadata.elements.collection.attributes.removeEntry = "enabled";
```

### How to move an element to the details area of a grid?

This feature only applies to the inner elements of a collection element.
In this sample, the element _notes_ (which is an inner element of _collection_) is placed in the details area:

```JavaScript
    this._metadata.elements.collection.elements.notes.attributes.isDetails = true;
```

### How to enable multiple selection of references in a grid?

This feature only applies to grids that contain at least one inner element of type reference.

In this sample we're enabling only one element named _product_ (which is an inner reference element of _collection_) for multiple selection:

```JavaScript
    this._metadata.elements.collection.attributes.multipleSelection = [
        { name: "product" }
    ];
```

To set more elements, simply add then to the multipleSelection list:

```JavaScript
    this._metadata.elements.collection.attributes.multipleSelection = [
        { name: "product" },
        { name: "resource" },
        ...
    ];
```

In the sample below, the element _product_ uses the custom Data Source _externalDatabase_:

```JavaScript
    this._metadata.elements.collection.attributes.multipleSelection = [
        { name: "product", dataSource: this.externalDatabase },
        { name: "resource" },
        ...
    ];
```

When the Data Source is not static, meaning it can change depending in another element of the Form, instead of _dataSource_ it should be identified using _dataSourceAttribute_.

In this sample the element _database_ (which is **not** an inner element of _collection_, but another element of the Form) defines the Data Source of the _product_ element:

```JavaScript
    this._metadata.elements.collection.attributes.multipleSelection = [
        { name: "product", dataSourceAttribute: "database" },
        { name: "resource" },
        ...
    ];
```

### **Custom Modals**

### How to open an Entity on a Modal?

In order to open an already created entity in a modal you must add a new `User Interface (UI) Behaviour` to the entity you wish to open the modal from.

The following properties are available when declaring a new modal instance:

| Value                | Type     | Required | Description                                                                                                                                                               |
| -------------------- | -------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 'disableCloseButton' | boolean  | no       | Be cautious when declaring this property because the modal might not close if you don't add the necessary code for it (explained below).                                  |
| 'hideFooter'         | boolean  | no       | Be cautious when declaring this property because the modal will not have the default option to close. You should add the necessary code for closing it (explained below). |
| 'hideHeader'         | boolean  | no       | Declare it if you intend to hide the title of the modal.                                                                                                                  |
| 'id'                 | string   | no       | The unique identifier necessary to close the modal.                                                                                                                       |
| 'name'               | string   | yes      | The name of the entity to open inside the modal.                                                                                                                          |
| 'onClose'            | function | no       | A callback function the triggers after the modal is closed. It receives a `result` (string) value and an `args` (object). The default value of `result` is `Close`.       |
| 'parameters'         | object   | no       | Any other information you wish to save inside the modal to use later.                                                                                                     |
| 'formConfiguration'         | object   | no       | Optional configuration when opening a modal with a form.              |
| 'size'               | string   | no       | There are four possible sizes: `small`, `medium`, `large` and `extra-large`. The default value is `extra-large`.                                                          |
| 'title'              | string   | no       | The text that appear in modal's header. The default is the entity's `name`.                                                                                               |
| 'type'               | string   | yes      | Identify the type of the entity. There are two possible types: `Dashboard` or `Form`.                                                                                 |

How to declare a modal:

```JavaScript
    //Modal to open a dashboard
    const modal = {
        name: "TermsOfServiceDashboard",
        type: "Dashboard"
    }
```

```JavaScript
    //Modal to open a form
    const modal = {
        name: "SupplierForm",
        type: "Form",
        //optional
        formConfiguration: {
            //Code of the entity to open. Use only when editing an existent entity.
            instanceCode: "S001",
            //DataSource of the entity being edited
            dataSource: "Default",
            //State of the button to close modal. Possible values: hidden or disabled. Default value is visible
            closeButton: "hidden"
        }
    }
```

Finally, to open the modal use the following code:

```JavaScript
    // The 'modal' argument is the constant you created with the properties above
    this._context.openModal(modal);
```

In this sample, there's an example of the `onClose` callback:

```JavaScript
    const modal = {
        ...,
        onClose: (result, args) => {
            console.log(`The modal was close after ${result} and received ${args}.`);
        },
        ...,
    };
```

### How to close a Modal using its Identifier

To close a modal on a specific behaviour you first need to declare the modal's `id` **during it's instantiation**. This way you're able to identify which modal you wish to close, because in the OMNIA Platform you can open multiple modals at once.

So, before opening the modal on a `UI Behaviour`, we recommend to create a **Universally Unique Identifier (UUID)** to differ modals from each other and be _certain_ that identifier isn't used in another instance. For that, use the following Javascript code logic:

```JavaScript
    const id = this._context.createUUID();

    const modal = {
        id: id,
        ...
    };

    this._context.openModal(modal);
```

It's important to declare the `id` in a constant so you can re-use it in the future.

To manually close the modal (for example, after changing a property) add the following code:

```JavaScript
    // When the onClose function doesn't receive any arguments, simply close the modal using it's id.
    this._context.closeModal(id);

    // When you wish to specify an action that triggered the closing action simply specify it as a string, adding it after the id.
    this._context.closeModal(id, result);

    // When the onClose function receives arguments, add it after the result
    this._context.closeModal(id, result, args);
```

### Example of Modal parameters usage

In this sample it's explained how you can add functions (with or without parameters) and constants to the modal's parameters field:

```JavaScript
    // The declaration of the modal, before using the 'this._context.openModal(modal)' method (explained above) to open it
    const modal = {
        ...
        parameters: {
            // In this example we only use one parameter, but you may add as much as you'd like
            functionWithParameters: (params) => {
                // You may use the 'params' constant here
            },

            functionWithoutParameters: () => {
            },

            constant: "example of a constant"
        },
        ...
    };
```

In the sample below it's explained how to use the parameters:

```JavaScript
    // Example on how to call a function with parameters
    this._metadata.parameters.functionWithParameters("example of a parameter");

    this._metadata.parameters.functionWithoutParameters();

    this._metadata.parameters.constant;
```

### How to check if an entity is a Modal

In this sample, it's verified if an entity is a modal or not:

```JavaScript
    // This property is a boolean
    this._metadata.isModal;
```
