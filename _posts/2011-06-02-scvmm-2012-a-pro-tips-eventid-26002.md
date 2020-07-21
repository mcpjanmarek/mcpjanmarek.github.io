---
id: 274
title: 'SCVMM 2012 a PRO Tips &#8211; EventID 26002'
date: 2011-06-02T21:37:51+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=274
permalink: /2011/06/02/scvmm-2012-a-pro-tips-eventid-26002/
jabber_published:
  - "1307043471"
  - "1307043471"
tagazine-media:
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:8:"17238236";s:7:"blog_id";s:8:"16623371";s:9:"mod_stamp";s:19:"2011-06-02 19:37:51";}'
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:8:"17238236";s:7:"blog_id";s:8:"16623371";s:9:"mod_stamp";s:19:"2011-06-02 19:37:51";}'
categories:
  - Nezařazené
  - SC Virtual Machine Manager
tags:
  - SCVMM
  - SCVMM 2012
  - System Center Virtual Machine Manager
  - Virtual Machine Manager
  - Virtualization
---
Pri konfigurace PRO na SCVMM 2012 Beta se SCOM 2007 R2 se muze na SCVMM serveru vyskytovat v logu Operations Manageru EventID 26002:

The Windows Event Log Provider was unable to open the Microsoft-Windows-Hyper-V-Network-Admin event log on computer &#8218;hypervserver.domain.com&#8216; for reading. The provider will retry opening the log every 30 seconds.

Priznaky jsou predevsim nefunkcni PRO a Dynamic Optimization v SCVMM 2012.

Resenim je dat uctu, pod kterym bezi Health Service na SCVMM Serveru, administratorska prava na managovanych Hyper-V serverech. Pokud tedy Health Service bezi pod Local Systemem, pak pridejte ucet serveru SCVMM do Local Administrators na Hyper-V Serverech.

Dle hledanych informaci na webu, jsem v tuto chvili asi prvni na svete, ktery toto popisuje na webu&#8230;
