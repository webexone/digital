---
title: 'Lab 2: Email Configuration'
author: Dave Easton, Karthik Sundaram
date: 2023-10-04
layout: post
---

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
      + [Lab Objective](#lab-objective)
      + [Prerequisite](#prerequisite)
      + [Quick Links](#quick-links)
- [Lab Section](#lab-section)
      + [Configuration Order](#configuration-order)
   * [Step 1. Gmail account configuration](#step-1-gmail-account-configuration)
      + [1. Gmail forwarding activation (for incoming emails)](#1-gmail-forwarding-activation-for-incoming-emails)
      + [2. Create a project at Google API Console](#2-create-a-project-at-google-api-console)
      + [3. Enable Gmail API (for outgoing emails)](#3-enable-gmail-api-for-outgoing-emails)
      + [4. Configure OAuth Consent Screen and Scopes](#4-configure-oauth-consent-screen-and-scopes)
      + [5. Credentials and authentication with OAuth 2.0](#5-credentials-and-authentication-with-oauth-20)
   * [Step 2. Create Email Asset and Register to Webex CC](#step-2-create-email-asset-and-register-to-webex-cc)
      + [1. Create Email Asset](#1-create-email-asset)
   * [Step 3. Email Entry Point and Queue creation](#step-3-email-entry-point-and-queue-creation)
      + [1. Create Entry Point in Management Portal](#1-create-entry-point-in-management-portal)
      + [2. Create 2 Queues in Management Portal](#2-create-2-queues-in-management-portal)
   * [Step 4. Create/Upload Email flow & verify Gmail account forwarding](#step-4-createupload-email-flow-verify-gmail-account-forwarding)
      + [1. Add forwarding Address Gmail Account and confirm the forwarding with URL from your email debug logs](#1-add-forwarding-address-gmail-account-and-confirm-the-forwarding-with-url-from-your-email-debug-logs)
   * [Step 5. Verification: Send an Email and accept the task](#step-5-verification-send-an-email-and-accept-the-task)
   


# Introduction

### Lab Objective

In this Lab, we will go through the tasks that are required to complete the basic email configuration. You will be able to initiate an email to the Contact Center and be able to accept/respond to the email by logging in as an agent.

In this lab you will be configuring **Gmail** Account settings, Email Assets, Entry Point and corresponding workflows. All those steps are required for connecting the Email account with our application.

### Prerequisite

1. You received an admin credentials to configure in Management Portal and Webex Connect.
2. You have created a Gmail account or have an existing gmail account you can use
3. Lab1 Preconfiguration has been completed

**Preconfiguration**.

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Portal: **[https://portal.wxcc-us1.cisco.com/portal](https://portal.wxcc-us1.cisco.com/portal){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\
> Gmail: **[https://mail.google.com](https://mail.google.com){:target="\_blank"}**\
> Workflows: **[GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels){:target="\_blank"}**\
> Webex Connect: **[https://labtenant.us.webexconnect.io](https://labtenant.us.webexconnect.io){:target="\_blank"}**\

# Lab Section

### Configuration Order

<img align="middle" src="/digital/assets/images/Lab2_ConfigOrder.png" width="1000" />
<br/>
<br/>

## Step 1. Gmail account configuration

Starting May 30, 2022 the **Less Secure Apps** feature was disabled on all Google accounts. As long as this setting was enabled, it was possible to send emails via Gmail SMTP. In this lab, we will be using new OAuth 2.0 authentication for outbound email functionality.

> **Note**: For this lab, we have created a Gmail account. Optionally, use your own account for polling and handling the emails. It can be a Gmail account or Office 365 account or any account which has email forwarding. The instructions below are applicable only for the Gmail accounts.

### 1. Gmail forwarding activation (for incoming emails)

| **User email**                                                       |
| -------------------------------------------------------------------- |
| **Use your own existing gmail account or create a new one for this lab.** You can create a new gmail address and not provide a cellphone number or recovery email address. It takes only a minute to create one. |

- Login to the Gmail account. If this is your firtst login, select **Turn off smart features**. To turn off Smart Features on an existing account, click the gear icon in top right corner (Optionally, click `See all Settings`) and scroll down in the General tab and uncheck the box next to **Smart Features and personalization**

<img align="middle" src="/digital/assets/new_images/LAB2_email/01.TurnOffSmartFeatures.png" width="1000" />
<br/>
<br/>


- Enable POP3/IMAP setting by clicking on settings icon on top right corner and selecting **See all settings**.

<img align="middle" src="/digital/assets/images/Lab2_Gmail1.png" width="1000" />
<br/>
<br/>

- Now Click on **Forwarding and POP/IMAP**, enable the `POP Download` and `IMAP access` then click **Save Changes**.

<img align="middle" src="/digital/assets/images/Lab2_Gmail2.png" width="1000" />
<br/>
<br/>

### 2. Create a project at Google API Console

We need to activate the API if we want to use a Gmail accont for outbound email.

- Login to [Google Developers Console](https://console.developers.google.com/){:target="\_blank"} with your Gmail credentials.

- You will have to agree with the Terms of Service and pick their Country of residence. Then click **Select a project** and create a **NEW PROJECT**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_2_google_console_new_project_png" width="1000" />
<br/>
<br/>

- Keep the default project's name and press **Create** at the bottom. Make sure that now you have selected this project.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_3_google_console_proj_name_png" width="1000" />
<br/>
<br/>

### 3. Enable Gmail API (for outgoing emails)

- Enter `Gmail API` in the search bar and click on it once found.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_4_google_console_gmail_API_png" width="1000" />
<br/>
<br/>

- You need to enable the API for your project by clickin **ENABLE** button.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_5_google_console_gmail_API_enable_png" width="1000" />
<br/>
<br/>

### 4. Configure OAuth Consent Screen and Scopes

- Once the API is enabled, you’ll be taken to a nice dashboard that says, `"To use this API, you may need credentials"`.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_6_google_console_gmail_API_may_need_creds_png" width="1000" />
<br/>
<br/>

- To create an OAuth client ID, you must first configure your consent screen. Under the APIs and Services section, click on **OAuth Consent Screen**, set the user type as `External` and click **CREATE** button.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_7_google_console_oauth_external_png" width="1000" />
<br/>
<br/>

- It will bring you to a page with many fields. Just enter the **App name** as `WebexApp`, choose your **User support email** and enter the same email in the **Developer contact information**. In the end press **SAVE AND CONTINUE**.

<img align="middle" src="/digital/assets/new_images/LAB2_email/02.ManyFields.png" width="1000" />
<br/>
<br/>

- On the next screen, you need to provide Auth 2.0 Scopes for Google APIs. Click the **Add Or Remove Scopes** button and add **https://www.googleapis.com/auth/gmail.send** to the list of scopes since we only want to send emails from Gmail and not read any user data. Click **SAVE AND CONTINUE**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_9_google_console_scopes_png" width="1000" />
<br/>
<br/>

- On the test user page, click **ADD USERS** and enter your gmail address. Click **Save and Continue**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_91_google_console_test_user_png" width="1000" />
<br/>
<br/>

### 5. Credentials and authentication with OAuth 2.0

Now create a new client ID that will be used to identify your application to Google’s OAuth servers.

- In the APIs & Services section, click on **Credentials** and then pick **OAuth client ID** from the drop-down list of the **CREATE CREDENTIALS** button.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_92_google_console_oauth_client_ID_png" width="1000" />
<br/>
<br/>

- Select `Web application` in the **Application type**

- You can leave the default name. The name of your OAuth 2.0 client is only used to identify the client in the Google Cloud console and will not be shown to application users.

- In the **Authorized redirect URIs** section click **ADD URI** button and set `https://labtenant.us.webexconnect.io/callback`. Click **CREATE** button in the end.

<img align="middle" src="/digital/assets/new_images/LAB2_email/03.CallbackURLCorrected.png" width="1000" />
<br/>
<br/>

- Download a JSON file with your credentials – you’ll need it later.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_931_google_console_json_png" width="1000" />
<br/>
<br/>

## Step 2. Create Email Asset and Register to Webex CC

### 1. Create Email Asset

- As an admin, login to Webex Connect UI using the provided URL [https://labtenant.us.webexconnect.io/](https://labtenant.us.webexconnect.io/)

- Select **Assets** -> **Apps** -> **CONFIGURE NEW APP** -> **Email**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\lab2_94_create_email_app_gif" width="1000" />
<br/>
<br/>

- Set the settings according to the table below:

| **Entity**          | **Name**                                                            |
| ------------------- | ------------------------------------------------------------------- |
| Asset Name          | EmailAsset0XX where <0XX> is your 3-digit Lab ID  (NOTE: underscore not permitted)             |
| Email ID            | Your gmail address here                                             |
| Authentication Type | OAuth 2.0                                                           |
| SMTP Server         | smtp.gmail.com                                                      |
| Username            | Your gmail address here                                             |
| Port                | 465                                                                 |
| Security            | SSL                                                                 |
| Client ID           | \<client_id from JSON file\>                                        |
| client Secret       | \<client_secret from JSON file\>                                    |
| Authorization URL   | https://accounts.google.com/o/oauth2/auth                           |
| Scope               | https://mail.google.com/ https://www.googleapis.com/auth/gmail.send |
| Access Token URL    | https://oauth2.googleapis.com/token                                 |
| Refresh Token URL   | https://oauth2.googleapis.com/token                                 |

> where \<ID\> is your Lab ID

- Click **GENERATE TOKEN** and follow the step on the screenshot:

<img align="middle" src="/digital/assets/new_images\LAB2_email\lab2_95_generate_token_gif" width="1000" />
<br/>
<br/>

- Verify that the **ACCESS TOKEN** and **REFRESH TOKEN** are generated and click **SAVE**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_96_email_app_save_tokens_png" width="1000" />
<br/>
<br/>

- Click on **REGISTER TO Engage** and Select the service **My First Service_0XX**. In the end click **REGISTER**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\lab2_97_register_to_engage_gif" width="1000" />
<br/>
<br/>

**NOTE:** If clicking on **Register to Engage** doesn't do anything, please contact your lab proctor to perform this step for you

## Step 3. Email Entry Point and Queue creation

### 1. Create Entry Point in Management Portal

Portal: **[https://portal.wxcc-us1.cisco.com/portal](https://portal.wxcc-us1.cisco.com/portal){:target="\_blank"}**\

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Entry Point_**.

- Click on `New Entry Point`.

- Input **_Name_** as `Email_EP_0XX where 0XX is your 3-digit lab ID`.

- Select `Email` in the **_Channel Type_** section.

- Leave the **_Asset Name_** as appered value `EmailASSET0XX`.

- Set **_Service Level Threshold_** as `2` hours.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="/digital/assets/new_images/LAB2_email/Lab2_Email_0XX.png" width="1000" />

<br/>
<br/>

### 2. Create 2 Queues in Management Portal

- Click on **_Provisioning_** and select **_Entry Points/Queues_** > **_Queue_**.

- Click on `New Queue`.

- Input **_Name_** as `Email_Q_0XX` where 0XX is your 3-digit Lab ID.

- Select `Email` in the **_Channel Type_** section.

- Leave the **_Queue Routing Type_** as default value `Longest Available Agent`.

- In the **_Email Distribution_** click on **Add Group** and select `Team1_0XX` where 0XX is your 3-digit Lab ID.

- Set **_Service Level Threshold_** as `2` hours.

- Set **_Maximum Time in Queue_** as `3` hours.

- The **_Time Zone_** can stay as default value.

- Click on **Save** after comparing your values with the screenshot below.

<img align="middle" src="/digital/assets/images/Lab2_Email_Q.png" width="1000" />
<br/>
<br/>

- Create a second queue by repeating the same steps as above.

- Input **_Name_** as `Email_Q2_0XX`.

- Select `Email` in the **_Channel Type_** section.

- In the the **_Email Distribution_** click on **Add Group** and select `Team2_0XX`.

<img align="middle" src="/digital/assets/images/Lab2_Email_Q2.png" width="1000" />
<br/>
<br/>

## Step 4. Create/Upload Email flow & verify Gmail account forwarding


- Go to **Assets** -> **Apps** -> Locate your Email asset `EmailAsset0XX` and copy and save the **Forwarding Address** somewhere to use in a subsequent step

<img align="middle" src="/digital/assets/new_images\LAB2_email/95_copy_bizemailid.jpg" width="1000" />
<br/>
<br/>

- Download the email flow from the [GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels/tree/main/Webex%20Connect%20Flows/v3.0/Template/Event%20Handling%20Workflows)

- Navigate to **webex connect flows -> 3.0 -> template -> media specific workflows -> email inbound flow.workflow.zip**, select the zip file and click download.

- Unzip the downloaded file.

- Go to Webex Connect, click on **Services** and select the service in which the Asset is created in step 2. It should be **My First Service_0XX**

- In the service click on **FLOWS** -> **CREATE FLOW** .

- Enter the **FLOW NAME** as **Email Inbound Flow**, select the **TYPE** as **Work Flow** and under **METHOD** select **Upload a flow**.

- Drag and drop the **Email Inbound Flow.workflow** flow that is downloaded in zip file, click **CREATE** and then click **SAVE**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_98_create_email_flow_png" width="1000" />
<br/>
<br/>

- Click **Save** and in the created workflow find the **Queue Task**, click twice, select the **QUEUE NAME** as **Email_Q1_0XX** and click on **SAVE**.

<img align="middle" src="/digital/assets/new_images\LAB2_email\Lab2_99_email_Qtask_node_png" width="1000" />
<br/>
<br/>


- Click **Settings** on top right corner and switch to **Custom variables** tab. Here in the **bizemailid** row, update the default value with the forwarding address you copied from your email asset earlier in step 2. Click SAVE Click **SAVE**.

<img align="middle" src="/digital/assets/new_images/LAB2_email/04.bizemailID.png" width="1000" />
<br/>
<br/>

When prompted, turn on descriptive logs and enter `1000`` in the **minutes** field and click **SAVE**

<img align="middle" src="/digital/assets/new_images/LAB2_email/05.logMinutes.png" width="1000" />
<br/>
<br/>

- Finally click on Make Live on top right corner -> Select the email Application/Asset (`EmailAsset0XX`) that we have created and click Make Live.

<img align="middle" src="/digital/assets/images/Lab2_WF4.png" width="1000" />
<br/>
<br/>

Wait approximately 2 minutes to make sure your flow shows LIVE before proceeding with the next steps.  

<img align="middle" src="/digital/assets/new_images/LAB2_email/06.MakeLive.png" width="1000" />
<br/>
<br/>


### 1. Add forwarding Address Gmail Account and confirm the forwarding with URL from your email debug logs

- Using the the forwarding address from your email asset in the previous step , go back to your gmail account.

<img align="middle" src="/digital/assets/images/Lab2_Assest4.png" width="1000" />
<br/>
<br/>

- In your Gmail account click on settings icon on top right corner -> Select **See all settings**.

<img align="middle" src="/digital/assets/images/Lab2_Gmail1.png" width="1000" />
<br/>
<br/>

- Click on **Forwarding and POP/IMAP** -> click on **Add a forwarding address** -> Paste the copied forwarding address from the created asset. Then click on **Next**. In a new pop up tab click **Proceed** and then click **OK** when it prompts.

<img align="middle" src="/digital/assets/images/Lab2_Gmail6.gif" width="1000" />
<br/>
<br/>

In order to fetch the confirmation email, go back to Webex Connect and click on the **Debug Console** Menu on the left pane, select `Query Historical Logs` – `Channel = Email` – `Date Range = Today/Last Hour`.  Click the **Search** button.  

<img align="middle" src="/digital/assets/new_images/LAB2_email/DebugConsole3.png" width="1000" />
<br/>
<br/>

- You should only have 1 transaction in your logs at this point.  Click the **Message ID** Link for `Event Handled`

<img align="middle" src="/digital/assets/new_images/LAB2_email/OneTransaction.png" width="1000" />
<br/>
<br/>

- Click the **decrypt logs** button, then click the **Trace Details** link for that transaction. Click the **copy** button next to the Data entry in the lower right pane.  

<img align="middle" src="/digital/assets/new_images/LAB2_email/email_copy debug.gif" width="1000" />
<br/>
<br/>

- Paste the copied data from the debug logs into the empty field below and press the Get URL button.  This will pull out the forwarding verification URL that google sent you.  

<textarea id="jsonETL" style="width: 1352px; height: 96px;">Delete this text and enter copied text here</textarea>
<button onclick="update()">Get URL</button>
<script>
    function update(){
        x = JSON.parse(document.getElementById("jsonETL").value);
        document.getElementById("jsonETL").value = x["email.message"].replaceAll("\\r\\n","\r\n").replaceAll("\\/","/").substring(x["email.message"].replaceAll("\\r\\n","\r\n").replaceAll("\\/","/").search("http"),x["email.message"].replaceAll("\\r\\n","\r\n").replaceAll("\\/","/").search("Ifyouclick|If you click")).trim()
    }
</script>

- Paste the URL into a new browser tab and hit **Enter**.  Click the **Confirm** button to OK the forwarding.

<img align="middle" src="/digital/assets/new_images/LAB2_email/email_paste debug.gif" width="1000" />
<br/>
<br/>

- You will get a confirmation message

<img align="middle" src="/digital/assets/new_images/LAB2_email/emailConfirmation.png" width="1000" />
<br/>
<br/>

- Back in the settings of your Gmail account, forwarding should be reflected in the Forwarding and POP/IMAP tab.

<img align="middle" src="/digital/assets/new_images/LAB2_email/CheckPopSetting.png" width="1000" />
<br/>
<br/>

- Last forwarding step: open your email flow and click the **Edit** button top right corner, then click the settings **gear icon** and click the `Custom Variables`` tab inside the Flow Settings box. Replace the **bizemailid** variable with **your Gmail address.** Save the settings, then click **Make Live** to publish your flow.

<img align="middle" src="/digital/assets/new_images/LAB2_email/bizemailid.png" width="1000" />
<br/>
<br/>

[To the top of this lab](#table-of-contents)

## Step 5. Verification: Send an Email and accept the task

- Go to personal email account and send an email to the support email address that was initially configured in the Email Asset.

- Go to the Agent Desktop and make the agent Available.

<img align="middle" src="/digital/assets/images/Lab2_Agent1.png" width="1000" />
<br/>
<br/>

- The Email will be offered to the agent. Click **Accept** to handle the email. Click "Reply" or Reply All" to the email and hit send button.

<img align="middle" src="/digital/assets/new_images/LAB2_email/Lab2__991_email_reply_in_agent_desktop_png" width="1000" />
<br/>
<br/>

- Add wrap up and close the task.

### Congratulations, you have completed this section!


