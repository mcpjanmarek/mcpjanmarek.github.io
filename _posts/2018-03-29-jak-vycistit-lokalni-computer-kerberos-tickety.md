---
id: 1821
title: Jak vyčistit lokální computer Kerberos tickety?
date: 2018-03-29T21:45:40+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1821
permalink: /2018/03/29/jak-vycistit-lokalni-computer-kerberos-tickety/
categories:
  - SC Configuration Manager
  - SC Configuration Manager
  - Windows 10
  - Windows 7
  - Windows 8
  - Windows 8.1
  - Windows Server
  - Windows Server 2012
  - Windows Server 2012 R2
  - Windows Server 2016
  - Windows Server 2016
tags:
  - SCCM
  - SCOM
  - Windows
  - Windows 10
  - windows server
  - Windows Server 2012 R2
  - Windows Server 2016
---
Určitě se vám už taky mnohokrát stalo, že jste při instalaci různých služeb zapomněli dát počítačový účet serveru/stanice do správné AD skupiny (pomocí které jste měli řízené potřebné oprávnění) a tak jste po adhoc přidání do skupiny museli server/stanici restartovat, aby se členství projevilo.

Nám se to občas stává při nasazování SCCM, SCOM či SCO a protože ne vždy si můžete restart serveru hned dovolit, tak by bylo dobré, kdyby to šlo i bez něj. A ono to jde. Stačí použít klasický příkaz **klist** a jen použít ten správný logon ID. Pro local system je to ID vždy stejné, takže ten příkaz pak vypadá takto:

<pre class="lang:default decode:true">C:\WINDOWS\system32&gt;klist.exe -li 0x3e7 purge

Current LogonId is 0:0x5097d
Targeted LogonId is 0:0x3e7
Deleting all tickets:
Ticket(s) purged!

C:\WINDOWS\system32&gt;</pre>

Musíte to samozřejmě spouštět jako admin&#8230; A pozor! Nepouštějte to v powershellu, ale opravdu v cmd, jinak to ne vždy nefunguje. Pokud už jste ale zvyklí pouštět vždy rovnou PowerShell Host, tak si to stačí jen zavolat přes CMD /C a taky vám to pak vždy pojede:

<pre class="lang:default decode:true ">PS C:\WINDOWS\system32&gt; cmd /c klist.exe -li 0x3e7 purge

Current LogonId is 0:0x5097d
Targeted LogonId is 0:0x3e7
Deleting all tickets:
Ticket(s) purged!
PS C:\WINDOWS\system32&gt;</pre>

Tak příště už bez restartu 😉

&nbsp;

