---
id: 533
title: Výkonný hypervisor zdarma
date: 2012-08-01T14:53:17+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=533
permalink: /2012/08/01/vykonny-hypervisor-zdarma/
categories:
  - Hyper-V
  - Microsoft
  - Nezařazené
  - Windows Server 2012
---
Dnes mě poměrně překvapil náhodně objevený údaj podporované konfigurace VMware vSphere Hypervisoru (ESXi) 5. Dle dokumentace a i mého otestování je maximální podporované množství operační paměti (RAM) jedním ESXi hostitelem 32GB!!!! Není to trochu málo??? Dnes už začínají mít výkonné notebooky 32GB RAM. Myslím, že tímto si VMware limituje své zákazníky. Což je ale pro nás &#8211; Microsoftí svět &#8211; dobře.

Pro srovnání doplňuji podporovanou konfiguraci Microsoft Hyper-V Serveru 2008 R2

  * maximum RAM per hostitel: 1 TB
  * maximální počet socketů: 8
  * počet virtuálních strojů na 1 hostiteli: 384
  * možnost konfigurace clusteru: ANO
  * počet členů clusteru: 16
  * počet virtuálních strojů v clusteru: 1000

a pro úplnost ještě údaje pro budoucí Microsoft Hyper-V Server 2012

  * maximum RAM per hostitel: 4 TB
  * maximální počet socketů: 32
  * počet virtuálních strojů na 1 hostiteli: 1024
  * možnost konfigurace clusteru: ANO
  * počet členů clusteru: 64
  * počet virtuálních strojů v clusteru: 4000

Pro mě osobně je odpověď na otázku &#8222;Jakou bezplatnou virtualizační platformu použít pro mou infrastrukturu?&#8220; jasná: &#8222;Microsoft Hyper-V Server![<img class="alignleft size-full wp-image-534" title="microsoft-hyper-v-server-2008-r2" src="/wp-content/uploads/2012/08/microsoft-hyper-v-server-2008-r2.png" alt="" width="665" height="366" />](/wp-content/uploads/2012/08/microsoft-hyper-v-server-2008-r2.png)&#8220;

&nbsp;
