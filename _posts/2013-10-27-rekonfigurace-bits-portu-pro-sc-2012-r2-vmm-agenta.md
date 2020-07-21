---
id: 618
title: Rekonfigurace BITS portu pro SC 2012 R2 VMM Agenta
date: 2013-10-27T16:55:59+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=618
permalink: /2013/10/27/rekonfigurace-bits-portu-pro-sc-2012-r2-vmm-agenta/
categories:
  - Nezařazené
  - System Center 2012 R2
---
System Center 2012 R2 Virtual Machine Manager Agent, který je nainstalován na každý server, který je pod správou VMM (Hyper-V hostitel, Management Server, Library Server, PXE server, apod.), používá v případě přenosu souborů technologii BITS (Background Intelligent Transfer Service). Ta typicky běží na portech HTTP (80) nebo HTTPS (443). Nastává tedy určitá pravděpodobnost, že bude s některým z portů v kolizi, protože je již používá jiná služba.

Jak změnit port pro BITS, na kterém VMM agent posílá soubory? Celá konfigurace je v registrech a to v této cestě:

> HKLM\Software\Microsoft\Microsoft System Center Virtual Machine Manager Agent\Setup\BITSTcpPort

<p style="text-align: center;">
  <a href="http://janmarek.eu/wp-content/uploads/2013/10/bitsportvmm.png"><img class="wp-image-621 aligncenter" alt="bitsportvmm" src="http://janmarek.eu/wp-content/uploads/2013/10/bitsportvmm.png" width="589" height="130" /></a>
</p>

Hodnotu změňte na jakýkoli volný port, restartujte služby VMM Management Serveru a nakonec samotného VMM Agenta na spravovaném serveru.

Kompletní soupis portů používaných VMM naleznete <a title="Ports and Protocols for VMM" href="http://technet.microsoft.com/en-us/library/gg710871.aspx" target="_blank">zde</a>.