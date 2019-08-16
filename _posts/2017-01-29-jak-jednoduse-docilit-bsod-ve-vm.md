---
id: 1655
title: Jak jednoduše docílit BSOD ve VM
date: 2017-01-29T19:29:17+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1655
permalink: /2017/01/29/jak-jednoduse-docilit-bsod-ve-vm/
categories:
  - Hyper-V
  - Hyper-V
tags:
  - Hyper-V
---
Používal jsem historicky různé způsoby jak &#8222;sestřelit&#8220; OS, aby člověk mohl zkoušet debugging, simulovat Guest OS reboot apod. Od Windows Server 2012 R2/Windows 8.1 Hyper-V lze tohoto docílit přímo pomocí powershellu z hostitelského OS. Použije se cmdlet **Debug-VM**. Ten samozřejmě není jen k vyvolání BSOD, ale k celkovému debuggingu.

Pro BSOD použijete následující příkaz, který spustíte v parent partition:

<pre class="lang:ps decode:true ">[string]$NazevVM = 'TestVM123'
Debug-VM -VMName $NazevVM -InjectNonMaskableInterrupt -Force</pre>