---
title: 'Lab Pre-requisites'
author: Dave Easton, Karthik Sundaram
date: 2023-10-04
layout: post
---

# Table of Contents

- [Lab Topology](#lab-topology)
- [Access URLs](#access-urls)
- [Before starting the labs](#before-starting-the-labs)
- [Lab Support](#lab-support)

# Introduction

Digital channels are now more impactful than ever. 
These labs are specially designed for this Webex ONE session. The  purpose of the labs is to give you a clear understanding of the New Digital Channels functionality. You will learn how to create and configure all digital channels including Chat, Email, Whatsapp and SMS. You will get a clear understanding of how to use scripts and troubleshoot issues by using the debug console.

## Lab Topology

<img align="middle" src="/digital/assets/images/topology.png" width="1000" />

## Access URLs

| Component            | URL                                                                                                     | Login                            |
| -------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------- |
| Webex CC Control Hub | [https://admin.webex.com](https://admin.webex.com){:target="\_blank"}                                   | wxcclabs+admin_ID<0XX>@gmail.com |
| Management Portal    | [https://portal.wxcc-us1.cisco.com/portal](https://portal.wxcc-us1.cisco.com/portal){:target="\_blank"} | wxcclabs+admin_ID<0XX>@gmail.com |
| Webex Connect        | [https://labtenant.us.webexconnect.io/](https://labtenant.us.webexconnect.io){:target="\_blank"}                                                                   | wxcclabs+admin_ID<0XX>@gmail.com |
| Agent Desktop        | [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com){:target="\_blank"}             | wxcclabs+admin_ID<0XX>@gmail.com |

> **NOTE:**  
> A lab ID will be assigned to you at the beginning of the lab. It will be in the form of <ID0XX> where 0XX is your 3-digit lab number. This ID number will be part of all admin and agent usernames used in this lab. A unique password will also be assigned to you for this account. All accounts used in this lab will use SSO

## Before starting the labs

1. You will need to an email address to use with SSO. We recommend you create gmail accounts in the format suggested for your lab 

2. Please confirm that you can login to the Webex CC Admin portal by using the links above.

3. You have to use the admin account (with Administrator privileges) for access to Control Hub and Administration portal.

4. Please follow the labs in the same order as they are provided.

### Users

The users have the following preconfiguration

| **User Role** | **User email**                      |
| ------------- | ----------------------------------- |
| Agent         | wxcclabs+agent\_ ID<0XX>@@gmail.com |
| Supervisor    | wxcclabs+supvr\_ ID<0XX>@@gmail.com |

### User Settings

| **Entity**          | **Name**  |
| ------------------- | --------- |
| Multimedia Profiles | MMP       |
| Site                | Site      |
| Team1               | Team1_0XX |
| Team2               | Team2_0XX |

## Lab Support

1. Proctors are your first point of contact. If you need assistance just raise your hand.

2. All registered participants are also added to the support room where Engineering resources and Product Management teams are added. You can also use that space for any questions related to the digital channels.

### May good fortune smile on you as you begin this new adventure :)

<script>
function mainPage() 
{
window.location.href = "Home";
}
function nextLab() 
 {
 window.location.href = "Lab1_Preconfiguration";
 }
</script>

<div id="button-row">
<button onclick="mainPage()" style="
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Main Page</button>

<button onclick="nextLab()" style="
  position: absolute;
  right: 200px;
  border-radius: 5px;
  background-color: rgb(116,191,75);
  padding: 10px;">Next Lab</button>

</div>
