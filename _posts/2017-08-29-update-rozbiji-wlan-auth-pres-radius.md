---
id: 1768
title: Update rozbíjí WLAN auth přes RADIUS
date: 2017-08-29T09:00:19+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1768
permalink: /2017/08/29/update-rozbiji-wlan-auth-pres-radius/
categories:
  - Nezařazené
  - Windows Server
tags:
  - NPS
  - Update
---
Microsoft vydal update <a href="https://support.microsoft.com/en-us/help/4025335/windows-8-1-windows-server-2012-r2-update-kb4025335" target="_blank" rel="noopener">KB4025335</a>, který ale rozbíjí ověřování na WLAN přes NPS (RADIUS). Tento update už je superseednutý updatem <a href="https://support.microsoft.com/en-us/help/4034681/windows-8-1-windows-server-2012-r2-update-kb4034681" target="_blank" rel="noopener">KB4034681</a>.

Pokud už to máte rozbité, tak je potřeba sáhnout do registrů a nastavit **SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13\DisableEndEntityClientCertCheck** na hodnotu **0**.

Restart to nepotřebuje a s nainstalovaným blbým updatem už si nemusíte lámat hlavu.

