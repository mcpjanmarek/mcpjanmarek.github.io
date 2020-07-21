---
id: 1124
title: Sítě v Hyper-V Clusteru
date: 2016-05-20T20:09:58+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1124
permalink: /2016/05/20/site-v-hyper-v-clusteru/
categories:
  - Failover Cluster
  - Hyper-V
  - Nezařazené
  - Windows Server 2012 R2
tags:
  - Hyper-V
  - WFC
---
Jinými slovy, sítě potřebné pro Windows Failover Cluster (WFC) sloužící k provozu vysoce dostupných VM.

V dnešním článku se zaměřím právě na sítě, které potřebujete k provozu stabilního Hyper-V clusteru. Sítě clusteru se v základu dělí na 3 typy:

  1. Síť využitá pouze pro cluster komunikaci.
  2. Síť využitá jak pro cluster komunikaci, tak připojení vnějších zařízení (klientů).
  3. Síť, na které je cluster komunikace zakázána.

Zvolení vhodného typu sítě lze provést přímo přes Failover Cluster Manager (dále jen FCM) nebo za použití PowerShellu (property _Role_ na objektu _Cluster Network_, Get-ClusterNetwork).

Aby bylo jasné toto rozdělení, uveďme si pár příkladů.

  1. Cluster Heartbeat
  2. Cluster Management
  3. iSCSI konektivita

V rámci jednotlivých nodů clusteru je každý Hyper-V host připojen do těchto cluster sítí pomocí virtuálních adapterů WFC. Tyto koncové endpointy jsou interpretovány NetFT (Network Fault-Tolerant) adapterem (v Device Manageru ho najdete pod skrytým zařízením „Microsoft Failover Cluster Virtual Network Adapter“). Ten byl zaveden od Windows Server 2008 v rámci naprosto přepsaných funkcionalit WFC a jsou pomocí něj zajištěny klíčové funkce.

MAC toto adapteru je vytvořena z MAC fyzického adapteru. Ovladačem je Cluster Virtual Miniport Driver (netft.sys), který běží v kernel modu (ring 0) a běží vždy současně s cluster službou.

Když prozkoumáte IP konfigurace tohoto síťové rozhraní, tak najdete na IPv4 nastavenou APIPA a na IPv6 Link-Local adresu. Není potřeba tyto adresy jakkoli měnit (ani to není obecně dobrý nápad dělat), jelikož veškerá tato komunikace je tunelována přes odpovídající validní síťové rozhraní.

Co se týče „tvrdých“ požadavků na sítě v Hyper-V clusteru, tak existuje jen jediný: mít dostupné minimálně dvě sítě pro cluster komunikaci.

Díky tomu je NetFT spolu s dalším komponentami (Topology Manager, FTI, Interface Manager) schopen například postavit celou routovací strukturu, aby byla zajištěna maximální míra vysoké dostupnosti.

Není samozřejmě nejvhodnější konfigurace postavit cluster pouza na dvou sítích, protože je pak např. nedostatečně zajištěna potřebná šířka pásma pro jednotlivé typy komunikace a tím hrozí snížení vysoké dostupnosti.

Typy samotných komunikací v rámci clusteru lze rozdělit takto:

  1. Cluster komunikace
  2. Komunikace pro správu clusteru

  * Komunikace VM

  1. Live Migration
  2. Komunikace na úložiště
  3. Komunikace Hyper-V Replica

Nejdůležitějším požadavkem pro následné samotné rozdělení na logické sítě je existence odlišných dedikovaných sítí. Nelze v rámci WFC definovat sítě pro rozdílné typy komunikace na identických subnetech.

Pro oddělení **cluster komunikace** se používá již zmíněné nastavení na začátku článku. V rámci této sítě “tečou” i jedny z nejdůležitějších komunikací clusteru – cluster heartbeat (HB). Ty jsou malé, ale velice citlivé na latenci. Pokud neprojde HB z jednoho nodu na druhý, může být tato situace interpretována jako výpadek nodu. Je tedy také ještě velmi vhodné nastavit pomocí QoS prioritu (802.1p PCP hodnota) na komunikaci na portu, který HB používá (unicast UDP 3343) pomocí PowerShellu (New-NetQoSPolicy –IPDstPort 3343 –Piority 6)

Pro zvolení **sítě pro správu** je vhodné ještě toto nastavení kombinovat s určitou formou zabezpečení komunikace (které možná stejně je požadáno), čímž jste následně schopni tuto komunikaci rozpoznat.

**Komunikace VM** není v rámci clusteru nutné žádným způsoben definovat, jelikož se jedná o data tekoucí přes rozhraní, které nemá vůbec aktivní TCP/IP stack (externí Hyper-V switch) a proto není clusterem jakkoli využívané.

**Live Migration** (LM) je v rámci funkcionalit Hyper-V samotného možné nastavit na TCP (výchozí stav je s komprimací) nebo SMB (s využitím SMB Direct v případě použití síťových karet podporujících RDMA). Oddělení komunikace je nastaveno přímo v FCM, kde se checkboxy volí požadované sítě pro LM, nebo pomocí PowerShellu, kde se naopak nastavuje parametr sítí, které nemají být použity pro LM (Set-ClusterParameter –Name MigrationExcludeNetwork).

**Komunikace s úložištěm** může být částěčně dána přenosovým médiem a protokolem (např. v případě FC tedy není opět nutné nic oddělovat, jelikož se nejedná o síť s TCP/IP). Pokud se jedná o blokový přístup (např. iSCSI), tak je vhodné na těchto sítích zakázat cluster komunikaci (opět viz. začátek článku). Pokud se jedná o SMB úložiště, tak je tok dat řízen pomocí SMB Multichannel, kde pomocí PowerShellu opět vymezíme dedikované sítě (New-SMBMultichannelConstraint).

K omezení **komunikace Hyper-V replikace** lze použít jedině trvalé statické routy (route add –p).

Trochu ošemetnou otázkou ještě zůstává, co dělat s **metadaty a případným redirected přístupem u Cluster Shared Volume** (**CSV**). Důležitou částí odpovědi je fakt, že od Windows Server 2012 používá CSV vždy pro metadata SMB protokol, tedy konkrétně SMB Multichannel. Tím je zajištěn maximální možný výkon v případě redirected accesu (tedy funkci, která se používá, když některý z nodů clusteru ztratí přímý přístup k úložišti). Jelikož SMB Multichannel je použit i pro metadata, použije se síť, které má povolenou SMB MC komunikaci. Pokud není dostupná žádná síť s SMB MC, tak je zpětně komunikace přepnuta na NetFT. V tom případě se použije cluster síť s nejnižší metrikou. Metriky si ve výchozím stavu řídí cluster sám automaticky, ale je možné je nastavit na vlastní hodnotu (Get-Cluster Network). Vhodné je také nastavit opět QoS obecně pro SMB (New-NetQoSPolicy –SMB –MinimumBandwidthWeightAction).

Závěrem bych ještě rád upozornil na to, že vaše Hyper-V servery mohou (a v mnoha případech by měly) mít další typy komunikace, které bude nutné/vhodné izolovat v rámci clusteru (např. backup). Nezapomínejte také na závislosti jendotlivých používaných funkcí, které celkově značně ovlivňují síťovou architekturu WFC (např. NIC Teaming vs. SMB Multichannel, FCoE, HNV apod.)

