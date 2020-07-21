---
id: 244
title: Site Server Role v System Center Configuration Manageru 2007
date: 2011-01-22T17:56:00+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/2011/01/22/site-server-role-v-system-center-configuration-manageru-2007/
permalink: /2011/01/22/site-server-role-v-system-center-configuration-manageru-2007/
jabber_published:
  - "1301158596"
  - "1301158596"
categories:
  - Nezařazené
  - SC Configuration Manager
tags:
  - Configuration Manager
  - SCCM
  - SCCM 2007
  - SCConfigMgr
---
**Tento článek si můžete přečíst především také na stránkách školícího centra WBI Systems: <http://learning.wbi.cz>**

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;float:left;padding-top:0;border:0;margin:0 10px 0 0;" title="1_6F99E53E" src="/wp-content/uploads/2011/03/1_6f99e53e_thumb.png" border="0" alt="1_6F99E53E" width="244" height="132" align="left" />](/wp-content/uploads/2011/03/1_6f99e53e.png)V tomto článku o System Center Configuration Manageru 2007 se zaměříme na role systému, jejichž znalost je zásadní pro následnou implementaci a celkové porozumění jeho jednotlivých funkcí. Instalací a konfigurací určité role „spouštíte“ na site serveru požadovanou funkcionalitu. Některé další role jsou využité interně a o jejich instalaci se starat nemusíte. Pojďme tedy hurá na ně!

## SMS Provider

Plní roli zprostředkovatele (jak již název napovídá) mezi konzolou a systémem ConfigMgr. Skládá se z WMI (Wíndows Management Instrumentation) vrstev a je prostředníkem komunikace s databází. Samozřejme tím poskytuje jakousi úroveň zabezpečení přístupu a autentifikace a autorizace operací.

## Component Server

Jednoduše řečeno – každý server, který plní některou roli ConfigMgr je zároveň i Component Serverem. Je to server, který provozuje službu SMS Executive. Výjimkou je ale, pozor, role Distribution Point, která není Component Serverem.

## Distribution Point

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;float:right;padding-top:0;border-width:0;margin:0 0 0 10px;" title="2_6F99E53E" src="/wp-content/uploads/2011/03/2_6f99e53e_thumb.png" border="0" alt="2_6F99E53E" width="194" height="244" align="right" />](/wp-content/uploads/2011/03/2_6f99e53e.png)  
Jedná se o roli, která vlastně existovala už v prapůvodním SMSku. Je zásadni pro distribuci balíčků na klienty. Historicky nebyl ale ničím víc, než jen promyšleným file serverem.Dnes ovšem s IIS je zdrojem instalačních balíčků pro klienty, kteří si je stahují pomocí technologie BITS.  
Celkově jsou tři typy distribučních bodů:

## Distribution Point (DP) (výchozí instalace)

