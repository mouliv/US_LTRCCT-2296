# Core Lab 1 - Let's Start From the Beginning

## Learning Objectives

In this section of the lab we will building and testing together as we explore the flow builder as well as other areas of the Webex Contact Center. We will start by creating a basic flow from scratch then add functionality as we learn about new features and concepts.  If you are already a seasoned veteran and complete the sections before the rest of teh group, please feel free to help others as we often learn more by teaching.

## Build

### Create a new flow
> Create a new flow named <copy>CL<w class="POD"></w>_core</copy>

---

### Add a Play Message node
> Connect the New Phone Contact output node edge to this Play Message node
>
> Enable Text-To-Speech
>
> Select the Connector: Cisco Cloud Text-to-Speech
>
> Click the Add Text-to-Speech Message button
>
> Delete the Selection for Audio File
>
> Text-to-Speech Message: <copy>Welcome to Lab 1.</copy>
>
---

### Add a Queue Contact node
>  Connect the output node edge from the Play Message node added in the previous step to this node
> 
> Select Static Queue
>
> Queue: <copy><w class="Queue">yourQueueID</w></copy>
>

---

### Add a Play Music node
> Connect the output node edge from the Queue Contact node added in the previous step to this node
>
> Select Static Audio File
>
> Music File: <copy>defaultmusic_on_hold_cisco_opus_no_1.wav</copy>
>
> Connect the output node edge from this node to the input node edge of this node (making  a loop)
>

---

### <details><summary>Check your flow</summary>![](./assets/core1Flow.png)</details>

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

### Map your flow to your inbound channel
> Navigate to Control Hub > Contact Center > Channels
>
> Locate your Inbound Channel (you can use the search): <copy><w class="EP"></w></copy>
>
> Select the Routing Flow: <copy>CL<w class="POD"></w>_core</copy>
>
> Select the Version Label: Live
>
> Click Save in the lower right corner of the screen

---

## Testing
1. Launch the [Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="_blank"} and log in selecting the Desktop option for your Voice connection (If it is not still open).
2. On your Agent Desktop, make sure your status is not set to Available
      1. Using Webex, place a call to your Inbound Channel number <copy><w class="DN"></w></copy>
      2. After you hear the queue treatment start, change your status to Available and answer the call. 
      3. End the call and wrap it up
3. In your flow:
      1. Open the Debugger
      2. Select the last interaction (at the top of the list)
      3. Trace the steps taken in the flow
         1. Note that you can see the path that the call took, input variables, output variables, and events
