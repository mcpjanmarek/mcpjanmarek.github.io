---
id: 519
title: Síť pro Live Migration ve Windows Server 2012
date: 2012-07-30T11:07:19+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=519
permalink: /2012/07/30/sit-pro-live-migration-ve-windows-server-2012/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2012
---
Ve Windows Serveru 2012 byla konečně provedena úprava do konzole Failover Cluster Manager týkající se nastavení sítě použité při přesunu běžícího virtuálního systému metodou Live Migration.

Dříve bylo nutné provést konfiguraci na úrovni virtuálního stroje. Tento přístup byl ale dost matoucí. Zaprvé nezapadal do konceptu nastavení ve Failvoer Cluster Manageru a zadruhé globální nastavení pro celý cluster se nastavovalo na úrovni vysoce dostupné služby.

Nově tedy přímo v sekci Networks je dostupná možnost **Live Migration Settings&#8230;**

[<img class="alignleft size-full wp-image-520" title="winsrv2k12_livemigrationnetwork" src="/wp-content/uploads/2012/07/LM.png" alt="winsrv2k12_livemigrationnetwork" width="763" height="726" />](/wp-content/uploads/2012/07/LM.png)

