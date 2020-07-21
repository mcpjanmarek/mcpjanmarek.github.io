---
id: 852
title: windows cannot find the microsoft software license terms
date: 2015-01-02T09:44:37+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=852
permalink: /2015/01/02/windows-cannot-find-the-microsoft-software-license-terms/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server
  - Windows Server 2012 R2
tags:
  - Hyper-V
  - windows server
  - Windows Server 2012 R2
---
Tak na tuhle chybovku můžete narazit v mnoha případech, teď se jedná ale o situaci, kdy instalujete OS do virtuálky.

[<img title="os-install-error-ram-less-than-768mb" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="os-install-error-ram-less-than-768mb" src="/wp-content/uploads/2015/01/osinstallerrorramlessthan768mb_thumb.png" width="689" height="519" />](/wp-content/uploads/2015/01/osinstallerrorramlessthan768mb.png) 

První co by vás asi napadlo je, že máte poškozené médium nebo ISO soubor. Problém je ale jinde a to v množství operační paměti (v tomto případě tedy virtuální). Pro instalaci Windows Server 2012 R2 obecně platí, že je potřeba 512MB RAM. Moje VM ale měla 512MB RAM a stejně setup hlásil tuto chybovku. Ono to totiž není tak jednoduché. Když instalujete OS do VM, tak jsou nároky o něco vyšší. Když si přečtete oficiální dokumentaci <a href="http://technet.microsoft.com/en-us/library/dn303418.aspx" target="_blank">zde</a>, tak se všimněte důležitého textu v rámečku:

[<img title="os-install-virtual-memory-issue" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="os-install-virtual-memory-issue" src="/wp-content/uploads/2015/01/osinstallvirtualmemoryissue_thumb.png" width="701" height="496" />](/wp-content/uploads/2015/01/osinstallvirtualmemoryissue.png) 

V 99% procentech případů jsem prostě zvýšil virtuální RAM na 768MB a instalace prošla bez problémů – viz tedy řešení zmíněné v prvním bullet pointu (ano píše se tam 800MB, ale z praxe mi stačilo 768MB :)).

Teď si možná říkáte – “Proč bych instaloval WS2012R2 jen s 512MB nebo s 768MB RAM? Vždyť pod 1,5GB RAM se to chová pekelně pomale.”. Ano při statické paměti tohle v mnoha případech dává smysl, ale berte v potaz Dynamic Memory na VM. Tam se typicky každý snaží do hodnoty Startup Memory nacpat čislo, které stačí pro boot OS (to se typicky odvíjí od paměti pro instalaci). 

[<img title="hyper-v-2012-r2-dynamic-memory" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="hyper-v-2012-r2-dynamic-memory" src="/wp-content/uploads/2015/01/hyperv2012r2dynamicmemory_thumb.png" width="458" height="483" />](/wp-content/uploads/2015/01/hyperv2012r2dynamicmemory.png) 

Tam tedy pozor na to, že ani tam nedávejte 512MB (narovinu – on ten WS2012R2 s 512MB nabootuje :)), ale aspoň 768MB. Tím pádem to tam v klidu nainstalujete a pak už si přes Integration Service – Dynamic Memory sáhne pro více paměti až bude VM potřebovat. _Mimochodem, do Minimum RAM klidně můžete dát i méně než 512 MB 🙂_

Aby to bylo kompletní, tak musím ještě dodat, že pokud vytváříte VM ze šablony (takže po startu tam projíždí jen sysprep), tak to v klidu najede i s 512MB samozřejmě.
