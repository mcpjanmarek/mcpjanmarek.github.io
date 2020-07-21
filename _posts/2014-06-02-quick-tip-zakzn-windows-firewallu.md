---
id: 800
title: 'Quick TiP: Zakázání windows firewallu'
date: 2014-06-02T10:56:00+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=800
permalink: /2014/06/02/quick-tip-zakzn-windows-firewallu/
categories:
  - Nezařazené
  - Windows Server
tags:
  - windows server
---
Jestli provozujete Windows Server v Core edici, tak jste možná narazili na to, jak rychle vypnout Windows Firewall. Jde to jednoduše přes následující příkaz:

> netsh firewall set opmode disable

Nebo můžete samozřejmě použít Windows PowerShell:

> Get-NetFirewallProfile -Name * | Set-NetFirewallProfile -Enabled false

Ale! Opravdu chcete úplně vypnout Windows Firewall? Zamyslete se 🙂
