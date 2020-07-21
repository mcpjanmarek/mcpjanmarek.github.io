---
id: 583
title: 'System Center 2012 R2: Konfigurace SQL Server Analysis Services ve VMM'
date: 2013-10-20T15:02:04+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=583
permalink: /2013/10/20/system-center-2012-r2-konfigurace-sql-server-analysis-services-ve-vmm/
categories:
  - Nezařazené
  - System Center 2012
  - System Center 2012 R2
---
**Požadavky:**

  * nainstalovaný a nakonfigurovaný SCOM Reporting
  * instance SQL Server Analysis Services (musí se jednat o identickou instanci, na které běží SCOM Reporting Services)
  * doménový účet, který má administrátorská práva ke zmiňované instanci SQL AS a který je členem SCOM built-in skupiny &#8222;Operations Manager Report Security Administrators&#8220; &#8211; říkejme mu např. SQLVMMAS
  * na všechny VMM servery (v případě, že máme vysoce dostupné VMM, tak je VMM serverů více) nainstalovat SQL Server Analysis Management Objects v adekvátní verzi

**Konfigurace**:

Ve VMM konzoli v části Settings &#8211; System Center Settings &#8211; Operations Manager Settins &#8211; SQL Server Analysis Services povolíme integraci a vyplníme název SQL Serveru a instanci, na kterých běží Analysis Services a použijeme zmiňovaný účet SQLVMMAS.

[<img class="alignleft size-full wp-image-588" alt="vmm-as-configuration" src="/wp-content/uploads/2013/10/vmm-as-configuration.png" width="772" height="577" />](/wp-content/uploads/2013/10/vmm-as-configuration.png)

Ve VMM konzoli v jobs sledujeme průběh konfigurace.

Oficiální informace <a href="http://technet.microsoft.com/en-us/library/hh882395.aspx" target="_blank">zde</a>.

