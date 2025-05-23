# Core Lab 3 - Adding Business Hours

## Learning Objectives

In this section of the lab we will continue building and testing together.  We will be creating a new Business Hours configuration item, adding it into our flow, and using node variable outputs in the flow logic.  We will also explore Overrides for Business Hours.

## New Elements
 - Business Hours
 - Overrides
 - Subflows
 - Callback
  
## Create New Configuration Items

### Create a new Business Hours
> In Control Hub, navigate to Business Hours and click Create Working Hours
>
> Name: <copy>CL<w class="POD"></w>_Business Hours</copy>
>
> Description: <copy>CL<w class="POD"></w>_Business Hours</copy>
>
> Timezone: <copy>America/Los_Angeles</copy>
>
> Click Add Shift
>
>> Name: <copy>Open</copy>
>>
>> Select Monday through Friday
>>
>> Time duration: 9:00 AM to 6:00 PM
>>
>> Click Save
>
> Click Create
>
> Keep this tab open

---


## Build

### Open flow CL<w class="POD">_core</w>
> Toggle the Edit switch on
>
---

### Add a Business Hours node
> Activity Label: <copy>BusinessHours</copy>
>
> Select Static Business Hours
>
> Business Hour: <copy>CL<w class="POD"></w>_Business Hours</copy>
>
> Delete the connection between New Phone Contact node and Play Message node
>
> Connect the Working Hours node edge to the Play Message node
>
---

### Add a Play Message node
> Connect the Default, Override, and Holidays node edges of the Business Hours node to this Play Message node
>
> Activity Label: <copy>ClosedMessage</copy>
>
> Enable Text-To-Speech
>
> Select the Connector: Cisco Cloud Text-to-Speech
>
> Click the Add Text-to-Speech Message button
>
> Delete the Selection for Audio File
>
> Text-to-Speech Message: <copy>Thank you for calling us.  Unfortunately our offices are currently closed.  Please call back during our normal business hours.</copy>
>

---

### Add a Disconnect Contact node
> Connect the Output node edge from the ClosedMessage node to this Disconnect Contact node
>
---

### <details><summary>Check your flow</summary>![](./assets/core3Flow1.png)</details>

---
### Publish your flow
> Turn on Validation at the bottom right corner of the flow builder
>
> If there are no Flow Errors, Click Publish
>
> Add a publish note
>
> Add Version Label(s): Live 
>
> Click Publish Flow

---

## Testing
1. Launch the [Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="_blank"} and log in selecting the Desktop option for your Voice connection (If it is not still open).
2. On your Agent Desktop, make sure your status is not set to Available
      1. Using Webex, place a call to your Inbound Channel number <copy><w class="DN"></w></copy>
      2. When your hear the hold music disconnect the call
         1. Open the Debugger and note that the path from the Business Hours node hit the welcome message node
         2. Note that you can see the name of the Business Hours 

---

## Edit Configuration Items

### Edit the Business Hours in Control Hub
> Navigate to Business Hours in Control Hub and open <copy>CL<w class="POD"></w>_Business Hours</copy> (if you previously closed it)
>
> Click on the Shift Name Open
>
>> Change the Time duration: 9:00 AM to 12:00 PM 
>>
>> Click Save
>
> Click Save on Business Hours
>
---

## Testing
1. Launch the [Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="_blank"} and log in selecting the Desktop option for your Voice connection (If it is not still open).
2. On your Agent Desktop, make sure your status is not set to Available
      1. Using Webex, place a call to your Inbound Channel number <copy><w class="DN"></w></copy>
      2. When your hear the hold music disconnect the call
         1. Open the Debugger and note that the path from the Business Hours node hit the ClosedMessage node
---

## Enhancement
Let's add a new option where we want to close the queue for lunch but let the caller opt-in for a callback when our agents return.

## Edit Configuration Items

### Edit the Business Hours in Control Hub
> Navigate to Business Hours in Control Hub and open <copy>CL<w class="POD"></w>_Business Hours</copy> (if you previously closed it)
>
> Click on the Shift Name Open
>
>> Change the Name to <copy>Open AM</copy> 
>>
>> Click Save
>
> Click Add Shift
> 
>> Name: <copy>Open PM</copy>
>>
>> Select Monday through Friday
>>
>> Time duration: 1:01 PM to 6:00 PM
>>
>> Click Save
>
> Click Add Shift
> 
>> Name: <copy>Lunch</copy>
>>
>> Select Monday through Friday
>>
>> Time duration: 12:00 PM to 1:00 PM (We may adjust these times during the lab exercise)
>>
>> Click Save
>
> Click Save on Business Hours
>
---

## Build

### Open flow CL<w class="POD">_core</w>
> Toggle the Edit switch on
>
---

### Create these Flow Variables
> Name: <copy>ANI</copy>
>
> Type: String
>
> Default Value: Leave Empty
---
> Name: <copy>cbChoice</copy>
>
> Type: Boolean
>
> Default Value: False
---

### Add a Condition node
> Activity Label: LunchCheck
>
> Expression: `{{BusinessHours.WorkingHoursShift_Name == "Lunch"}}`
>
> Delete the connection between the play welcome message node and the Queue Contact node
>
> Connect the play welcome message node edge to this Condition node
>
> Connect the False node edge to the play welcome message node
>
---

### Add a Subflow node
> Name: LTRCCT2296Callback
>
> Connect the True node edge from LunchCheck to this Subflow node
>
> Subflow Label: Live
>
> Map Subflow Input Variables
>
>> Click Add New
>>
>> Current Flow Variable: <copy>NewPhoneContact.ANI</copy>
>>
>> Subflow Input Variable: <copy>ANI</copy>
> 
> 
>> Click Add New
>>
>> Current Flow Variable: <copy>BusinessHours.WorkingHoursShift_Name</copy>
>>
>> Subflow Input Variable: <copy>BusinessHours</copy>
>
> Map Subflow Output Variables
>
>> Click Add New
>>
>> Subflow Output Variable: <copy>CBbool</copy>
>>
>> Current Flow Variable: <copy>cbChoice</copy>
> 
> 
>> Click Add New
>>
>> Subflow Output Variable: <copy>ANI</copy>
>>
>> Current Flow Variable: <copy>ANI</copy>
> 
---

### Add a Condition node
> Activity Label: CBchoice
>
> Expression: <copy>`{{cbChoice}}`</copy>
>
> Connect the output node edge from the Subflow node to this Condition node
>
> Connect the False node edge to the Disconnect Contact node
>
---

### Add a Callback node
> Connect the True node edge from the CBchoice node to this Callback node
>
> Callback Dial Number: <copy>ANI</copy>
>
> Callback Queue: Static
>
> Callback Queue: <copy><w class="Queue"></w></copy>
> 
> Callback ANI: Static
>
> Callback ANI: <copy><w class="DN"></w></copy>
>
> Connect output node to the Disconnect Contact node
>
---

### <details><summary>Check your flow</summary>![](./assets/core3Flow2.png)</details>

---
### Publish your flow
> Turn on Validation at the bottom right corner of the flow builder
>
> If there are no Flow Errors, Click Publish
>
> Add a publish note
>
> Add Version Label(s): Live 
>
> Click Publish Flow

---

## Testing
1. Launch the [Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="_blank"} and log in selecting the Desktop option for your Voice connection (If it is not still open).
2. On your Agent Desktop, make sure your status is not set to Available
      1. Using Webex, place a call to your Inbound Channel number <copy><w class="DN"></w></copy>


---