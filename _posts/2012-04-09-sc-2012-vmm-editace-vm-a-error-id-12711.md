---
id: 450
title: 'SC 2012 VMM &#8211; editace VM a Error ID 12711'
date: 2012-04-09T14:45:59+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=450
permalink: /2012/04/09/sc-2012-vmm-editace-vm-a-error-id-12711/
jabber_published:
  - "1333975562"
  - "1333975562"
publicize_results:
  - 'a:1:{s:7:"twitter";a:1:{i:76316228;a:2:{s:7:"user_id";s:11:"mcpjanmarek";s:7:"post_id";s:18:"189333359644770305";}}}'
  - 'a:1:{s:7:"twitter";a:1:{i:76316228;a:2:{s:7:"user_id";s:11:"mcpjanmarek";s:7:"post_id";s:18:"189333359644770305";}}}'
categories:
  - Hyper-V
  - Nezařazené
  - SC Virtual Machine Manager
---
Nedávno jsem narazil na chybu, která se často stává po manipulaci s CSV diskem, na kterém jsou umístěné VM.

Například vezměme v úvahu zvětšení disku figurujícího v clusteru jako CSV. Disk damé do maintenance modu, provedeme zvětšení a následně chceme například zeditovat velikost operační paměti VM pomocí SC2012VMM. Výstupem z operace je pak chyba podobná této:

> <span style="color:#ff0000;"><strong>Set-SCVirtualMachine : VMM cannot complete the WMI operation on the server (hyperv.domain.local) because of an error: [MSCluster_Resource.Name="9932aa98-99a2-4fff-8e6c-xxxxxxxxxxxx"] The cluster resource could not be found. (Error ID: 12711, Detailed Error: The cluster resource could not be found (0x138F))</strong></span>
> 
> <span style="color:#ffff00;"><a href="http://janmarek.eu/wp-content/uploads/2012/04/error_id_12711__error2.png"><img title="error_id_12711__error" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;" border="0" alt="error_id_12711__error" src="http://janmarek.eu/wp-content/uploads/2012/04/error_id_12711__error_thumb1.png" width="634" height="235" /></a></span>
> 
> <span style="color:#ff0000;"></span>

Když na této VM provedete operaci Repair s parametrem Ignore, nic se nezmění. Problém je totiž v konfiguraci VM na úrovni clusteru. Není aktuální. Proto je nutné provést Refresh konfigurace VM na úrovni clusteru (ne Refresh VM na úrovni SC2012VMM). Pro refresh všech VM v clusteru můžete použít např. tento powershell příkaz:

> <span style="color:#ffff00;"><strong>Get-ClusterResource -Cluster "název_hyperv_clusteru" | Where-Object {$_.ResourceType.Name -eq &#8218;Virtual Machine Configuration&#8216;} | Update-ClusterVirtualMachineConfiguration</strong></span>

Poté již lze v SC2012VMM konzoli opravit stav VM a následně provést samotnou editaci konfigurace.

[<img title="error_id_12711__refreshVM" class="alignleft size-full wp-image-452" style="margin:7px 14px 6px 0;" alt="" src="http://janmarek.eu/wp-content/uploads/2012/04/error_id_12711__refreshvm.png" width="467" height="448" />](http://janmarek.eu/wp-content/uploads/2012/04/error_id_12711__refreshvm.png)