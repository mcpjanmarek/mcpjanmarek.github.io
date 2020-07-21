---
id: 497
title: Update Rollup 2 pro System Center 2012
date: 2012-07-26T10:29:44+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=497
permalink: /2012/07/26/update-rollup-2-pro-system-center-2012/
jabber_published:
  - "1343291385"
  - "1343291385"
email_notification:
  - "1343291387"
  - "1343291387"
categories:
  - Nezařazené
  - SC App Controller
  - SC Data Protection Manager
  - SC Operations Manager
  - SC Orchestrator
  - SC Service Manager
  - SC Virtual Machine Manager
  - System Center
  - System Center 2012
---
Včera 25.7. 2012 vyšel balík záplat pro System Center 2012. Stahovat ho můžete na Microsoft Download Centeru nebo přes Windows Update. Více info ze dozvíte [zde](http://support.microsoft.com/kb/2706783).

Obsahuje opravy na poměrně zásadní chyby v System Center 2012 komponentách:

  * App Controller (3 chyby)
  * Data Protection Manager (11 chyb)
  * Operations Manager (2 chyby + 3 opravené Management Packy pro Unix/Linux)
  * Orchestrator (1 chyba)
  * Service Manager (12 chyb)

Za sebe a mou oblíbenou virtualizaci musím vypíchnout hlavně problémy se stavem virtuálního stroje ve Virtual Machine Manageru, který se po &#8222;sdíleném&#8220; připojení ISO souboru z Library dostane do Unsupported stavu (a to i přes správnou konfiguraci delegace a share oprávnění). Nepříjemný je také obdobný stav v případě, kdy virtuální stroj má své disky umístěné na cluster disku (i CSV) a přitom není nakonfigurovaný jako vysoce dostupný.