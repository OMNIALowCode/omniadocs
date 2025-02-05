---
title: State Machines
keywords: finite state machines lowcode web app development
summary: "Learn all you need to know about our finite-state machine feature and how it easily allows you to build custom, complex state machines and easy implement them on your web applications."
sidebar: omnia3_sidebar
permalink: omnia3_modeler_statemachines.html
folder: omnia3
---

## 1. Introduction

OMNIA Platform enables you to model a [finite-state machine (FSM)](https://en.wikipedia.org/wiki/Finite-state_machine){:target="\_blank"} to describe the states and transitions that occur during the entity lifetime.

The State Machine can change from one state to another in response to some external inputs. The change from one state to another is called a transition. A State Machine is defined by a list of its states and transitions.

## 2. Model State Machines

By choosing _**Business / State Machines**_ in the sidebar, you will have access to the _State Machines'_ management screen, in which will be presented the existing data of the model.

### How to create a State Machine?

Select the option _Add new_ and define the following properties:

- **Related to**: the entity that will be managed using the State Machine;
- **Description**: a textual explanation of this State Machine(can be used as development documentation).

After creating a new state machine, will be automatically created two states: _Initial_ (the State Machine's initial state) and _Completed_.

Also, a new [_Enumeration_](omnia3_modeler_enumerations.html) will be created containing the existing states (this enumeration will be updated everytime a state is added or removed). The _Enumeration_ will be named using the _State Machine_ name with the suffix "States" (e.g.: the State Machine to the entity _Customer_ will be named _CustomerStateMachine_ and the Enumeration _CustomerStateMachineStates_).

In the entity to which the State Machine was created, will be added two system attributes: **\_state** (to store the current state of the record) and **\_assigned** (to store to whom is assigned the entity in the current state).

### How to create a State?

**_Business / State Machine / States_**

Accessing to the details of a _State Machine_ you can add a new state. To do that, in the _States_ list, select the option _Add new_ and define the following properties:

- **Name**: the name of the state (needs to be unique inside the state machine);
- **Description**: the textual explanation of the state's purpose (can be used as development documentation);
- **Is the initial state?**: if the state is the initial one or not;
- **Disable all attributes?**: if marked, all the attributes will be all be shown as read-only, when the entity is in the state;
- **Disable all operations?**: if marked, all the operations (e.g.: save, add lines, etc.) will be disabled, when the entity is in the state;
- **Assign to (C# expression)**: a C# expression to define to whom will be assigned the record when it is in this state.

_Note 1_: If the _Disable all attributes_ property is checked, will be possible to define an exception list of attributes. The attributes in this exception list will not have the _read-only_ property overridden.

_Note 2_: If the _Disable all operations_ property is checked, will be possible to define an exception list of operations. The operations in this exception list will not have the value overridden.

_Note 3_: If there is any User Interface Behaviour in the entity's Form to set an attribute as read-only (or editable) or to set an operation as disabled (or enabled), the configuration set in the Behaviour will be maintained.

### How to define the initial state?

**_Business / State Machine / States / State_**

In the details page of a _State Machine_, selecting one of the existing states is possible to change the _State Machine's_ initial state.

In the State's details page, select the option _Edit State_ and mark the property _Is the initial state?_.

Since a _State Machine_ can have one, and only one, initial state, after marking a state as initial, the previous initial state will be unmarked. If you try to remove the initial state will get an error remembering you that you need one initial state.

### How to assign the entity to someone in a given State?

**_Business / State Machine / States / State_**

In the details page of a _State Machine_, selecting one of the existing states is possible to change to whom the _State's_ is assigned, using the property **Assign to (C# expression)**.

In the State's details page, select the option _Edit State_ and change the property _Assign to (C# expression)_.

Everytime the entity is saved in the _State_, the C# code expression provided in the _Assign to_ property is evaluated and the result is stored in the system attribute **\_assigned**.

The C# expression must return a string, as seen on the example below:

```c#
//Assign to role "Administration" is the TotalAmount value is equal or bigger than 1000. Otherwise, assign to role "Approver"

if(this.TotalAmount >= 1000)
    return "Administration";
else
    return "Approver";
```

The string returned on this behaviour can contain any possible value (a security role, a reference to another entity, ...).

The assignation of the entity to someone does not limit the access to that entity. The queries of that entity type must be reviewed to control access.

### How to disable all attributes in a given State?

**_Business / State Machine / States / State_**

In the details page of a _State Machine_, selecting one of the existing states is possible to set all attributes as _read-only_ when a record is in the _State_.

In the State's details page, select the option _Edit State_ and mark the property _Disable all attributes?_.

### How to disable all operations in a given State?

**_Business / State Machine / States / State_**

In the details page of a _State Machine_, selecting one of the existing states is possible to set all operations as _disabled_ when a record is in the _State_.

In the State's details page, select the option _Edit State_ and mark the property _Disable all operations?_.

### How to enable an attribute in a given State?

**_Business / State Machine / States / State / Enabled Attributes_**

The _Enabled Attributes_ list works as an exception list to the disabled attributes.

It's possible to define a set of enabled attributes in each state.

In order to do that, access the details page of a _State Machine_ and select a state. In the _Enabled Attributes_ list, select the option _Add new_ and define the following properties:

- **Which is the attribute to enable?**: the path to the attribute to enable - corresponds to the attribute name (if the attribute is inside a collection, the path should be the collection name and the attribute's name joined using a dot).

_Note_: This is only possible if the property _Disable all attributes?_ is checked.

### How to enable an operation in a given State?

**_Business / State Machine / States / State / Enabled Operations_**

The _Enabled Operations_ list works as an exception list to the disabled operations.

It's possible to define a set of enabled operations in each state.

In order to do that, access the details page of a _State Machine_ and select a state. In the _Enabled Operations_ list, select the option _Add new_ and define the following properties:

- **The operation is related to...**: define if the operation to enable is over the current Entity or a given Collection Attribute of the Entity. This will influence the operation types _"(Which is the operation to enable?)"_ that the user can select;
- **Which is the attribute?**: the path to the operation to enable - corresponds to the attribute name, if the attribute is a collection (if the operation is relative to the entity, the path should be left empty);
- **Which is the operation to enable?**: the operation type (_Add_, _Update_ or _Delete_).
  - _Add_ - Can be used when a collection is referenced in the _Path_. Use this to enable the user to Add new entries to the collection.
  - _Update_ - Can be used to enable the user to save the entity in the current state. Leave the _Path_ empty to use it.
  - _Delete_ - Can be used for both entity and collections. Use this to enable Entity delete or remove entries from Collection.

_Note_: This is only possible if the property _Disable all operations?_ is checked.

### How to create a Decision?

**_Business / State Machine / States / State / Decisions_**

A decision allows the users to take an action when the entity is in a specific state.

It's possible to define a set of allowed decisions in each state.
In order to do that, access the details page of a _State Machine_ and select a state. In the _Decisions_ list, select the option _Add new_ and define the following properties:

- **Name**: the name of the decision (needs to be unique inside the state);
- **Description**: the textual explanation of the decision's purpose (can be used as development documentation);
- **Should the user write a comment when taking the decision?**: the type of comment that will be prompted to the user, when the decision is made (_None_, _Optional_ or _Required_);
- **Order**: an integer representing the order of the decision in the state.

_Note_: When a state has decisions, a new [_Enumeration_](omnia3_modeler_enumerations.html) is created to store the state's decisions. Everytime a decision is added or removed, the _Enumeration_ is updated.
The _Enumeration_ will be named using the _State Machine_ name, the _State_ name and the suffix "Decisions" (e.g.: the State Machine to the entity _Customer_ will be named _CustomerStateMachine_ and the Enumeration representing the decision of the state _Initial_ _CustomerStateMachineInitialDecisions_).

### How to create a Transition?

**_Business / State Machine / States / State / Transitions_**

A transition describes a condition, that when is met, moves the entity from the current state to a new one.

It's possible to define a set of transitions in each state.
In order to do that, access the details page of a _State Machine_ and select a state. In the _Transitions_ list, select the option _Add new_ and define the following properties:

- **Name**: the name of the transition (needs to be unique inside the state);
- **Description**: the textual explanation of the transition's purpose (can be used as development documentation);
- **Go to state**: the state to where the entity will be moved when the transition is successfully evaluated;
- **Evaluation type**: the type of the evaluation - Automatic (based on a C# expression) or Decision (based on a user's decision);
- **Based on decision**: the decision used to evaluate if the transition should occur (if a C# expression is provided, the two conditions need to be true to the transition occur) - only available in the _Evaluation type_ "Decision";
- **Evaluate using the C# expression**: The C# expression used to evaluate if the transition should occur;
- **Order**: an integer representing the order of evaluation of the transition in the state.

### How to condition a Transition?

**_Business / State Machine / States / State / Transitions_**

A transition can be conditioned using one of two methods: _Automatic evaluation_ or _Decision evaluation_.

**Automatic evaluation**:
The automatic evaluation only uses the C# code expression to decide if the transition will occur or not.

**Decision evaluation**:
The decision evaluation uses the user's decision and the C# code expression to decide if the transition will occur or not.
If the C# code expression is not provided, only the decision will be take in consideration.

To change the way how to evaluate a Transition, edit a transition (accessing to the state details, in the _Transitions_ list) and change the following properties to correspond to the model needs: **Evaluation type**, **Based on decision** and **Evaluate using the C# expression**.

### How to manage State and Decision labels?

Each _State Machine_ has an [_Enumeration_](omnia3_modeler_enumerations.html) representing its _States_.

The same way, each _State_ has an _Enumeration_ representing its _Decisions_.

In order, to change the labels of a _State_ or a _Decision_, it's only necessary to change the label of the respective _Enumeration_.

## 3. State Machine Entity Behaviours

### Transition behaviours

In the modeler, you can add behaviours to be triggered when a transition happens. These behaviours will be executed either when the entity enters (**In**) in a given state or exits (**Out**) a given state.

**In** and **Out** behaviours execute in a transaction together with the state machine evaluation and receive the old state and the new state respectively.

### Project structure

In the behaviours project, you will find in the Entity folder a file with the name _"{Entity}.StateMachine.cs"_ (example: _Customer.StateMachine.cs_).
The state machine definition is in this C# class, side by side with the entity Operations class.

In the _StateMachine.cs_ file you will find the following methods:

- **EvaluateStateTransitions:** Used by the platform to decide the next state. This method can't be changed and is a representation of the modeled State Machine.
- **EvaluateStateTransition*{State}*{TransitionName}:** Transition boolean expression method to decide if the transition should take place. The data from the current entity can be accessed since this is a method of the class.
- **AssignTo\_{State}:** Assign expression method to decide the value of the _\_assigned_ attribute when the entity is in a given state. The data from the current entity can be accessed since this is a method of the class.
- **On{State}In:** Expression method to be executed when the entity enters the State. Old state is received in the variable _fromState_.
- **On{State}Out:** Expression method to be executed when the entity exits the State. New state is received in the variable _toState_.

### The state machine in the context of the entity lifecycle

The evaluation of the State Machine happens immediately before the Platform invokes the Before Save behaviours.

### Accessing the user Decision

In the context of entity behaviours, the modeler can access to the Decision taken through the Context using `_Context.Operation.Decision`. Example:

```c#
if("Accept".Equals(_Context.Operation.Decision))
{
    ...
}
```

### Accessing the user comment

In the context of entity behaviours, the modeler can access to the Comment written by the user through the Context using `_Context.Operation.Comment`.

## 4. State Machine UI Behaviours

When a user selects a decision, the _Save_ action is performed. When the _BeforeSave_ behaviour is executed it is possible to use the user's decision in the JavaScript code.

### Accessing the user Decision

Accessing the context, it's possible to know the decision the user has selected.

In the following sample is shown how to use the decision value in a condition.

```JavaScript
if(this._context.operation.decision === 'Accept'){
    ...
}
```

### How to control the available decisions?

In this sample, the decision _myDecision_ is hidden from the decision selector:

```JavaScript
    this._metadata.attributes.decisionSelector.elements.myDecision.isHidden = true;
```
