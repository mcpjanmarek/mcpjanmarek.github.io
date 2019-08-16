---
id: 1079
title: Jak vytvořit Nano Server VM ve Windows Server 2016 TP4
date: 2016-01-07T07:33:29+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1079
permalink: /2016/01/07/jak-vytvorit-nano-server-vm-ve-windows-server-2016-tp4/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2016
tags:
  - Nano Server
---
### Co potřebujete?

  * Instalačku Windows Server 2016 TP4 (ISO)
  * Lokální disk s adresáři (třeba D:\ a D:\Hyper-V)

### Jak vytvořit VHDčko pro Nano Server VM?

  1. Mountněte ISO WS 2016 TP4. Řekněme, že se připojí jako disk E:.
  2. Spusťte PowerShell konzoli a použijte příkazy: 
      1. **cd E:\NanoServer**
      2. **Import-Module .\NanoServerImageGenerator.psm1**
      3. **New-NanoServerImage -MediaPath E:\ -BasePath .\Base -TargetPath D:\Hyper-V\nano1\nano1.vhd -ComputerName nano1 -GuestDrivers** 
          * MediaPath ukazuje na písmenko jednotky, která reprezentuje ISO WS 2016 TP4
          * BasePath je pracovní dočasný adresář, kde se bude vyrábět VHDčko
          * TargetPath je adresář, kam to vyhodí výsledné VHDčko
          * ComputerName je vnitřní název OS virtuálky
          * GuestDrivers je přepínač, proto tam není žádná hodnota, který říká, aby se injectly ovladače potřebné pro běh Nano Serveru ve virtuálce
  3. Výsledkem bude v TargetPath VHDčko (opravdu je to VHD a ne VHDX) o velikosti cca 450 MB.
  4. Teď už můžete jednoduše vyrobit VM s použitím tohoto VHD. Dejte pozor, že to musí být Generation 1 VM. Stačí jí naprosto 512 MB paměti.

### Jak nastavit Nano Server VM?

Hodně věcí se dá udělat rovnou s použitím autounattend.xml souboru, který injectnete do VHD během jeho vytváření. Pokud si ale chcete pohrát, můžete použít PowerShell Direct.

Nano Server má téměř nulové GUI. Tady je pár screenshotů:



Zapněte tedy Nano Server VM a na hostiteli použijte následující PowerShell příkazy:

  1. **Enter-PSSession -VMName Nano1**
  2. Do okna zadejte credentials pro připojení &#8211; tedy **Administrator a heslo**, které jste zadali v cmdletu New-NanoServerImage
  3. **Get-NetIPAddress** vám ukáže aktuální IP adresaci
  4. **New-NetIPAddress -InterfaceAlias &#8218;Ethernet&#8216; -IPAddress 192.168.88.55 -PrefixLength 24** vám nastaví statickou IP adresu
  5. **Set-DnsClientServerAddress -InterfaceAlias &#8218;Ethernet&#8216; -ServerAddresses 192.168.88.11** vám nastaví DNS server

Pro přidání do domény nemůžete použít Add-Computer cmdlet, jelikož v Nano Serveru není potřebný modul. Musíte ted provést offline domain join:

  1. Na nějaké stanici v doméně si vyrobíte BLOB objekt: **djoin.exe /provision /domain domain.local /machine nano1 /savefile .\odjblob**
  2. Výsledný blob po síti nebo přes **Copy-VMFile** přenesete do VM a v ní spustíte:** djoin /requestodj /loadfile c:\Temp\odjblob /windowspath c:\windows /localos**
  3. Uděláte restart třeba přes **shutdown -r -t 0**
  4. Nakonec zavřete session **Exit-PSSession**

Pokud byste opravdu chtěli použít Copy-VMFile, tak postup je následující:

  1. Musíte si povolit Guest Services a to buď v Hyper-V konzoli na Nano VM v Integration Services a nebo PowerShellem **Enable-VMIntegrationService -VM (Get-VM nano1) -Name &#8218;Guest Service Interface&#8216;**
  2. Zkopírujete si BLOB pomocí **Copy-VMFile -Name &#8218;nano1&#8216; -SourcePath D:\odjblob -DestinationPath C:\ -FileSource Host**

Další nastavování už je buď klasický PowerShell nebo si jen v Nano povolíte na firewallu remote management a použijete vzdáleně konzole.