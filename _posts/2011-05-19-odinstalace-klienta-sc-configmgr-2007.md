---
id: 271
title: Odinstalace klienta SC ConfigMgr 2007
date: 2011-05-19T16:36:12+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=271
permalink: /2011/05/19/odinstalace-klienta-sc-configmgr-2007/
jabber_published:
  - "1305815772"
  - "1305815772"
categories:
  - Nezařazené
  - SC Configuration Manager
tags:
  - Configuration Manager
  - SCCM
  - SCCM 2007
  - SCConfigMgr
---
Občas narazím na otázky ohledně odinstalace klienta SC ConfigMgr 2007.

CCMCLEAN, obsažený v toolkitu pro SMS 2003, byl vyvinut především pro odinstalaci Advanced Clienta SMS 2003. Není tedy podporovaným nástrojem pro odinstalaci klienta SCCM 2007.

Jednou z novinek ve verzi 2007 ale byla právě zjednodušená odinstalace. Stačí zavolat CCMSETUP.EXE s parametrem /UNINSTALL.

**CCMSETUP.EXE /UNINSTALL**