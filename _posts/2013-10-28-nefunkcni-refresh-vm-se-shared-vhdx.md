---
id: 650
title: Nefunkční Refresh VM se Shared VHDX
date: 2013-10-28T19:40:36+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=650
permalink: /2013/10/28/nefunkcni-refresh-vm-se-shared-vhdx/
categories:
  - Hyper-V
  - Nezařazené
  - System Center 2012 R2
  - Windows Server 2012 R2
---
Dnes jsem v System Center 2012 R2 Virtual Machine Manager konzoli našel pravděpodobně bug. Pokud se pokusíte provést Refresh akci na virtuálním počítačí generace 2, který používá sdílený VHDX, tak získáte jen chybovou hlášku (error 2912):

> The requested operation cannot be performed on the virtual disk as it is currently used in shared mode (0xC05CFF0A)

[<img class="alignleft size-full wp-image-651" alt="refresh-gen2vm-shared-vhdx-error" src="/wp-content/uploads/2013/10/refresh-gen2vm-shared-vhdx-error.png" width="1080" height="231" />](/wp-content/uploads/2013/10/refresh-gen2vm-shared-vhdx-error.png)

Refresh u ostatních VM probíhá bez problémů. Na chybu konfigurace to u mne v tuto chvíli také nevypadá.

Jedná se tedy pravděpodobně o bug produktu. Budu vás dále informovat o případném řešení.

UPDATE 30.1.2014: Včera vyšel UR1 pro SC 2012 R2 VMM a řeší krom jiného i tuto chybu. Více info <a href="http://janmarek.eu/vysel-update-rollup-1-pro-system-center-2012-r2/" target="_blank">zde</a>.

