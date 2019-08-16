---
id: 872
title: 'posh skript v orchestratoru hlásí “Exception setting &#8222;ForegroundColor&#8220;”'
date: 2015-01-08T15:48:21+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=872
permalink: /2015/01/08/posh-skript-v-orhestratoru-hlasi-exception-setting-foregroundcolor/
categories:
  - Nezařazené
  - PowerShell
  - SC Orchestrator
tags:
  - PowerShell
  - SCOR
---
Cela chybová hláška zní takto:

> Exception setting &#8222;ForegroundColor&#8220;: &#8222;Cannot convert null to type &#8222;System.ConsoleColor&#8220; due to invalid enumeration values. Specify one of the following enumeration values and try again. The possible enumeration values are &#8222;Black, DarkBlue, DarkGreen, DarkCyan, DarkRed, DarkMagenta, DarkYellow, Gray, DarkGray, Blue, Green, Cyan, Red, Magenta, Yellow, White&#8220;.&#8220;

V Runbook Testeru to vypadá takhle:

[<img style="display: inline; border: 0px;" title="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb6.png" alt="image" width="667" height="66" border="0" />](http://janmarek.eu/wp-content/uploads/2015/01/image6.png)

V celém PowerShell skriptu zdůrazňuji nemám žádný cmdlet, který používá parametr ForegroundColor.

Po dvou hodinách troubleshootingu celého skriptu (upozorňuju, že má cca 3500 řádek, takže to chvíli trvalo) jsem už přistoupil k postupnému odmazávání nepotřebného balastu.

Najednou koukám, že mám ve skriptu zapomenutý cmdlet Clear-Host, který je tam “na nic”, ale protože skript vždy nejdřív testuju v klasickém PowerShell endžínu, tak jsem si tím čistil obrazovku.

> <span style="background-color: #ffffff; color: #333333; font-family: Thread-000039ac-Id-00000000;">Clear-Host</span>

Ano, toto byl ten problém. Orchestrator se s **Clear-Host** nedokáže vypořádat. Takže jsem ho vyhodil a už to jede!

[<img style="display: inline; border: 0px;" title="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb7.png" alt="image" width="501" height="51" border="0" />](http://janmarek.eu/wp-content/uploads/2015/01/image7.png)

Magické! 🙂