---
id: 1076
title: Co je nového ve Windows Server 2016 TP4 (Hyper-V)
date: 2016-01-07T06:21:28+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1076
permalink: /2016/01/07/co-je-noveho-ve-windows-server-2016-tp4-hyper-v/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2016
---
Už v listopadu 2015 byl uvolněn Technical Preview 4 pro Windows Server 2016. Další zlomový okamžik pro všechny, co se těší na příští� verzi Windows Serveru. Co je v TP4 nového kolem Hyper-V?

  1. Nano Server 
      * Vylepšení oproti TP3
      * Podpora kontejnerů
      * Podpora nested virtualizace (Hyper-V v Hyper-V)
      * Pro ty, co neví co to je &#8211; ultra ořezaný OS, který nemá žádné GUI (ani příkazovku) a tak jeho režie je cca 120 MB paměti a 450 MB dat na disku.
      * Pro ty, co se toho bojí ještě víc než se teď bojí Core Edice, mám skvělou zprávu &#8211; bude to preferovaný typ OS pro Hyper-V hostitele. Takže co teď? Hybaj� se naučit PowerShell!
  2. Podpora režimu Connected Standby 
      * Surface 4 a podobné devices používají nový AOAC režim. Hyper-V tak nemá problém běžet ani na nich.
  3. Discrete Device Assignment 
      * Možnost &#8222;protáhnout&#8220; z fyzického hostitele PCIe zařízení do VM. Především se teď jedná o NVMe a GPUčka.
      * Tato funkce nemá nic společného s Processor Affinity nebo podobně, které používají konkureční platformy.
  4. Hot Add paměti a síťovky 
      * Lze měnit velikost přidělené virtuální paměti (VM Static Memory) za běhu. A to jak přidávat, tak odebírat. Task Manager ve VM z toho dost blázní.
      * Lze přidávat a odebírat virtuální síťovky (VM Network Adapter) za běhu. VM přitom nejde do pauzy.
  5. Vylepšená Hyper-V konzole 
      * Podpora WS-MAN protokolu (konečně!)
      * Podpora alternativního přihlašování. Moc se hodí pro konzultanty, jako jsem já.
      * Podpora správy starších verzí Hyper-V, ale jen do Hyper-V 2012 (Windows 8/Windows Server 2012). Jestli máte ještě starší Hyper-V, tak už je opravdu čas udělat upgrade.
  6. Instalace Integration Services 
      * Už to nejde přes Hyper-V konzoli. Hyper-V hostitel už ani nemá v System32 adresáři náš oblíbený soubor vmguest.iso.
      * Bude se instalovat klasicky přes Windows Update
  7. Secure Boot pro Linuxy 
      * Do teď byl podporávan pro Secure Boot jen WS 2012+ a Windows 8 x64+
  8. Samotná nested virtualization 
      * Na tuhle funkci čekám od existence Hyper-V. Když si totiž potřebujete postavit Hyper-V lab, tak máte jen 2 možnosti &#8211; mít hoodně fyzického železa nebo použít VMware Workstation. Teď už ale rozjedete v Hyper-V virtuálku a v ní můžete nainstalovat Hyper-V a v něm vytvořenou virtuálku zapnout. Podporovány jsou i krásy jako NVGRE, Live Migration atd. atd. Má to ale několik limitů &#8211; ta virtuálka, co simuluje Hyper-V hostitele nemůže používat Dynamic Memory, CheckPointy, Saved State apod. To ale nevadí &#8211; už teď mám na svém domácím serveru postavený díky tomu Hyper-V lab se Scale-out File Serverem.
  9. Síťová vylepšení 
      * SET. Zní to jak nějaká ultra vědecká funkce, ale je to jen podpora teamingu přímo na úrovni Hyper-V switche. Dnes je možné použít pro Hyper-V switch taky teamované adaptery, ale musí se nejdříve udělat team pomocí NIC Teaming funkce.
      * RDMA podpora pro síťovky připojené k Hyper-V switchi.
      * Rozšířené možnosti nastavování QoS pro různé typy komunikací (aneb SDN, neboli Software Defined Networking, v SDDC, neboli Software Defined Data Center).
 10. Production CheckPoints 
      * Nejdříve je potřeba si říct, že aktuální CheckPointy nejsou na některých workloadech nepodporované a hlavně obecně nedoporučované (viz <a href="https://technet.microsoft.com/en-us/library/dn818483.aspx" target="_blank">tady</a>). Naše známé CheckPointy se budou ve WS 2016 jmenovat Standard (buďte rádi, čekal jsem, že je pojmenují Legacy nebo Deprecated nebo tak, aby je nikdo už nikdy nechtěl použít) a budou fungovat pořád tak, jako dnes. Nové Production CheckPointy jsou ale samozřejmě lepší a jsou nastavené by default. Fungují obdobně jako Standard, akorát že pro konzistentní propis dat používají ještě navíc VSS (takže klasicky přes IS do VM volají request).
 11. Rolling Cluster Upgrade 
      * Strašně se mi ten název líbí! Je to vylepšení procesu upgradu Hyper-V clusteru zaživa, jako jsme už viděli při migraci 2012 na 2012 R2. Tam šla Live Migration ale udělat je jedním směrem &#8211; verzí nahoru. Teď můžete VM migrovat tam i zpět, ale po tu dobu nemůžete používat krásné nové 2016 funkce. Celé je zařízeno přes verzi VM (pozor VERZI! ne generaci!), která nás doteď moc nezajímala, protože Hyper-V dělalo auto upgrade verze při importu VM, a taky přes Cluster Functional Level (což je něco jako DFL/FFL v ADčku, resp. má to podobné dopady).
 12. Shielded VM 
      * Dřív byl nejsilnější ITík ten, kdo měl v AD Enterprise Admina. S virtualizací už je ale nejsilnější ten, kdo má admina na Hyper-V hostech, jelikož může třeba vykopírovat VHDčka DCček a dělat pak offline útoky na AD databázi nebo se může připojovat adminům (kteří jsou hloupí) přes VMConnect do virtuálek apod. Shielded VM je kombinace několika security funkcí &#8211; virtuálního TPM chipu (novinka ve 2016) (čímž tedy můžete BitLockerovat data uvnitř VM), Host Resource Protection (taky novinka) a Secure Bootu. Díky tomu už Hyper-V admin nemá plnou kontrolu nad VM&#8230;. Rozlučte se tedy ale s klasickým troubleshootingem takových VM, protože jsou to pak super blackboxy.
 13. Storage QoS na SOFSu 
      * Teď nastavíte Storage QoS na virtuálním disku. Má to mraky nedostatků: co když chci nastavit limit per VM/private cloud/oddělení/zákazníka, co když chci nastavit limit per logický (no asi trochu zavádějící, ale lépe to popsat nejde) disk? Nelze. Microsoft sice nepřišel s tím, že jde nastavit Storage QoS na úrovni CSV disku (to si asi nechává do další verze), ale aspoň to budete moci nastavit na úrovni Scale-Out File Serveru. Problém je, že v ČR SOFS nikdo moc nepoužívá&#8230;
 14. Formát konfig souboru VM 
      * Ještě když Hyper-V nebylo úplně Hyper-V a celé to bylo moc podobné VirtualPC, které MS koupil s celým Connectixem, tak byla celá konfigurace VM v souboru VMC. Pak se ale řeklo, že to je blbost, že přeci vše má MS v XML, tak i VM musí mít XML. Teď se ale přišlo na to, že se v tom XML admini vrtaj a že je to vlastně celé k ničemu a že bude lepší udělat zbrusu nový převratní binární formát konfig souboru, který bude mít koncovku (světě div se) VMCX. Taky se mění VSV a BIN stavové soubory na VMRS (RS = Runtime State).
 15. PowerShell Direct 
      * Pro admina nejlepší funkce ze všech. Vezmete cmdlet Invoke-Command třeba a pustíte ho z hostitele s parametrem VMName. Tím zavoláte daný ScriptBlock přímo ve VM. A v ní NEmusíte mít povolený PowerShell Remoting!!! Cool, co? A víte, na co je to také� řešení? Na ten zpropadený Nano Server, který nejde nijak moc nastavovat.

Průbežně sem přihazuji další features, tak si klidně post někam uložte a mrkněte za měsíc nebo tak znovu.

A jestli vás to zajímá více, tak přijďte na <a href="http://www.hypercon.cz" target="_blank">HYPERCON</a>!!!