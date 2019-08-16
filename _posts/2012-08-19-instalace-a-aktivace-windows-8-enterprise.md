---
id: 545
title: Instalace a aktivace Windows 8 Enterprise
date: 2012-08-19T09:14:18+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=545
permalink: /2012/08/19/instalace-a-aktivace-windows-8-enterprise/
categories:
  - Nezařazené
  - Windows 8
---
Nemohl jsem čekat ani minutu a stáhl jsem nově dostupné ISO instalace Windows 8. Díky partner programu jsem objevil Enterprise edici s licenčním klíčem, takže hurá na to.

Vzhledem k tomu, že jsem člověk vrhající se do mnoha věcí pohlavě a také proto, že věřím funkčnosti RTM verze, jsem se rozhodl zformátovat stávající Windows 7 disk a nainstalovat Windows 8 načisto. Rád instaluji OS z flash disku, protože je to rychlé. Stačí tedy jen připojit USB flash disk (min. 4GB) a přes diskpart ho připravit:

> diskpart
> 
> list disk
> 
> select disk� _číslo\_disku\_z\_předchozího\_příkazu\_které\_reprezentuje\_USB\_flash_disk_
> 
> clean
> 
> create partition primary
> 
> format fs=ntfs quick
> 
> active
> 
> assign letter=X

poté stačí překopírovat obsah instalačního DVD (řekněme, že je reprezentován písmenem E:) na USB flash disk:

> xcopy E:\*.* X:\ /f/s/e

Nyní je již možné restartovat stanici a provést instalaci.

Po instalaci jsem ale narazil na menší problém s aktivací OS. Aktivace se nedařila a error hlásal něco ve znění, že nemůže nalézt KMS server. Ano, já ještě KMS server nemám, protože jednak sedím zrovna na hotelu a jednak protože ještě není k dispozici Windows Server 2012. Chtěl jsem tedy provést změnu licenčního čísla na MAK. Bohužel z Control panelu tlačítko na změnu zmizelo. Nevadí, použiji tedy příkazovou řádku a nástroj SLMGR a zadám MAK klíč:

> slmgr.exe -ipk� _licenční_číslo_

V tuto chvíli lze již spustit aktivaci nebo opět použít příkazovou řádku:

> slmgr.exe -ato

Problém vyřešen, OS zalicencován.