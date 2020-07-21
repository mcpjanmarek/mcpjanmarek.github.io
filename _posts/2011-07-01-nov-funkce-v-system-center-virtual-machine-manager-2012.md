---
id: 296
title: Nové funkce v System Center Virtual Machine Manager 2012
date: 2011-07-01T10:55:07+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/2011/07/01/nov-funkce-v-system-center-virtual-machine-manager-2012/
permalink: /2011/07/01/nov-funkce-v-system-center-virtual-machine-manager-2012/
jabber_published:
  - "1309510509"
  - "1309510509"
categories:
  - Nezařazené
  - SC Virtual Machine Manager
tags:
  - SCVMM
  - SCVMM 2012
  - System Center Virtual Machine Manager
---
**Tento článek si můžete přečíst především také na stránkách školícího centra WBI Systems: <http://learning.wbi.cz>**

V předchozím článku jsme prošli instalaci budoucího nástupce System Center Virtual Machine Manageru – verzi 2012. Nyní se pojďme blíže seznámit s novými funkcemi, které nám 2012ka nabídne. Samozřejmostí je podpora všech „vymožeností“, které přináší Service Pack 1 pro Windows Server 2008 R2 (Dynamic Memory, RemoteFX).

### Privátní Cloud

Funkce vytvoření a správy privátních cloudů poskytuje možnosti oddělení spravovaných prostředí a jejich resource konfiguraci. Můžete díky ní jednoduše řídit oprávnění k virtuálním strojům či službám, nastavovat, na kterých hostitelích cloud poběží, množství zdrojů hostitele, jež může cloud využít a samozřejmě konkrétní nastavení Performance and Resource Optimization (PRO) funkce.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="1" border="0" alt="1" src="/wp-content/uploads/2011/07/1_thumb.png" width="244" height="191" />](/wp-content/uploads/2011/07/1.png)

### Poskytované služby a šablony

Pomocí nástroje Service Template Designer jste schopni vytvořit šablony struktur poskytovaných služeb. Na základě těchto šablon je pak možné velice rychle vytvářet hierarchie a topologie prostředí pro konkrétní systémy. Např. vytvořit Sharepoint Farmu o specifickém množství front-endů, clusterovaném SQL Serveru o daném množství nódů atd.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="2" border="0" alt="2" src="/wp-content/uploads/2011/07/2_thumb.png" width="244" height="152" />](/wp-content/uploads/2011/07/2.png)

### Citrix XenServer jako hostitel

Nová verze VMM rozšiřuje podporované spravované virtualizační hostitele o Citrix XenServer. Vzhledem k použití profilů při konfiguraci hostitele můžeme pravděpodobně očekávat plynulejší a snadnější rozšiřitelnost o další hostitele či jejich nové verze.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;margin:0;" title="3" border="0" alt="3" src="/wp-content/uploads/2011/07/3_thumb.png" width="230" height="244" />](/wp-content/uploads/2011/07/3.png)[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="4" border="0" alt="4" src="/wp-content/uploads/2011/07/4_thumb.png" width="262" height="116" />](/wp-content/uploads/2011/07/4.png)

&#160;

### Fabric Storage Management

Pro mě osobně jedna z nejlepších funkcí. Integrace správy diskového pole přímo do VMM, resp. vytváření logických disků a mapování informací o těchto úložištích k hostitelům a clusteru. Tato funkce je podporovaná ale pouze pro Hyper-V hostitele. Zapotřebí je ovšem management pole podporující SMI-S (z toho částečně vyplývá i podpora polí: HP StorageWorks Enterprise Virtual Array (EVA) (toto pole nám běží v infrastruktuře školítka WBI Learning), NetApp FAS, EMC Symmetrix a CLARiiON CX)

### Server App-V balíčky

Virtualizací aplikací se zabývám již dlouhou dobu, a proto jsem netrpělivě čekal, co se bude skrývat pod názvem SERVER APP-V. A je opravdu na co se těšit. Server App-V funguje podobně jako dnes známé Client App-V: odděluje aplikaci od operačního systému, či od dalších jiných aplikací, které na něm běží a tím řeší problémy kompatibility a velice zásadně urychluje distribuci aplikace. Server App-V těchto vlastností využívá k distribuci předkonfigurovaných webových aplikací, konfigurovaných instalací SQL Server a díky tomu vám umožňuje před Service Template Designer postavit infrastrukturu jako stavebnici. 

K vytvoření Server App-V balíčků slouží speciální Server Application Virtualization Sequencer a aplikace bude distribuována přímo z konzole VMM 2012 (v tuto chvíli lze distribuovat balíčky pouze Powershellem manuálně) na každý virtuální stroj, kde je nainstalován Server App-V klient.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="5" border="0" alt="5" src="/wp-content/uploads/2011/07/5_thumb.png" width="244" height="132" />](/wp-content/uploads/2011/07/5.png)

### Instalace Hyper-V a Patch Management

Další novinkou je přímá instalace operačního systému s rolí Hyper-V či Hyper-V serveru přímo z konzoly VMM. K tomu slouží konfigurace s existujícím PXE Serverem, který vyřizuje požadavky na síťovou instalaci operačního systému. Můžete využít existující WDS server či PXE Service Point běžící na System Center Configuration Manageru (SCCM). S tímto také souvisí propojení s existujícím WSUS serverem či opět Software Update Pointem na SCCM, jenž umožňuje patchovat jednotlivé servery infrastruktury VMM a hotové šablony virtuálních strojů uložené v library.

### Dynamic a Power Optimization

Ve VMM 2008 jste pro automatický balancing virtuálních serverů mezi hostitele museli použít integraci se System Center Operations Managerem v rámci Performance and Resource Optimization (PRO). Ve verzi 2012 bude tuto funkci plnit již samotný VMM server díky Dynamic Optimization. Po konfiguraci parametrů je možné volitelně zapnout i automatickou dynamic optimization. 

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="6" border="0" alt="6" src="/wp-content/uploads/2011/07/6_thumb.png" width="244" height="103" />](/wp-content/uploads/2011/07/6.png)

Úspora energie je také jednou z důležitých témat v IT. SC VMM 2012 vám v této oblasti přináší automatické vypnutí hostitele, na kterém neběží žádné služby či virtuální servery (které mohou být automaticky „stěhovány“ pomocí zmíněné Dynamic Optimization). Konfigurovat můžete schedule, kdy se může provádět úspora energie.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="7" border="0" alt="7" src="/wp-content/uploads/2011/07/7_thumb.png" width="244" height="111" />](/wp-content/uploads/2011/07/7.png)

### Důležité změny ve verzi 2012

V rámci Self-Service (S-S) provisioningu už nemusí S-S User přistupovat k prostředí přes S-S Portal. Nově může využít plnohodnotnou konzolu VMM, kde se mu zobrazí samozřejmě jen moduly, ke kterým má práva.

Bohužel již není možné využít pro databázi VMM serveru SQL Server Express. Také nejsou již podporované hostitelé VMware ESX 3.0/ESXi 3.0 či Microsoft Virtual Server 2005.

