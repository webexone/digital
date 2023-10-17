---
title: 'Lab 3: Live Chat Configuration'
author: Dave Easton, Karthik Sundaram
date: 2023-10-04
layout: post
---

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
  - [Lab Objective](#lab-objective)
  - [Pre-requisite](#pre-requisite)
  - [Quick Links](#quick-links)
- [Lab Section](#lab-section)
  - [Step 1. Live Chat Asset creation & register to Webex Engage](#step-1-live-chat-asset-creation--register-to-webex-cc)
  - [Step 2. Chat Template creation for website integration](#step-2-chat-template-creation-for-website-integration)
  - [Step 3. Chat Entry Point and Queue creation](#step-3-chat-entry-point-and-queue-creation)
    - [1. Create Entry Point in Management Portal](#1-create-entry-point-in-management-portal)
    - [2. Create Queue in Management Portal](#2-create-queue-in-management-portal)
    - [3. Skill and Skill profile](#3-skill-and-skill-profile)
  - [Step 4. Website Settings](#step-4-website-settings)
    - [1. Configure Live Chat widget](#1-configure-live-chat-widget)
    - [2. Verify that live chat widget loads](#2-verify-that-live-chat-widget-loads)
  - [Step 5. Quick response template creation](#step-5-quick-response-template-creation)
  - [Step 6. Create/Upload Live Chat flow](#step-6-createupload-live-chat-flow)
    - [1. Initial flow loading](#1-initial-flow-loading)
    - [2. Start node and Custom Variables](#2-start-node-and-custom-variables)
    - [3. Select Live Chat form](#3-select-live-chat-form)
    - [4. Edit Queue Task node](#4-edit-queue-task-node)
  - [Step 7. Verification - start live chat and accept the request](#step-7-verification---start-live-chat-and-accept-the-request)
  - [Step 8. Search and view conversation transcripts](#step-8-search-and-view-conversation-transcripts)
  - [Step 9. Challenge Lab - Enhance flow](#step-9-challenge-lab---enhance-flow)
    - [1. Add Branch to handle Dropdown form field](#1-add-branch-to-handle-dropdown-form-field)
  - [Back to top](#back-to-top)
    - [Congratulations, you have completed this section!](#congratulations-you-have-completed-this-section)

# Introduction

### Lab Objective

In this Lab, we will go through the tasks that are required to complete a basic Live chat integration. You will be able to initiate a Chat contact to the Contact Center from a sample website and be able to accept/respond to the contact by logging in as an agent.

In this lab you will be configuring the Service, Chat Assets, Entry Point, Queue, Chat Template, Website Settings, and corresponding workflows.

### Pre-requisite

1. You received an admin credentials to configure in Management Portal and Webex Connect.
2. You have successfully completed the previous Lab **Preconfiguration**

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Portal: **[https://portal.wxcc-us1.cisco.com/portal](https://portal.wxcc-us1.cisco.com/portal){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\
> Workflows: **[GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels/tree/main/Webex%20Connect%20Flows/v3.0/Template/Event%20Handling%20Workflows){:target="\_blank"}**\
> Connect: **[https://labtenant.us.webexconnect.io](https://labtenant.us.webexconnect.io){:target="\_blank"}**\

# Lab Section

## Step 1. Live Chat Asset creation & register to Webex Engage

- Login to your respective Webex Connect UI using the provided URL [https://labtenant.us.webexconnect.io](https://labtenant.us.webexconnect.io){:target="\_blank"}\

- Navigate to `Assets` > `Apps` > `Configure New App` > `Mobile / Web`

<img align="middle" src="/digital/assets/images/Lab3_1.gif" width="1000" />
<br/>
<br/>

- Name your asset `LiveChatAsset_0XX` where 0XX is your 3-digit Lab ID

- Toggle/Enable `Live Chat / In-AppMessaging` to "ON" and choose `PRIMARY TRANSPORT PROTOCOL` as MQTT" & `SECONDARY TRANSPORT PROTOCOL` as Web Socket" and enable `Use Secured Port` and `SAVE`.

<img align="middle" src="/digital/assets/images/Lab3_2.jpg" width="700" />
<br/>
<br/>

- Select `REGISTER TO WEBEX Engage` and choose the Service you have created and REGISTER

<img align="middle" src="/digital/assets/new_images/Lab3_chat/lab3_1_register_app_to_webex_engage_png" width="1000" />
<br/>
<br/>

- In the resulting window, select a service under which this asset would be managed. This service will be Service_0XX you created in the prior steps

<img align="middle" src="/digital/assets/new_images\Lab3_chat\lab3_2_register_app_to_service_png" width="600" />
<br/>
<br/>

- Verify that the `Register to Webex Engage` option is now disabled and there is a message indicating the time when the asset was registered along with the service to which it is assigned.

<img align="middle" src="/digital/assets/new_images/Lab3_chat/lab3_3_confirm_register_app_to_service_png" width="1000" />
<br/>
<br/>

- Click the back arrow next to go back to the list of Apps. Then take note of the Application ID (App ID). We will need this later so please copy this ID somewhere handy like a text file or take note of it.

<img align="middle" src="/digital/assets/images/Lab3_33.jpg" width="600" />
<br/>
<br/>

[To the top of this lab](#table-of-contents)

## Step 2. Chat Template creation for website integration

- Creating a chat template allows you to configure a pre-defined chat form that will presented to the customer. Data points can be collected from the customer in a chat-like interface.

- From Webex Connect interface, go to `TOOLS` > `Templates` then click on `Add New Template`

<img align="middle" src="/digital/assets/images/Lab3_8.jpg" width="200" />
<br/>
<br/>

- Name your template `ChatTemplate_0XX` where <0XX> is your 3 digit Lab ID. Choose Channel as `Live Chat / In-App Messaging`

- Message Type as `Form`

- Provide the Title as `Welcome to Webex CC Live Chat` or some other message.

<img align="middle" src="/digital/assets/images/Lab3_9.jpg" width="1000" />
<br/>
<br/>

- We will be adding the form fields now. Firstly the Name. Click on `Add field` and then fill in the details as per the screenshot

<img align="middle" src="/digital/assets/images/Lab3_10.jpg" width="600" />
<br/>
<br/>

-Continue by adding the `Email` and `Reason` fields in the same manner with the info in this table.

| Type     | Name        | Label                    | Mandatory Field |
| -------- | ----------- | ------------------------ | --------------- |
| Name     | Name        | Name                     | true            |
| Email    | Email       | Email                    | true            |
| Dropdown | Reason      | Reason for Contacting Us | true            |
| Text     | Description | Description              | false           |

Here is a screenshot of the Dropdown configuration with 2 options, one for **Sales** and one for **Support**. We will use this later to perform Skills Based Routing so chats are routed to most skilled agents.

<img align="middle" src="/digital/assets/images/Lab3_11.jpg" width="600" />
<br/>
<br/>

- Finally click `SAVE`

<img align="middle" src="/digital/assets/images/Lab3_12.jpg" width="1000" />
<br/>
<br/>

[To the top of this lab](#table-of-contents)

## Step 3. Chat Entry Point and Queue creation

### 1. Create Entry Point in Management Portal

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Entry Point_**.

- Click on `New Entry Point`.

- Input **_Name_** as `Chat_EP_0XX` where <0XX> is your 3-digit lab ID

- Select `Chat` in the **_Channel Type_** section.

- Leave the **_Asset Name_** as the configured value earlier.

- Set **_Service Level Threshold_** as `300` seconds.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="/digital/assets/images/Lab3_6.jpg" width="800" />
<br/>
<br/>

### 2. Create Queue in Management Portal

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Queue_**.

- Click on `New Queue`.

- Input **_Name_** as `Chat_Q_SBR_0XX` where <0XX> is your 3-digit lab ID

- Select `Chat` in the **_Channel Type_** section.

- Select **_Queue Routing Type_** as `Skills Based`.

- Set **_Agent Selection_** as `Best Available Agent`

- In the the **_Chat Distribution_** click on **Add Group** and select `Team1`.

- Set **_Service Level Threshold_** as `90` seconds.

- Set **_Maximum Time in Queue_** as `600` seconds.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="/digital/assets/images/Lab3_7.jpg" width="800" />
<br/>
<br/>

### 3. Skill and Skill profile

- We are now going to configure skills and skill profiles for the skills based Queue Click on **_Provisioning_** and select **_Skills_** > **_Skill Definition_**.

- Click on `New Skill Definition`

- Set **_Name_** as `Sales_0XX` where 0XX is your 3-digit lab ID

- Set **_Service Level Threshold_** as `60` seconds.

- Set **_Type_** as Boolean.

- Click on **Save**

<img align="middle" src="/digital/assets/images/Lab3_27.jpg" width="600" />
<br/>
<br/>

- Create another Skill definition of same type `Boolean` with **_Name_** as `Support_0XX`

<img align="middle" src="/digital/assets/images/Lab3_28.jpg" width="600" />
<br/>
<br/>

- Next we'll create 2 Skill profiles, one for Sales and one for Support. Click on **_Provisioning_** and select **_Skills_** > **_Skill Profile_**.

- Click on `New Skill Profile`

- Set **_Name_** as `Sales_0XX` where <0XX> is your 3-digit lab ID

- Select the `Sales_0XX` Skill and set the **_Skill Value_** to `True`

- Select the `Support_0XX` Skill and set the **_Skill Value_** to `False`

- Click on **Save**

<img align="middle" src="/digital/assets/images/Lab3_29.jpg" width="600" />
<br/>
<br/>

- Create another Skill Profile with Name `Support_0XX` with `Sales_0XX` skill value to False and Support skill value to True

<img align="middle" src="/digital/assets/images/Lab3_30.jpg" width="600" />
<br/>
<br/>

- Finally we'll assign the Sales Skill profile to our agent. Click on **_Provisioning_** and select **_Users_**

- Edit the Agent user created earlier by clicking on the 3 dotted menu

<img align="middle" src="/digital/assets/images/Lab3_31.jpg" width="600" />
<br/>
<br/>

- In the agent settings, Select `Skill Profile_0XX` as `Sales_0XX` and click **Save**

<img align="middle" src="/digital/assets/new_images/Lab3_chat/lab3_4_assign_agent_skill_profile_png" width="600" />
<br/>
<br/>

[To the top of this lab](#table-of-contents)

## Step 4. Website Settings

### 1. Configure Live Chat widget

- From Management Portal, access the menu and cross launch **New Digital Channels Admin Portal** by choosing `New Digital Channels`

<img align="middle" src="/digital/assets/images/Lab3_13.jpg" width="400" />
<br/>
<br/>

- Go to `Assets` > search and edit the chat asset which we created earlier in **Step 1**

<img align="middle" src="/digital/assets/images/Lab3_14.jpg" width="400" />
<br/>
<br/>

- Scroll down and click the pencil icon under the Action menu

<img align="middle" src="/digital/assets/new_images/Lab3_chat/01.ActionMenu.png" width="1000" />
<br/>
<br/>

- Scroll to top of the page and choose `Websites` and then click `Add Website`

<img align="middle" src="/digital/assets/images/Lab3_16.jpg" width="1000" />
<br/>
<br/>

- Enter the respective fields as per Screenshots below. Note we are going to insert the chat bubble into an online HTML editor called `glitch.me`. The `Domain` field should contain the domain where you will insert the chat bubble.

<img align="middle" src="/digital/assets/new_images/Lab3_chat/02.glitchMe" width="1000" />
<br/>
<br/>

- Take a moment to explore the rest of the customization options for the chat bubble and then click `SAVE CHANGES`

- Scroll up, select the `Appearance` tab and change the settings (Widget Color, Logo, Emojis, attachments etc.;) as per your requirement and `SAVE CHANGES`

- Select the `Widget Visibility` tab and click on `Show without restriction` and `SAVE CHANGES`

<img align="middle" src="/digital/assets/images/Lab3_26.jpg" width="1000" />
<br/>
<br/>

- Explore the `Banned Customers` tab so you are familiar with the settings but we are not going to change the default settings for those at this point

### 2. Verify that live chat widget loads

- There's still a few bits to configure but we can now verify that the live chat widget loads.
- Go to Webex Connect Engage portal, select Installation tab and Copy the chat script code.

<img align="middle" src="/digital/assets/images/Lab3_18.jpg" width="1000" />
<br/>
<br/>

- Open a new tab in your browser and navigate to [Glitch.com](https://www.glitch.com){:target="\_blank"}.

- You must create an account at glitch.com in order to use their html test tool.
You may login with an existing Facebook,Google or Github account, or use a magic link.  

<img align="middle" src="/digital/assets/new_images/Lab3_chat/03.GlitchLogin.png" width="1000" />
<br/>
<br/>

-	Once you are logged in, click the **New Project** Button and select `glitch-hello-website` from the menu

<img align="middle" src="/digital/assets/new_images/Lab3_chat/04.GlitchNewProject.png" width="1000" />
<br/>
<br/>

<img align="middle" src="/digital/assets/new_images/Lab3_chat/05.GlitchNewProject2.png" width="1000" />
<br/>
<br/>

The name of your new glitch project will appear in the top left menu (in this example it is plump-tame-pumpkin).  Your website will be accessible from glitch.me with that suffix later if you need it.  Click on the `index.html` link under the Files menu 

<img align="middle" src="/digital/assets/new_images/Lab3_chat/06.GlitchIndex.png" width="1000" />
<br/>
<br/>

-	Delete everything between the `<body>` and `</body>` takes in the index file. This is where you will paste your chat bubble code from Engage.  

-	Click the **Preview** button in the lower browser bar and select `Preview in New Window`.  Verify that the Live Chat bubble pops up in the lower right corner and that your widget loads correctly. 

<img align="middle" src="/digital/assets/new_images/Lab3_chat/07.GlitchPreview.gif" width="1000" />
<br/>
<br/>

[To the top of this lab](#table-of-contents)

## Step 5. Quick response template creation

- This section applies to all channels, not just Live chat. You can preset quick responses that agents can use when they respond to customer queries. You can set up the responses in Templates, and group them in a Template Group to organize the content and make the templates easier to find. We'll configure some so you can test them in all the successive lab exercises

- Go to `Assets` > `Templates` and click the + icon besides Template Groups table header.

<img align="middle" src="/digital/assets/new_images/Lab3_chat/08.TemplateGroup.png" width="1000" />
<br/>
<br/>


- You can choose to create a common template for all channels or create channel-specific templates. We will create a common template but also feel free to create other channel specific templates. Channel specific templates will only be shown to the agent when they receive a contact from that channel. Click `Add Template` button at the top right

<img align="middle" src="/digital/assets/images/Lab3_49.jpg" width="1000" />
<br/>
<br/>

- Enter the template name in the `Template ID` field.

- Enter the template text in the `Template Text` field. You can use variables by typing `@@` and also custom fields between chevron brackets `<>`. Variables will be autopopulated based on the active task and custom fields will be editable even if the template is locked. You can use the example on the screenshot or some other text.


<img align="middle" src="/digital/assets/images/Lab3_50.jpg" width="1000" />
<br/>
<br/>

- To exclude other teams from sharing this template, choose them from the `Teams excluded` drop down box.   For this lab, leave this field blank.

- Click `SAVE CHANGES`

<img align="middle" src="/digital/assets/new_images/Lab3_chat/09.UploadTemplate.png" width="1000" />
<br/>
<br/>



## Step 6. Create/Upload Live Chat flow

### 1. Initial flow loading

- Download the default inbound chat flow from the [GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels){:target="\_blank"}.

- Navigate to **webex connect flows** -> **v3.0** -> **template** -> **media specific workflows** -> **Live Chat inbound flow.workflow.zip**, select the zip file and click download.

- Unzip the downloaded file.

- Go to Webex Connect, click on **Services** and select `Service_0XX` in which your asset `Asset_0XX`` is created in step 2. It should be **My First Service**

- In the service click on **FLOWS** -> **CREATE FLOW** .

<img align="middle" src="/digital/assets/images/Lab3_19.jpg" width="1000" />
<br/>
<br/>

- Enter the **FLOW NAME** as **Live Chat Inbound Flow**, select the **TYPE** as **Work Flow** and under **METHOD** select **Upload a flow**.

- Drag and drop the **Live Chat Inbound Flow.workflow** flow file that you unzipped, click **CREATE** and then click **SAVE**.

<img align="middle" src="/digital/assets/images/Lab3_20.jpg" width="1000" />
<br/>
<br/>

### 2. Start node and Custom Variables

- A page will load with the imported workflow. We must make some changes to the default inbound flow based on our setup.

- First Click `Save` in the `Configure APP Event` page that loaded, this defines what will trigger the flow and the default settings are already good.

<img align="middle" src="/digital/assets/images/Lab3_21.jpg" width="1000" />
<br/>
<br/>

- Click on the gear button on the top right to load the flow settings dialog

<img align="middle" src="/digital/assets/images/Lab3_34.jpg" width="600" />
<br/>
<br/>

- Select the Custom Variables tab and set the following variable defaults:

_domain_: Set it to `*.glitch.me` (if this field is not present, move on)

_liveChatDomain_: Set it to `*.glitch.me*`

_appID_: this will be the APP ID of your chat asset created earlier

<img align="middle" src="/digital/assets/new_images/Lab3_chat/10.FlowSettings.png" width="1000" />
<br/>
<br/>


<img align="middle" src="/digital/assets/new_images/Lab3_chat/lab3_8_chat_flow_cust_var_1_png" width="1000" />
<br/>
<br/>

- In your production setup domain should be set to your website's domain

### 3. Select Live Chat form

- We must select the right Live Chat Template as configured earlier so that the right Form is presented to the customer. Click on the `Pre-chat form` node and select `Form Template` as configured earlier and `Save`

<img align="middle" src="/digital/assets/new_images/Lab3_chat/lab3_9_select_pre_chat_template_gif" width="1000" />
<br/>
<br/>

3. The same must be done in the Receive node, double click on it and select the Form from the dropdown menu and `Save`

<img align="middle" src="/digital/assets/new_images/Lab3_chat/lab3_91_select_pre_chat_template_receive_node_gif" width="1000" />
<br/>
<br/>

### 4. Edit Queue Task node

- In the created workflow find the **Queue Task**, click twice, select the **QUEUE NAME** as **Chat_Q_SBR_0XX** and add Skill requirement for Sales_0XX to be True and click on **SAVE**.

<img align="middle" src="/digital/assets/images/Lab3_36.jpg" width="1000" />
<br/>
<br/>

- Finally click on Make Live on top right corner -> Under Application select LiveChatAsset_0XX that corresponds to your Lab ID and click `Make Live`.

<img align="middle" src="/digital/assets/new_images/Lab3_chat/lab3_92_chat_flow_make_live_png" width="1000" />
<br/>
<br/>

- Wait for 2 minutes and verify that the flow is published successfully.

<img align="middle" src="/digital/assets/images/Lab3_38.jpg" width="1000" />
<br/>
<br/>

[To the top of this lab](#table-of-contents)

## Step 7. Verification - start live chat and accept the request

- Open a new tab and login to the Agent Desktop and make the agent Available (if you haven't done already in Lab2).

<img align="middle" src="/digital/assets/images/Lab2_Agent1.png" width="1000" />
<br/>
<br/>

- Go back to the tab where you opened `glitch.com` project and pasted the live chat widget code.

-	Click your chat bubble to initiate the chat. Fill out the form with your options. You will see `message successfully queued` when the message enters your chat queue.  

<img align="middle" src="/digital/assets/new_images/Lab3_chat/12.LiveChat.gif" width="1000" />
<br/>
<br/>

- The Live Chat will be offered to the agent. Click **Accept** to handle the Chat

<img align="middle" src="/digital/assets/new_images/Lab3_chat/13.LiveChatOffer.png" width="1000" />
<br/>
<br/>

- The form submission will be presented to the customer

<img align="middle" src="/digital/assets/new_images/Lab3_chat/14.FormPresented.png" width="1000" />
<br/>
<br/>

- Type a response and hit send button.

<img align="middle" src="/digital/assets/new_images/Lab3_chat/15.TypeAResponse.png" width="1000" />
<br/>
<br/>

- Make sure you test the Predefined Quick Response templates we created earlier in Step 5

<img align="middle" src="/digital/assets/images/Lab3_53.jpg" width="700" />

- End the contact

<img align="middle" src="/digital/assets/new_images/Lab3_chat/16.EndContact.png" width="1000" />
<br/>
<br/>

- Add wrap up and close the task.

<img align="middle" src="/digital/assets/images/Lab3_46.jpg" width="400" />
<br/>
<br/>

## Step 8. Search and view conversation transcripts

- You can search and view conversation transcripts from the New Digital Channels Engage interface. Go to the already openned tab or from Management Portal, access the menu and cross launch **New Digital Channels Admin Portal** by choosing `New Digital Channels`. Then click on Switch to Customer Care button at the top right.

<img align="middle" src="../new_images/Lab3_chat/lab3_93_customer_care_png" width="400" />
<br/>
<br/>

- Click on the Search button at the top left

<img align="middle" src="/digital/assets/images/Lab3_55.jpg" width="1000" />
<br/>
<br/>

- You can search for transcripts using many fields depending on the channel. In this case use the Name field and search using the Customer Name used while testing in Step 7. Once the conversation transcript shows up, click on the button in the last column.

<img align="middle" src="/digital/assets/images/Lab3_56.jpg" width="1000" />
<br/>
<br/>

- Conversation transcript will load and you have the option to print as PDF

<img align="middle" src="/digital/assets/images/Lab3_57.jpg" width="500" />
<br/>
<br/>

- On the customer end, they can also access the transcript by emailing it to their personal email account. Once conversation ended, click on the chat bubble hamburger icon and then select `Email transcript` option

<img align="middle" src="/digital/assets/images/Lab3_58.jpg" width="400" />
<br/>
<br/>

- Enter email address to send the transcript to

<img align="middle" src="/digital/assets/images/Lab3_59.jpg" width="400" />
<br/>
<br/>

<img align="middle" src="/digital/assets/images/Lab3_60.jpg" width="400" />
<br/>
<br/>

- Conversation transcript will be received in the following format:

<img align="middle" src="/digital/assets/images/Lab3_61.jpg" width="500" />
<br/>
<br/>

## [Back to top](#table-of-contents)

### Congratulations, you have completed this section!

<script>
function mainPage() {window.location.href = "Home";}
function nextLab()
 {
 window.location.href = "Lab4_FBM";
 }
</script>

<div id="button-row">
<button onclick="mainPage()" style="
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Home Page</button>

<button onclick="nextLab()" style="
  position: absolute;
  right: 200px;
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Go to the Next Lab</button>

</div>
