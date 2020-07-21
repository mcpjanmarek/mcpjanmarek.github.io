---
id: 579
title: 'System Center 2012 R2: Integrace SCOM a SCVMM &#8211; Management Packy'
date: 2013-10-20T12:40:22+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=579
permalink: /2013/10/20/system-center-2012-r2-integrace-scom-a-scvmm-management-packy/
categories:
  - Nezařazené
  - Private Cloud
  - SC Operations Manager
  - SC Virtual Machine Manager
  - System Center 2012
  - System Center 2012 R2
---
[<img class="alignleft size-full wp-image-581" alt="scom-scvmm-integration" src="/wp-content/uploads/2013/10/scom-scvmm-integration.png" width="502" height="418" />](/wp-content/uploads/2013/10/scom-scvmm-integration.png)Integrovat Operations Manager a Virtual Machine Manager přináší mnoho funkcí jako např. Reporting pro VMM, Forecast využití zdrojů nebo synchronizaci Maintenance Modu.

Jedním z požadavků pro integraci je naimportovat do Operations Manager ty správné Management Packy. Jak sám průvodce říká, potřebujete tyto:

  * SQL Server Core Library version 6.0.5000.0 or later
  * Windows Server Internet Information Services Library version 6.0.5000.0 or later
  * Windows Server Internet Information Services 2003 version 6.0.5000.0 or later
  * Windows Server 2008 Internet Information Services 7 version 6.0.6539.0 or later

Dnes je už ale částečně problém některé z nich najít. Zmiňovaný SQL MP stáhnete klasicky z katalogu a to jak přes SCOM konzoli, tak ručně z <a href="http://www.microsoft.com/en-us/download/details.aspx?id=10631" target="_blank">webu</a>.

Zbylé tři IIS MP ale v katalogu nejsou. Když se po nich začnete pídit po internetu, tak narazíte jen na &#8222;Windows Server Internet Information Services 7 Management Pack for System Center Operations Manager 2007&#8220;. Ano, je pro SCOM 2007, ale dá se použít i pro SCOM 2012 (R2). Ten je tedy ke stažení <a href="http://www.microsoft.com/en-us/download/confirmation.aspx?id=9815" target="_blank">zde</a>.

Teď už jen nastavit práva pro správné účty a nastavit z VMM konzole integrace. Hodně štěstí!
