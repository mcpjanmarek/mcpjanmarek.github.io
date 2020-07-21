---
id: 128
title: Zálohování VMs na Microsoft Hyper-V Serveru
date: 2012-07-30T13:00:06+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/2010/10/21/how-to-backup-hyper-v-server/
permalink: /2012/07/30/how-to-backup-hyper-v-server/
jabber_published:
  - "1287656527"
  - "1287656527"
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server
---
[<img style="background-image: none; padding-left: 0; padding-right: 0; display: inline; float: left; padding-top: 0; border: 0; margin: 0 10px 0 0;" title="logo-hypervsrvr2" src="http://janmarek.eu/wp-content/uploads/2010/10/logo-hypervsrvr2_thumb.png" alt="logo-hypervsrvr2" width="240" height="72" align="left" border="0" />](http://janmarek.eu/wp-content/uploads/2010/10/logo-hypervsrvr2.png)

Nedávno jsem dostal otázku, jak zálohovat virtuální stroje bežící na Microsoft Hyper-V Server 2008 R2 (bezplatném Microsoft hypervisoru).

V prvé řadě je nutné nainstalovat Windows Server Backup. Na core edici jak jinak, než pomocí OCSetup:

> _start /wait ocsetup WindowsServerBackup_

Následně je důležité povolit vzdálenou správu a zálohování pomocí příkazu NetSh:

> _netsh advfirewall set rule group=”Windows Backup” NEW enable=YES_

V tuto chvíli je možné se vzdáleně připojit konzolí Windows Server Backup  na Hyper-V server a konfigurovat zálohování. Samozřejmě se jedná o zálohováni &#8222;zaživa&#8220; za běhu virtuálních strojů.