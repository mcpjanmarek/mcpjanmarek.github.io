---
id: 31
title: Microsoft System Center Configuration Manager – client agents
date: 2009-08-07T11:02:00+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2009/08/07/microsoft-system-center-configuration-manager-%e2%80%93-client-agents'
permalink: /2009/08/07/microsoft-system-center-configuration-manager-client-agents/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!331')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!331')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SC Configuration Manager
---
<div id="msgcns!6E7B9216726D07B8!331" class="bvMsg">
  <p>
    <img style="display:inline;margin:0 10px 0 0;" alt="System Center Configuration Manager" align="left" src="http://i.microsoft.com/global/systemcenter/en/us/PublishingImages/SysCnt-ConfigMgr_80.png" width="310" height="80" />Pokud planujete prejit ze stavajiciho Microsoft Systems Management Serveru 2003 na Microsoft System Center Configuration Manager 2007 (v tuto chvili SP1 R2) chci Vas upozornit, ze jiz nebudete moci konfigurovat na sekundarni site jine nastaveni nez je na primary site. Pokud si nainstalujete nekam na otestovani ConfigMgr 2007 uvidite, ze sekce Client Agents uz na secondary site vubec neni. Nedeste se, to neni chyba Vasi instalace, ale vlastnost. Samozrejme, ze se take jedna o licencni politiku. Pokud totiz chcete rozdilne nastaveni na podrizenych site, musite si poridit dalsi licenci pro primary site. Zvazte proto, zda opravdu potrebujete rozdilne nastaveni pro urcite lokality, nebo zda jste schopni dojit ke kompromisu a tim usetrite a samozrejme si take zjednodusite spravu ConfigMgr.
  </p>
</div>