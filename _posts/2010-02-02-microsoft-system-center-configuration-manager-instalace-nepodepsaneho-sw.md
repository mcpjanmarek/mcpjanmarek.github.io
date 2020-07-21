---
id: 30
title: Microsoft System Center Configuration Manager – instalace nepodepsaného sw
date: 2010-02-02T13:05:00+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/02/02/microsoft-system-center-configuration-manager-%e2%80%93-instalace-nepodepsaneho-sw'
permalink: /2010/02/02/microsoft-system-center-configuration-manager-instalace-nepodepsaneho-sw/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!332')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!332')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SC Configuration Manager
---
<div id="msgcns!6E7B9216726D07B8!332" class="bvMsg">
  <p>
    <img style="display:inline;margin:0 15px 0 0;" alt="System Center Configuration Manager" align="left" src="http://i.microsoft.com/global/systemcenter/en/us/PublishingImages/SysCnt-ConfigMgr_80.png" width="310" height="80" />Vyrabite silent instalacni balicek na nejakou aplikaci, nebo na instalaci ovladace (hw) a ikdyz specifikujete silent parametry, tak vam Windows zahlasi warning ze se snazite instalovat nepodepsany software (okenko ma hlavicku "Hardware Installation" napr., a zacina textem "The software you are installing for this hardware: <em>nazev zarizeni</em> has not passed Windows Logo testing to verify its compatibility with Windows XP&#8230;&#8230;; a ma potvrzovaci volby "Continue Anyway" nebo "Stop Installation")?
  </p>
  
  <p>
    Staci kdyz na lokalnim stroji date vlastnosti My Computer -> zalozku Hardware -> Driver signing a zvolte Ignore &#8211; Install the software anyway and don&#8217;t ask for my approval.<br />V Group Policy (Windows Server 2008) toto nastaveni zmenite v User Config -> Policies -> Adm templates -> System -> Driver Installation -> polozka "Code signing for device drivers" -> povolte policy a nastavte hodnotu na Ignore.
  </p>
</div>

