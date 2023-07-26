---
title: State Machine Tutorial
keywords: omnia3
summary: "Learn to create and apply state machines to an entity"
sidebar: omnia3_sidebar
permalink: omnia3_statemachine.html
folder: omnia3
---


## 1. Introduction

Now that you have completed the Beginner Tutorial, whose result is a functional order management application, this State Machines Tutorial will focus on the addition of Document states to our application's Purchase Order Document.

In this example, we’ll create a state machine for our document with four states: "Initial", "Review", "Approved" and "Denied". When a user submits a document it will adopt the "Review" state. If accepted, the document will move to the "Approved" state, if rejected, it will move to the "Rejected" state. 

To know more about how State Machines work, see our [State Machine](omnia3_modeler_statemachines.html) page.


## 2. Prerequisites

This tutorial assumes that you have created a OMNIA tenant, and are logged in as a user with modeling privileges to this tenant.

It is necessary to have completed the steps in the  [Beginner tutorial](omnia3_beginnertutorial.html), as this tutorial builds upon it.

## 3. State Machine

1. Go to the modeling area and access the option ***Business / State Machines / Add New***

1.1 Click on the "Related to" field and select the option ***Document / Purchase Order***

![CreateStateMachine](/images/tutorials/statemachine/modeler-create-state-machine.jpg)
![NewStateMachine](/images/tutorials/statemachine/modeler-new-state-machine.jpg)

1.2 Open the new "PurchaseOrderStateMachine" by clicking on it and use the "Add New" button to add the new "Review" state

![AddNewState](/images/tutorials/statemachine/modeler-add-new-state.jpg)
	

1.3 Repeat the process to create the "Approved" and "Rejected" states, but in these states activate the options "Disable all attributes" and "Disable all operations":
	![AddNewStateApproved](/images/tutorials/statemachine/modeler-add-approved-state.jpg)
	![AddNewStateRejected](/images/tutorials/statemachine/modeler-add-rejected-state.jpg)

1.4 Let's remove the "Completed" state, since we're not going to use it, by simply accessing it and using the "Delete" option:
	![DeleteCompleted](/images/tutorials/statemachine/modeler-delete-completed-state.jpg)

1.5 Now let's add the decisions that will trigger our document's state transitions:

1.5.1 Open the "Review" state (it will open on the "Decisions" tab by default), click on "Add New", fill its name as "Approve" and save it.
	![AddApprovedDecision](/images/tutorials/statemachine/modeler-add-approve-decision.jpg)

1.5.2 Add another decision to the "Review" state, but this time name it "Reject" and make the decision commentary required:
	![AddRejectedDecision](/images/tutorials/statemachine/modeler-add-rejected-decision.jpg)

1.6 Now let's finalize our state machine by adding Transitions:

1.6.1 Go back to your state machine, open the "Initial" state, go to the tab "Transitions" and "Add New":
	![InitialToReviewTransition](/images/tutorials/statemachine/modeler-add-initialtoreview-transition.jpg)

1.6.2 Now go to the "Review" state, access the "Transitions" tab and let's add two new transitions:
	
- ReviewToApproved
	![ReviewToApproved](/images/tutorials/statemachine/modeler-add-reviewtoapproved-transition.jpg)
	
- ReviewToRejected
	![ReviewToRejected](/images/tutorials/statemachine/modeler-add-reviewtorejected-transition.jpg)

This is what your State Machine should look like:
	![AddApprovedDecision](/images/tutorials/statemachine/modeler-statemachine-finished.jpg)

1.7 Build and Deploy your model and visit your application

1.7.1 Create a new Purchase Order Document and submit it
	![AddNewDocument](/images/tutorials/statemachine/application-add-purchaseorder.jpg)

1.7.2 Now open that same document and approve it.
	![OpenReviewDocument](/images/tutorials/statemachine/application-review-purchaseorder.jpg)

This should be the look of your approved document:
	![AcceptedDocument](/images/tutorials/statemachine/application-approved-purchaseorder.jpg)

1.7.3 Let's create another document, but this time reject it, instead of accepting it, and add the rejection commentary:
	![AddComentary](/images/tutorials/statemachine/application-comment-purchaseorder.jpg)

1.7.4 Now open the rejected document and use the option "More Options" > "Show History". You should now see the comentary that rejected the document.
	![OpenHistoryTab](/images/tutorials/statemachine/application-purchaseorder-history.jpg)

That's it, we've just created a new State Machine and added it to our Purchase Order Management.