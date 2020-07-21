---
id: 505
title: 'SC 2012 Operations Manager &#8211; ADTAdmin Access Denied'
date: 2012-07-27T10:44:31+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=505
permalink: /2012/07/27/sc-2012-operations-manager-adtadmin-access-denied/
jabber_published:
  - "1343378672"
  - "1343378672"
email_notification:
  - "1343378673"
  - "1343378673"
categories:
  - Nezařazené
  - SC Operations Manager
  - System Center
  - System Center 2012
---
Jedna ze skvělých volitelně instalovatelných služeb Operations Manageru jsou Audit Collection Services. Ty se starají o to, aby byly audit logy dle určitého filtru automaticky přeposílány z eventlogu monitorovaného systému do SQL databáze, nad kterou pak můžete spouštět reporty.

Tento filtr se konfiguruje na úrovni ACS collectoru, kterým je Management Server, kam jste ACS služby nainstalovali. Typicky Operations Manager Management Server.

K nastavení filtru slouží nástroj příkazové řádky ADTAdmin.exe, který naleznete na ACS collectoru ve složce C:WindowsSystem32SecurityADTserver.

Jeho syntaxe je popsaná v [dokumentaci](http://technet.microsoft.com/en-us/library/hh212727.aspx) k Operations Manageru. Bohužel jsem ale právě teď narazil na problém při jeho spuštění.

I při správné syntax a spuštění pod právy administrátora (pozor také na UAC) se dočkáte výstupu Access Denied.

[<img class="alignleft size-full wp-image-506" style="margin: 7px 14px 6px 0; display: inline; float: left;" title="adtadmin_access_denied" src="/wp-content/uploads/2012/07/adtadmin_access_denied.png" alt="" width="590" height="91" align="left" />](/wp-content/uploads/2012/07/adtadmin_access_denied.png)

Problém je v tom, že ve výchozí instalaci a nastavení beží ACS služba pod Network Service účtem. Při spuštění ADTadmin příkazu se snaží tato služba zapsat hodnotu do klíče HKLMSYSTEMCurrentControlSetservicesAdtServerParametersDbQueueQuery, kam nemá práva.

[<img class="alignleft size-full wp-image-507" style="margin: 7px 14px 6px 0; display: inline; float: left;" title="adtadmin_regedit" src="/wp-content/uploads/2012/07/adtadmin_regedit.png" alt="" width="590" height="377" align="left" />](/wp-content/uploads/2012/07/adtadmin_regedit.png)

&nbsp;

Stačí tedy na úrovni klíče Parameters změnit nastavení security pro uživatele Network Service na Full Control.

[<img class="alignleft size-full wp-image-508" style="margin: 7px 14px 6px 0; display: inline; float: left;" title="adtadmin_regedit_permissions" src="/wp-content/uploads/2012/07/adtadmin_regedit_permissions.png" alt="" width="363" height="412" align="left" />](/wp-content/uploads/2012/07/adtadmin_regedit_permissions.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

Po opětovném spuštění příkazu ADTadmin již proběhne vše vpořádku a v registrech můžete vidět nastavenou query

[<img class="alignleft size-full wp-image-509" style="margin: 7px 14px 6px 0; display: inline; float: left;" title="adtadmin_final" src="/wp-content/uploads/2012/07/adtadmin_final.png" alt="" width="590" height="383" align="left" />](/wp-content/uploads/2012/07/adtadmin_final.png)

