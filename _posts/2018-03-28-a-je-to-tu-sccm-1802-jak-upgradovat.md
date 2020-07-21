---
id: 1816
title: 'A je to tu &#8211; SCCM 1802 &#8211; jak upgradovat?'
date: 2018-03-28T19:57:19+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1816
permalink: /2018/03/28/a-je-to-tu-sccm-1802-jak-upgradovat/
categories:
  - SC Configuration Manager
  - SC Configuration Manager
tags:
  - SCCM
---
Po delší době se zas vracím k blogu a omlouvám se vám čtěnářům za tak dlouhou odmlku.

Nedávno nám vyšla nová verze SCCM a to 1802. Přináší mnoho novinek a také mnoho funkcionalit konečně přechází z preview režimu do fully supported, např. Cloud Management Gateway.

Oznámení o nové verzi je už cca týden staré, ale pokud zběsile klikáte v SCCM konzoli na Check for Updates, tak 1802ku stejně asi nevidíte. Je to proto, že rollout je ve vlnách a není veřejně dostupné, kdy se v našem regionu dočkáme. Pokud ale chvátáte (jako já), tak můžete lehce SCCMku pomoct. Sosněte si skript <a href="https://gallery.technet.microsoft.com/ConfigMgr-1802-Enable-4c8c0003" target="_blank" rel="noopener">zde</a> a jen ho spusťte s použitím parametru SiteServer.

<pre class="theme:shell-default lang:batch decode:true   ">PS C:\FastRingScript_1802&gt; .\EnableFastUpdateRing1802.ps1 -siteServer sccm1.janmarek.local
-Message Determine the providers on the siteServer: 'sccm1.janmarek.local'
-Message SiteCode: 'PR1'
-Message Provider Machine Name: 'sccm1.janmarek.local'


Path : \\sccm1.janmarek.local\root\SMS\site_PR1:SMS_SCI_Component.FileType=2,ItemName="SMS_DMP_DOWNLOADER|SMS
 Dmp Connector",ItemType="Component",SiteCode="PR1"
RelativePath : SMS_SCI_Component.FileType=2,ItemName="SMS_DMP_DOWNLOADER|SMS Dmp
 Connector",ItemType="Component",SiteCode="PR1"
Server : sccm1.janmarek.local
NamespacePath : root\SMS\site_PR1
ClassName : SMS_SCI_Component
IsClass : False
IsInstance : True
IsSingleton : False

The command(s) completed successfully


PS C:\FastRingScript_1802&gt;</pre>

Pak už byste měli po stisknutí Check for Updates vidět novou verzi téměř okamžitě a být tak schopni ji nainstalovat.

Mimochodem 1802ka by měla být dostupná také už jako přímá instalace (jedná se o tzv. baseline version) a tak případné nove sites bude možné instalovat rovnou jako 1802.

Více detailů o novinkách najdete <a href="https://docs.microsoft.com/en-us/sccm/core/plan-design/changes/whats-new-in-version-1802" target="_blank" rel="noopener">tady</a>.

