---
id: 1053
title: Přejmenování názvu SCCM site
date: 2015-12-29T17:46:37+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1053
permalink: /2015/12/29/prejmenovani-nazvu-sccm-site/
categories:
  - Nezařazené
  - SC Configuration Manager
---
Změnit site code po instalaci nelze, ale upravit site name ano. Přes konzoli to neuděláte ovšem. Musíte sáhnout do WMI. Nejlépe to jde přes PowerShell (jak jinak ;)). Stačí tedy vzít následujících pár řádek kódu:

<pre>$NovyNazevSite = 'Tohle bude novy nazev SCCM site'
$SiteKod = 'ABC'
$SiteServer = 'sccmserver01.janmarek.local'
$site = Get-WmiObject -Namespace root/SMS/site_$($SiteKod) -ComputerName $SiteServer -Class SMS_SCI_SiteDefinition
$site.Name = $NovyNazevSite
$site.Put()</pre>