---
title: 'Lab 10: Bot Configuration'
author: Dave Easton, Karthik Sundaram
date: 2023-10-11
layout: post
---

- [Table of Contents](#table-of-contents)
      + [Introduction](#introduction)
      + [Prerequisite](#prerequisite)
      + [Quick Links](#quick-links)
   * [Step 1. Create new QA Bot in Bot Builder <a name="create-bot"></a>](#step-1-create-new-qa-bot-in-bot-builder)
   * [Step 2. Import a Banking article into your Bot & preview responses <a name="import-preview"></a>](#step-2-import-a-banking-article-into-your-bot-preview-responses)
   * [Step 3. Configure a new chat app in Connect for your Bot <a name="new-chat-app"></a>](#step-3-configure-a-new-chat-app-in-connect-for-your-bot)
   * [Step 4. Assign the bot asset to your Chat EP in WxCC <a name="assign-to-EP"></a>](#step-4-assign-the-bot-asset-to-your-chat-ep-in-wxcc)
   * [Step 5. Configure widget website settings in Engage <a name="configure-engage"></a>](#step-5-configure-widget-website-settings-in-engage)
   * [Step 6. Download bot flow and upload to Connect <a name="bot-flow-upload"></a>](#step-6-download-bot-flow-and-upload-to-connect)
   * [Step 7. Configure the flow to use the QA bot & make it LIVE! <a name="make-live"></a>](#step-7-configure-the-flow-to-use-the-qa-bot-make-it-live)
   * [Step 8. Test the QA bot with an agent <a name="test-QA-bot"></a>](#step-8-test-the-qa-bot-with-an-agent)
   * [Step 9. Customer:  request email of chat transcript <a name="request-transcript"></a>](#step-9-customer-request-email-of-chat-transcript)
   
      


### Introduction

This lab is designed for you to build a small banking Question & Answer bot.  In the lab you will import a banking article that will allow a customer to converse with the bot about their debit card. You will test the article, add a test case, and learn about curation. In the end you will verify the bot can successfully hand the customer off to a human agent.

### Prerequisite

- Preconfiguration of the tenant has been done. 

- You have admin credentials to complete configurations in Webex Contact Center and Webex Connect portals. 

- You have completed Lab 3 – Live Chat and have a working chat app in Connect/Webex CC that includes a chat Entry Point, a chat Queue, and a pre-chat form template. We will re-use all of these in our config steps below.

### Quick Links

> Control Hub: **[https://admin.webex.com](https://admin.webex.com){:target="\_blank"}**\
> Portal: **[https://portal.wxcc-us1.cisco.com/portal](https://portal.wxcc-us1.cisco.com/portal){:target="\_blank"}**\
> Agent Desktop: **[https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}**\
> Workflows: **[GitHub page](https://github.com/CiscoDevNet/webexcc-digital-channels/tree/main/Webex%20Connect%20Flows/v3.0/Template/Event%20Handling%20Workflows){:target="\_blank"}**\
> Connect: **[https://labtenant.us.webexconnect.io](https://labtenant.us.webexconnect.io){:target="\_blank"}**


## Step 1. Create new QA Bot in Bot Builder <a name="create-bot"></a>

- Log on to Connect portal [https://labtenant.us.webexconnect.io/](https://labtenant.us.webexconnect.io/) and navigate to BOT Builder

<img align="middle" src="/digital/assets/new_images/Lab10_bot/1.QAbot_gotoBB.gif" width="1000" />
<br/>
<br/>

- Click the +New Q&A Bot button in upper right corner.  Give your bot a name and enable **agent handover** and the **allow feedback** options.  Name your bot `QABot_0XX` where 0XX is your 3-digit Lab ID

<img align="middle" src="/digital/assets/new_images/Lab10_bot/2.Qabot_addBot.gif" width="1000" />
<br/>
<br/>

## Step 2. Import a Banking article into your Bot & preview responses <a name="import-preview"></a>

- Navigate to **Article** -> click the 3dots **(…)** icon -> **import from catalogue**. Scroll down thru the list of banking articles and choose `Card not working`.  

**NOTE:** If you were setting up a production QA bot for a bank you could import multiple (or all) of the articles in the catalogue and then customize them as per the needs of your application.  

<img align="middle" src="/digital/assets/new_images/Lab10_bot/3.QAbot_article.gif" width="1000" />
<br/>
<br/>

- Click on the `Card not working` article and then in the right-hand pane under `Variant 1`, make the response something more friendly and descriptive:

*“I am sorry you are having trouble with your card.  For this problem, I think you will need to speak to an agent.  Type “help” or “agent” to be transferred to customer service rep who can help you.”*

- Click **Save & Train** to save your changes and train the bot to use your new response. 

<img align="middle" src="/digital/assets/new_images/Lab10_bot/4.QAbot_newReply.gif" width="1000" />
<br/>
<br/>

- Add a new variant to the article to give a greater chance for a match when customers are asking questions of you bot.  Click **Add variant** and type a question that a customer might ask about their debit or credit card not working.  Type *“My card is stuck in the ATM”* in the box.  Click **Save & Train**

<img align="middle" src="/digital/assets/new_images/Lab10_bot/5.QAbot_newVariant.gif" width="1000" />
<br/>
<br/>

- Change the bot’s default agent handoff response to let the customer know you are sending them to an agent.  Click the default Agent Article and in the `Variant 1` text box, overwrite the default message with *“Sure. Let me forward you to one of our helpful representatives. One moment…”*

<img align="middle" src="/digital/assets/new_images/Lab10_bot/5a.QAbot_agentmsg2.gif" width="1000" />
<br/>
<br/>


- Once the Article and variants are added, click on preview on top right to test your BOT responses.  Type your new variant (*“My card is stuck in the ATM”*) to verify the bot responds correctly.  If the response is correct, you can upvote it.  Also feel free to try some of the variants in other articles to see how the default bot answers.

<img align="middle" src="/digital/assets/new_images/Lab10_bot/6.QAbot_preview.gif" width="1000" />
<br/>
<br/>

- Click on the **Sessions** menu to see previous bot interactions and how user inputs matched with your Articles

<img align="middle" src="/digital/assets/new_images/Lab10_bot/7.QAbot_sessions.gif" width="1000" />
<br/>
<br/>


## Step 3. Configure a new chat app in Connect for your Bot <a name="new-chat-app"></a>

- Navigate to the Connect portal [https://labtenant.us.webexconnect.io/](https://labtenant.us.webexconnect.io/) and click **Assets menu** >> **Apps menu**

- Click **Configure new App** button >> select `Mobile/Web`

- Name your App `QAbot_app_0XX` where 0XX is your 3-digit lab ID.

- Set the primary and secondary transport protocols as `MQTT` and `WebSockets` and check `Use Secured port` box.   **SAVE**

<img align="middle" src="/digital/assets/new_images/Lab10_bot/9.QAbot_createapp.gif" width="1000" />
<br/>
<br/>

- Register your new app to Engage and associate it to your lab `Service_0XX`

<img align="middle" src="/digital/assets/new_images/Lab10_bot/91.QAbot_engage.gif" width="1000" />
<br/>
<br/>

- Back at the main **Assets** >> **Apps** menu, note the App ID of your new app.  You will need this alphanumeric ID later in step 7.  

<img align="middle" src="/digital/assets/new_images/Lab10_bot/99.QAbot_AppID.png" width="1000" />
<br/>
<br/>




## Step 4. Assign the bot asset to your Chat EP in WxCC <a name="assign-to-EP"></a>

- Open the WxCC admin portal and select the **Provisioning** >>  **Entry Point/Queues** >> **Entry Point** menu

- Find the chat EP you created earlier in Chat lab 3 

- In the **Asset Name** drop down box, choose the new `QA_Bot_0XX` asset you created in the steps above.  **SAVE**

<img align="middle" src="/digital/assets/new_images/Lab10_bot/93.QAbot_Asset.png" width="1000" />
<br/>
<br/>


## Step 5. Configure widget website settings in Engage <a name="configure-engage"></a>

- Cross-launch the engage portal from the Webex CC admin portal by clicking the **New Digital Channels** icon in the sidebar menu. 

<img align="middle" src="/digital/assets/new_images/Lab10_bot/95.QAbot_engage.gif" width="1000" />
<br/>
<br/>

- Click the **Assets** Menu icon, then click the **pencil edit** icon by your `QA_bot_0XX` asset

<img align="middle" src="/digital/assets/new_images/Lab10_bot/700.PencilEdit.png" width="1000" />
<br/>
<br/>

- Click the **Websites** Tab and the **ADD Website** button.

<img align="middle" src="/digital/assets/new_images/Lab10_bot/1. QAbot_addwebsite.gif" width="1000" />
<br/>
<br/>

- The configuration here will be very similar to the `Livechat` asset you created in Lab 3.  In the **General** tab, make sure at a minimum you configure these two fields:  

   - General Tab >> Display Name >> use any name you would like here 
   - General Tab >> Domain >> `*.glitch.me*`


<img align="middle" src="/digital/assets/new_images/Lab10_bot/2. QAbot_addGlitch.gif" width="1000" />
<br/>
<br/>


- Click the **Appearance** tab.  Change the appearance of your chat widget however you would like.  Save your appearance changes and go to the Widget Visibility tab.  

   - Select >> **show without any restrictions** 

<img align="middle" src="/digital/assets/new_images/Lab10_bot/97.QAbot_appearance.gif" width="1000" />
<br/>
<br/>

- Click the back arrow next to website settings and click the **Installation** tab.  Click the **copy** button and paste the html code into notepad.  Or alternately, keep this window open so you can access it later. You will need this code in subsequent steps when we test our QA bot.   

<img align="middle" src="/digital/assets/new_images/Lab10_bot/98.QAbot_code.gif" width="1000" />
<br/>
<br/>


## Step 6. Download bot flow and upload to Connect <a name="bot-flow-upload"></a>

- Access the pre-built [GITHUB BOT FLOWS](https://github.com/CiscoDevNet/webexcc-digital-channels/tree/main/Webex%20Connect%20Flows/v3.0/Sample/Bot%20Flows) and download the file named `LiveChatQAInboundFlow.workflow.zip`

<img align="middle" src="/digital/assets/new_images/Lab10_bot/8.QAbot_getFlow.png" width="1000" />
<br/>
<br/>

- From the **Connect Dashboard**, click your service (Service 0XX you created earlier) click **flows** and then click **create flow**.

- Give your flow a name like `QA_chatbot_flow0XX` using your lab ID then choose **Upload a Flow** in the **Method** drop down box.  Click Choose **File** button and browse to the file you extracted in the prior step.  

- Click **Create** and then click **Save** on the **Configure Mobile & Web App Event** box. After a few seconds, your flow will populate in the flow builder.   

<img align="middle" src="/digital/assets/new_images/Lab10_bot/92.QAbot_uploadflow.gif" width="1000" />
<br/>
<br/>


## Step 7. Configure the flow to use the QA bot & make it LIVE! <a name="make-live"></a>

In this step you will configure the flow’s custom variables and change fields in 4 different nodes so it will work with your QA bot. 


- Click the **EDIT** button at the top right corner of the screen, then click the **Gear icon** next to Edit to get to the flow’s settings.  Click the **Custom Variables** tab

- Enable Descriptive Logs for 1000 minutes

- In the **appID** field, paste the app ID of your chat asset that you saved back in step 3.

- In the **liveChatDomain** field, type in the test website domain: `www.w3schools.com`

- Click **SAVE**.  

<img align="middle" src="/assets/new_images/Lab10_bot/3. QAbot_custVar.gif" width="1000" />
<br/>
<br/>

- Next double click the **pre-chat form node** in the flow and in the Form Template field select the form template you created in your basic Livechat lab (Lab 3).  

- Do the same thing for the first **receive node**

- In the **QnA bot node**, go to the **BOT** field and select the QnA bot you built in step 1 of the lab. 

- In the **Queue Task** node, go to the **Queue name** field and select the chat queue you built earlier in Livechat Lab 3. Make sure to add your `Sales_0XX`` skill and set it to true. 


<img align="middle" src="/digital/assets/new_images/Lab10_bot/704.QueueDetails.png" width="1000" />
<br/>
<br/>

- Click the **Make Live** button in the upper right corner of the flow.   

- When prompted, associate the flow to the `QAbot_app_0XX`` that you created earlier in the steps above.  Click **Make Live** again. 

<img align="middle" src="/digital/assets/new_images/Lab10_bot/992.QAbot_makeLive.gif" width="1000" />
<br/>
<br/>

- Once you make your flow live, it will move to a publishing stage…. 

<img align="middle" src="/digital/assets/new_images/Lab10_bot/993.QAbot_pub.png" width="1000" />
<br/>
<br/>

- •	…and then a few minutes later it will show up as Live.  You cannot test your flow until it is LIVE

<img align="middle" src="/digital/assets/new_images/Lab10_bot/994.QAbot_live.png" width="1000" />
<br/>
<br/>

## Step 8. Test the QA bot with an agent <a name="test-QA-bot"></a>

- Navigate to the agent Desktop URL at [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com) and login with your lab’s designated agent account.   Place your agent in Available state.  

- On this step we will need our chat widget code from Engage >> Assets.  (See step 5 above.)  

- Navigate to the `glitch.com` project you created in LAB 3 and open your existing project

- In the `index.htm` file, paste your QABot chat widget code from Engage in between the `</body>` tags. Then select preview in new window from the browser’s bottom bar.

<img align="middle" src="/digital/assets/new_images/Lab10_bot/705.TestQABot.png" width="1000" />
<br/>
<br/>


   - In the new window, click your chat button in the lower right pane to launch the widget.

   - Fill in the form and wait for the bot to respond with it’s opening greeting. In this case `Hi there`

<img align="middle" src="/digital/assets/new_images/Lab10_bot/706.HiThere.png" width="1000" />
<br/>
<br/>

   - Type  `my card is stuck in the ATM`  to see the bot answer with your new variant text. 

   - Type `agent` to trigger the handoff from the bot to a human agent.  You will see a `Message Queued` response from the bot.   

<img align="middle" src="/digital/assets/new_images/Lab10_bot/4.QAbot_ask4agent.gif" width="1000" />
<br/>
<br/>


   - Switch back to your contact center agent and answer the incoming chat in desktop.  
   
   - Respond back and forth with your customer, then end the chat and wrap it up. 

<img align="middle" src="/digital/assets/new_images/Lab10_bot/5.QAbot_converse.gif" width="1000" />
<br/>
<br/>


## Step 9. Customer:  request email of chat transcript <a name="request-transcript"></a>

- In the chat widget, click the **menu** icon in the upper left corner.  
- Select **email transcript**.  Enter your email address and hit Send. 

<img align="middle" src="/digital/assets/new_images/Lab10_bot/995.Qabot_emailtranscript.gif" width="1000" />
<br/>
<br/>

**You have successfully built and tested a QA Chat bot!  Congratulations!** 


## [Back to the top](#table-of-contents)

**Congratulations, you have completed this section!**


