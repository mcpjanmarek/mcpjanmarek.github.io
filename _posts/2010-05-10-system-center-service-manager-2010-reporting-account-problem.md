---
id: 20
title: System Center Service Manager 2010 – reporting account problem
date: 2010-05-10T12:00:46+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/05/10/system-center-service-manager-2010-%e2%80%93-reporting-account-problem'
permalink: /2010/05/10/system-center-service-manager-2010-reporting-account-problem/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!291')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!291')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SC Service Manager
---
<div id="msgcns!6E7B9216726D07B8!291" class="bvMsg">
  <p>
    <img style="display:inline;margin:0 10px 0 0;" alt="System Center Service Manager" align="left" src="http://i.microsoft.com/global/systemcenter/en/us/PublishingImages/SysCnt-ServiceMgr.png" width="230" height="64" />
  </p>
  
  <p>
    Včera jsem při instalaci Service Manageru 2010 narazil na problém při specifikaci uživatele pro Reporting Service. Vytvořil jsem Active Directory uživatele s názvem SCSM_ReportingAccount. Po zadání tohoto uživatele s heslem do instalátoru a testu connection na mne vyskočila chyba. Zkoušel jsem znovu heslo, resetoval heslo v AD, dal uživatele jako lokálního administrátora a stále nic. Po 2 hodinách bádání a zkoušení mne napadla myšlenka, co když je uživatelské jméno příliš dlouhé. A opravdu to tak je. Přejmenoval jsem uživatele na SCSM_RepAccount a vše proběhlo úspěšně. Takový problém bych teda nečekal…
  </p>
</div>
