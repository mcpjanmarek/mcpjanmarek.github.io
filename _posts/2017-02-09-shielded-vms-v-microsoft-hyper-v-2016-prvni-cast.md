---
id: 1679
title: Shielded VMs v Microsoft Hyper-V 2016 (první část)
date: 2017-02-09T22:46:56+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1679
permalink: /2017/02/09/shielded-vms-v-microsoft-hyper-v-2016-prvni-cast/
categories:
  - Hyper-V
  - Hyper-V
  - Windows Server 2016
  - Windows Server 2016
tags:
  - Hyper-V 2016
  - Shielded VM
---
## O co se jedná?

Shielded VM je virtuální stroj, jehož data jsou chráněna kombinací několika spolupracujících technologií, které byly představeny ve Windows Server 2016. Velkou výhodou je ochrana VM jak v jejím statickém stavu (běží na některém Hyper-V hostiteli a má někde uložena data), tak ve chvíli jejího přesunu (při Live Migration, SNLM apod.)

<figure id="attachment_1680" aria-describedby="caption-attachment-1680" style="width: 300px" class="wp-caption aligncenter">[<img class="wp-image-1680 size-medium" src="http://janmarek.eu/wp-content/uploads/2017/02/ws2016-virtmgmt-vm-gen2-security-300x292.png" width="300" height="292" srcset="/wp-content/uploads/2017/02/ws2016-virtmgmt-vm-gen2-security-300x292.png 300w, /wp-content/uploads/2017/02/ws2016-virtmgmt-vm-gen2-security.png 440w" sizes="(max-width: 300px) 100vw, 300px" />](http://janmarek.eu/wp-content/uploads/2017/02/ws2016-virtmgmt-vm-gen2-security.png)<figcaption id="caption-attachment-1680" class="wp-caption-text">Security nastavení Gen 2 VM v Hyper-V 2016</figcaption></figure>

## Proč by mě to mohlo/mělo zajímat?

Hned z několika důvodů a to například:

  * Provozuji infrastrukturu pro své zákazníky a chci jim dát maximální jistotu zabezpečení jejich informací
  * Provozuji infrastrukturu pro své kolegy a chci jim dát maximální jistotu zabezpečení jejich informací
  * Někdo pro mě provozuje infrastrukturu a já chci mít maximální jistotu zabezpečení mých informací

Ono totiž nění úplně málo způsobů, jak se „dostat“ k datům uvnitř VM. Například zevnitř:

  * Hyper-V admin může cokoli – vykrádat RAM VM, mountovat VHDčka a odnášet data, kdykoli se připojovat do VM apod.
  * Síťový admin může také hodně – sniffovat traffic VM, krást RAM VM během její Live Migration apod.
  * Storage admin, backup admin, domain admin, a další nemají také moc svázané ruce něco nepěkného provést&#8230;

Útoky zvenku nebudu rozvádět, protože si asi dokážete představit do jakých oblastí bych musel zabrousit.

## Co k tomu potřebuji?

Záleží na režimu nastavení a provozu, o kterém se dozvíte dále, ale vesměs se celé řešení skládá ze tří hlavních komponent &#8211; Host Guardian Service (HGS), Guarded Hosts a samotných Shielded VMs.

### Host Guardian Service

Jedná se o roli Windows Serveru 2016, která zajišťuje atestaci Hyper-V hostitelů (tzv. Guarded Hosts) a ochranu klíčů, které jsou použité k ochraně dat (šifrování VHD bitlockerem, šifrování dat při Live Migration apod.).

<figure id="attachment_1681" aria-describedby="caption-attachment-1681" style="width: 300px" class="wp-caption aligncenter">[<img class="wp-image-1681 size-medium" src="http://janmarek.eu/wp-content/uploads/2017/02/ws2016-servermanager-hgs-role-300x204.png" width="300" height="204" srcset="/wp-content/uploads/2017/02/ws2016-servermanager-hgs-role-300x204.png 300w, /wp-content/uploads/2017/02/ws2016-servermanager-hgs-role.png 529w" sizes="(max-width: 300px) 100vw, 300px" />](http://janmarek.eu/wp-content/uploads/2017/02/ws2016-servermanager-hgs-role.png)<figcaption id="caption-attachment-1681" class="wp-caption-text">HGS role ve Windows Server 2016</figcaption></figure>

### Guarded Host

Vlastně se jedná o krásný název pro chráněný Windows Server 2016 s rolí Hyper-V. Chráněným se váš hostitel stane až ve chvíli, kdy atestační služba HGS validuje jeho identitu a konfiguraci. Jinými slovy, potvrdí, že se na něj můžete z pohledu bezpečnosti spolehnout (že např. neobsahuje škodlivý kód, nemá pozměněné boot záznamy, že má aktivní Virtulization-Based Security (VBS), dostupné požadované bezpečnostní technologie a hardware atd.)

### Shielded VM

K vysvětlení v úvodu článku zde doplním, že se jedná o VM generace 2, která používá virtuální TPM (vTPM) k ochraně dat uvnitř svých VHD pomocí BitLockeru a jejíž obsah paměti (a případně saved state) je také chráněn.

## Režimy ochrany Shielded VM

Spíše se jedná o režimy zabezpečení dat, atestace a řízení přístupu k TK (Transport Key), které umožňují odemykat a spouštět Shielded VM na Guarded Hosts.

### TPM Trusted Attestation

Jedná se právě o tu nejsilnější formu atestace, která má ovšem největší nároky na konfiguraci a komponenty (UEFI 2.3.1, Secure Boot, TPM 2.0). Hyper-V hostitel se stává Guarded Hostitelem ve chvíli, kdy má dostupný a nastavený TPM, zabezpečený boot a vygenerované a platné Code Integrity (CI) politiky.

### Admin Trusted Attestation

Forma atestace, kdy nepotřebujete žádný super nový hardware (především TPM 2.0) a kdy chcete poměrně snadno zvýšit zabezpečení vašich VM. Hyper-V hostitel se stává Guarded Hostitelem ve chvíli, kdy HGS ověří jeho členství v požadované AD Security Group. Tedy opravdu jednoduchý scénář.

Všimněte si, že v obou režimech má ovšem finální slovo HGS a proto je samozřejmostí zajištění jejího zabezpečení (vytváří se dedikovaný AD Forest) a její dostupnosti (Clustering). Pokud vám totiž HGS nedá TK a to buď protože vám (hostiteli) nevěří nebo prostě jen není dostupná, tak VM ani nezapnete.

## Chápu. A co dál?

V další části si nejdříve zkusíme blíže ukázat celé fungování HGS, GH a Shielded VMs, a tím si připravíme půdu na konfiguraci – nejdříve bez Microsoft System Center 2016 a poté s ním.

&nbsp;