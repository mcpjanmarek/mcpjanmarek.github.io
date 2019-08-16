---
id: 1088
title: Povolení Isolated User Modu ve WS 2016 TP4
date: 2016-01-08T07:47:55+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1088
permalink: /2016/01/08/povoleni-isolated-user-modu-ve-ws-2016-tp4/
categories:
  - Nezařazené
  - Security
  - Windows Server 2016
---
Isolated User Mode je funkce, která zajišťuje, aby určitá security related data (např. NT Hash, kterou drží v paměti proces LSASS.EXE) byla managována izolovanými procesy pomocí Virtual Secure Modu. VSM je paměťově kompletně oddělený prostor OS a funguje pomocí HW virtualizace stejně jako Hyper-V.

IUM povolíte třeba PowerShellem takto:

<pre>Install-WindowsFeature Isolated-Usermode
New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord –Force
Restart-Computer</pre>