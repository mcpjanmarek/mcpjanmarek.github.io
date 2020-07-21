---
id: 736
title: Exchange Server 2013 a poškozený applicationhost.config
date: 2014-01-28T17:26:04+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=736
permalink: /2014/01/28/exchange-server-2013-a-poskozeny-applicationhost-config/
categories:
  - Misc...
  - Nezařazené
---
V mém labu na System Center a Windows Server dnes přestal fungovat Exchange Server 2013. ECP dělalo, že neexistuje a když jsem se na něj chtěl podívat přes IIS Manager, tak jsem při kliknutí na Application Pools dostal takovouhle krásnou hlášku:

> <span class="st">Configuration file is <em>not well</em>&#8211;<em>formed XML</em></span>

To už mě dost vyděšilo, protože mám jen jeden exchange server a proto nemám moc odkud zkopírovat funkční applicationhost.config (a backup nemám, protože je to lab). Napadlo mě zkusit udělat restore z IIS backupu. Takže jsem zkusil ze složky C:\Windows\System32\InetSrv\Backup vykopírovat config soubor do Config adresáře. Bohužel ten backup nebyl úplně aktuální, takže jsem nedostal původní konfiguraci IIS. Napadlo mě si vyrobit ty virtuální adresáře potom ručně přes Exchange Management Shell a příkazy typu New-ECPVirtualDirectory. Problém byl ale v tom, že ta web site byla tak rozhašená, že se mi ani PowerShell Exchange Modul nepřipojil k serveru.

Co teď? Už jsem si představoval, jak deinstaluju Exchange server (natvrdo, přes adsiedit apod., protože neudělám normální uninstall). Napadlo mě ještě ale vzít applicationhost.config z C:\inetpub\history. Tak jsem vzal nějaký z data, kdy vím, že mi Exchange jel, překopíroval do C:\Windows\System32\InetSrv\Config a rozjelo se to. ECP jede, Outlooky se připojí, maily chodí&#8230;

Jinak ten Exchange Server byl samozřejmě virtualizovaný, na Hyper-V 2012 R2. Na disku nebylo úplně moc místa (je to lab, tak to moc nehlídám) &#8211; asi tak 2GB, takže předpokládám, že se mi to IIS poškodilo kvůli tomu, ale to jsou jen mé domněnky. V této oblasti nejsem moc specialista 🙂
