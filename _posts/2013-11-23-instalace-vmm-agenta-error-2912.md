---
id: 698
title: 'Instalace VMM Agenta &#8211; Error 2912'
date: 2013-11-23T11:08:00+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=698
permalink: /2013/11/23/instalace-vmm-agenta-error-2912/
categories:
  - Hyper-V
  - Nezařazené
  - System Center
  - System Center 2012 R2
  - Windows Server 2012 R2
---
Jeden z dalších důvodů, proč nejde nainstalovat VMM agent na Hyper-V hostitele:

Scénář: Instalace VMM Agenta z VMM konzole s použitím RunAs účtu (domain user) s právy lokálního admina na Hyper-V hostiteli (účet je napevno v lokálních administrátorech).

Chyba:

> Error (2912)  
> An internal error has occurred trying to contact the host.domain.local server: : .
> 
> WinRM: URL: [http://host.domain.local:5985], Verb: [ENUMERATE], Resource: [http://schemas.microsoft.com/wbem/wsman/1/wmi/root/cimv2/Win32\_PerfFormattedData\_Tcpip_NetworkInterface], Filter: []
> 
> Unknown error (0xc0000bbb)
> 
> Recommended Action  
> Check that WS-Management service is installed and running on server lsghv10.learning.local. For more information use the command &#8222;winrm helpmsg hresult&#8220;. If lsghv10.learning.local is a host/library/update server or a PXE server role then ensure that VMM agent is installed and running. Refer to http://support.microsoft.com/kb/2742275 for more details.

Po mnoha různých pokusech o opravu jsem zjistil, že v lokálních adminech na Hyper-V hostiteli je účet služby VMM management serveru (ano, ten tam po instalaci má být), ale zároveň ještě stále RunAs účet použitý pro instalaci (ten tam po instalaci být nemá). Odebral jsem ho tedy a vše nyní funguje. Pravděpodobně se jedná o bug.

