---
id: 150
title: Rekonfigurace SCVMM Self-Service Portalu na jiný Management Server
date: 2011-01-21T16:27:15+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=150
permalink: /2011/01/21/rekonfigurace-scvmm-self-service-portalu-na-jiny-management-server/
jabber_published:
  - "1295623638"
  - "1295623638"
categories:
  - Nezařazené
  - SC Virtual Machine Manager
---
Pro rekonfiguraci SSP na jiný management server stačí pouze změnit hodnotu &#8222;VMMServerName&#8220; v klíči &#8222;HKLMSOFTWAREMicrosoftMicrosoft System Center Virtual Machine Manager Self-Service PortalSettings&#8220; na FQDN nového management server a restartovat službu SSP.