Protected Distribution Point (PDP)(chráněný – poskytuje balíčky pouze klientům, kteří spadají do nastavené Boundary na site serveru)  
Branch Distribution Point (pobočkový &#8211; je to vlastně odlehčený [např. nezprostředkovává balíčky internet-based klientům] DP, ktery můžete nainstalovat na klientskou stanici na dané pobocce a tím nepotřebujete windows server system)  
Od releasu R2 na roli Distribution Point konfigurujeme také Streaming pro virtuální aplikace App-V.

## Fallback Status Point (FSP)

Tato role je nově v ConfigMgr a je prostředníkem mezi správou stavu klientu a systémem ConfigMgr. Pokud pouzivate native mode (klient tedy musí mít certifikát), tak se může stát, že klientský certifikát vyprší nebo se poškodí. Tím klient zjednodušeně řečeno přestává komunikovat se systémem ConfigMgr. A v tuto chvíli přichází na scénu FSP. Přijímá stavové zprávy od takto „nefunkčních klientů“ a vy pak vidíte, kde je problém atd. Samozřejmě, že na FSP jdou i stavové zprávy o úspěšné instalaci klienta, reinstalaci atd.

## Management Point (MP)

Je prostřednikem mezi klientem a systémem ConfigMgr z pohledu celkove správy. Klient komunikuje vždy s MP, tudíž v každé hierarchii musí existovat min. jeden MP. Přes MP jde nastavení klienta, posílání Advertisements (nabídek balíčků), informace, na který DP se má klient obrátit; klient posílá na MP výsledky HW a SW inventur, atd.  
Pokud nainstalujete MP na secondary site, MP získává status Proxy MP. Proč vůbec instalovat MP na secondary site? Z důvodu snížení provozu na síti. Proxy MP je totiž orientován na snížení zátěže linky směrem k a od rodičovské site. Pokud ale máte na secondary site pouze několik klientu, tak rozdíl pravděpodobně nezaznamenáte (myšleno rozdíl mezi komunikací klienta s proxy MP nebo rovnou s MP).  
V některém z následujících článků se pokusím ještě popsat, jak probiha komunikace klienta s MP (příp. s PMP) a jak klient zjistí, na který MP se má podívat.

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;float:left;padding-top:0;border:0;margin:0 10px 0 0;" title="3_6F99E53E" src="/wp-content/uploads/2011/03/3_6f99e53e_thumb.png" border="0" alt="3_6F99E53E" width="244" height="194" align="left" />](/wp-content/uploads/2011/03/3_6f99e53e.png)

## PXE Service Point

Tato role se týká pouze distribuce operačních systémů (obrazů) na klientské stanice a jejím jediným úkolem je zpracovávat požadavky na PXE boot (Preboot Execution Environment boot). Požadavky PXE je ochoten ConfigMgr obsluhovat pouze z autentifikovných klientů a to s využitím certifikátů. V případě režimu site Mixed Mode, lze využít buď Self-Signed Certificate nebo certifikát vydaný důvěryhodnou certifikační autoritou. Informace o této autoritě se zadávají také v konfiguraci PXE Service Pointu a to vložením root CA certifikátu.

## Reporting Point

Myslím, že o této roli ani není co psát. Setkáte se s ní snad u všech Microsoft systémů pro správu. Ke své funkci potřebuje IIS a ASP.NET a jednoduše vám zprostředkovává reporty ConfigMgr systému, které jsou vystaveny pomocí standardních integrovaných webových služeb ConfigMgr.

## Reporting Services Point (RSP)

Standardní reporting SCCM využívající Reporting Point roli nabízí pouze základní sadu reportů, které nemají příliš velké možnosti konfigurace výstupu a jsou zprostředkovávány rozhraním bez jakékoli možnosti přizpůsobení vzhledu. Proto bylo přistoupeno k využití SQL Server Reporting Services (SQLSRS), které nabízí širší funkcionality (výstup, export, „branding“). Pro komunikaci SCCM s SQLSRS je využita právě role RSP, která dále působí jako konektor pro konverzi web based reportů do reporů na SQLSRS.

## Server Locator Point (SLP)

Jak opět sám název vypovídá, klient díky SLP získává informace o tom, ke které spadá ConfigMgr site, kde jsou instalační soubory pro ConfigMgr klienta a kde je jeho Management Point.  
SLP klient použije ale až jako poslední možnost. Nejdříve se totiž tyto informace pokusí získat z Active Directory (s rozšířeným schématem pro ConfigMgr).  
Ovšem samotný SLP klient najde v Active Directory. Tudíž bez AD se opravdu neobejdete.

## Software Update Point (SUP)

Je rolí, která poskytuje klientovi Windows záplaty pomocí služby Windows Server Update Services (WSUS), ke které si ConfigMgr nainstaluje pomocnou komponentu pro řízení distribuce záplat. Samotné stahování a instalace záplat probíhá na klientovi pomocí standardního Windows Update Agenta.  
Často se mne klienti ptají, zda používat pouze WSUS nebo po implementaci přejít na SUP v ConfigMgr. Osobne si myslím, že pokud máte funkční WSUS, používejte ho dál. Ale samozřejmě SUP vám přinese možnost lepšího řízení patchování a navíc distribuci vlastních záplat a aktualizací (vytvořených např. pomocí System Center Update Publisher).

## State Migration Point (SMP)

Pokud víte, co je User State migrace (např. pomocí USMT), tak prakticky již není, co vysvětlovat. SMP je v podstatě takový obrácený Distribution Point. Během distribuce operačního systému se na SMP ukládají user state data (pokud v sekvenci použijete krok migrace dat).

## System Health Validator Point (SHVP)

Tuto roli můžete použít pouze v případě, že používáte NPS (Network Policy Service), resp. NAP (Network Access Protection) technologii. SHVP je tedy možné nainstalovat pouze na Windows Server 2008 s NPS. Následně SHVP kontroluje zdraví NAP-podporujících klientů a reportuje výsledky. Protože tyto výstupy jsou dále zasílány do Active Directory Domain Services a replikovány do Systems Management kontejneru, musíte mít pro tuto roli rozšířené Active Directory schéma pro ConfigMgr.  
Na základě této role, se pak dá použít automatická karanténa klientů do oddělené site, pokud nesplňují určité požadavky apod.

