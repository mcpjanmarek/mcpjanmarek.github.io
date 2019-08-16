---
id: 18
title: System Center Configuration Manager – Site Roles
date: 2010-05-07T12:31:00+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/05/07/system-center-configuration-manager-%e2%80%93-site-roles'
permalink: /2010/05/07/system-center-configuration-manager-site-roles/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!286')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!286')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SC Configuration Manager
---
<div id="msgcns!6E7B9216726D07B8!286" class="bvMsg">
  <p>
    <img style="margin:0 15px 0 0;" alt="System Center Configuration Manager" align="left" src="http://i.microsoft.com/global/systemcenter/en/us/PublishingImages/SysCnt-ConfigMgr_80.png" width="310" height="80" />
  </p>
  
  <p>
    SMS Provider<br />Plní roli zprostředkovatele (jak již název napovídá) mezi konzolou a systémem ConfigMgr. Skládá se z WMI (Wíndows Management Instrumentation) vrstev a je prostředníkem komunikace s databází. Samozřejme tím poskytuje jakousi úroveň zabezpečení přístupu a autentifikace a autorizace operací.
  </p>
  
  <p>
    Component Server<br />Jednoduše řečeno – každý server, který plní některou roli ConfigMgr je zároveň i Component Serverem. Je to server, který provozuje službu SMS Executive. Výjimkou je ale, pozor, role Distribution Point, která není Component Serverem.
  </p>
  
  <p>
    Distribution Point<br />Jedná se o roli, která vlastně existovala už v prapůvodním SMSku. Je zásadni pro distribuci balíčků na klienty. Historicky nebyl ale ničím víc, než jen promyšleným file serverem.Dnes ovšem s IIS je zdrojem instalačních balíčků pro klienty, kteří si je stahují pomocí technologie BITS. <br />Celkově jsou tři typy distribučních bodů
  </p>
  
  <p>
    &#8211; Distribution Point (DP) (výchozí instalace)
  </p>
  
  <p>
    &#8211; Protected Distribution Point (PDP)(chráněný – poskytuje balíčky pouze klientům, kteří spadají do nastavené Boundary na site serveru)
  </p>
  
  <p>
    &#8211; Branch Distribution Point (pobočkový &#8211; je to vlastně odlehčený [např. nezprostředkovává balíčky internet-based klientům] DP, ktery můžete nainstalovat na klientskou stanici na dané pobocce a tím nepotřebujete windows server system)
  </p>
  
  <p>
    Fallback Status Point (FSP)<br />Tato role je nově v ConfigMgr a je prostředníkem mezi správou stavu klientu a systémem ConfigMgr. Pokud pouzivate native mode (klient tedy musí mít certifikát), tak se může stát, že klientský certifikát vyprší nebo se poškodí. Tím klient zjednodušeně řečeno přestává komunikovat se systémem ConfigMgr. A v tuto chvíli přichází na scénu FSP. Přijímá stavové zprávy od takto „nefunkčních klientů“ a vy pak vidíte, kde je problém atd. Samozřejmě, že na FSP jdou i stavové zprávy o úspěšné instalaci klienta, reinstalaci atd.
  </p>
  
  <p>
    Management Point (MP)<br />Je prostřednikem mezi klientem a systémem ConfigMgr z pohledu celkove správy. Klient komunikuje vždy s MP, tudíž v každé hierarchii musí existovat min. jeden MP. Přes MP jde nastavení klienta, posílání Advertisements (nabídek balíčků), informace, na který DP se má klient obrátit; klient posílá na MP výsledky HW a SW inventur, atd. <br />Pokud nainstalujete MP na secondary site, MP získává status Proxy MP. Proč vůbec instalovat MP na secondary site? Z důvodu snížení provozu na síti. Proxy MP je totiž orientován na snížení zátěže linky směrem k a od rodičovské site. Pokud ale máte na secondary site pouze několik klientu, tak rozdíl pravděpodobně nezaznamenáte (myšleno rozdíl mezi komunikací klienta s proxy MP nebo rovnou s MP) <br />V některém z následujících článků se pokusím ještě popsat, jak probiha komunikace klienta s MP (příp. s PMP) a jak klient zjistí, na který MP se má podívat.
  </p>
  
  <p>
    PXE Service Point<br />Tato role se týká pouze distribuce operačních systémů (obrazů) na klientské stanice a jejím jediným úkolem je zpracovávat požadavky na PXE boot (Preboot Execution Environment boot)
  </p>
  
  <p>
    Reporting Point<br />Myslím, že o této roli ani není co psát. Setkáte se s ní snad u všech manage softwarů Microsoftu. Ke své funkci potřebuje IIS a ASP.NET a jednoduše vám zprostředkovává reporty ConfigMgr systému.
  </p>
  
  <p>
    Server Locator Point (SLP)<br />Jak opět sám název vypovídá, klient díky SLP získává informace o tom, ke které spadá ConfigMgr site, kde jsou instalační soubory pro ConfigMgr klienta a kde je jeho Management Point. <br />SLP klient použije ale až jako poslední možnost. Nejdříve se totiž tyto informace pokusí získat z Active Directory (s rozšířeným schématem pro ConfigMgr). <br />Ovšem samotný SLP klient najde v Active Directory. Tudíž bez AD se opravdu neobejdete.
  </p>
  
  <p>
    Software Update Point (SUP)<br />Je rolí, která poskytuje klientovi Windows záplaty pomocí služby Windows Server Update Services (WSUS), ke které si ConfigMgr nainstaluje pomocnou komponentu pro řízení distribuce záplat. Samotné stahování a instalace záplat probíhá na klientovi pomocí standardního Windows Update Agenta. <br />Často se mne klienti ptají, zda používat pouze WSUS nebo po implementaci přejít na SUP v ConfigMgr. Osobne si myslím, že pokud máte funkční WSUS, používejte ho dál. Ale samozřejmě SUP vám přinese možnost lepšího řízení patchování a navíc distribuci vlastních záplat a aktualizací (vytvořených např. pomocí System Center Update Publisher).
  </p>
  
  <p>
    State Migration Point (SMP)<br />Pokud víte, co je User State migrace (např. pomocí USMT), tak prakticky již není, co vysvětlovat. SMP je v podstatě takový obrácený Distribution Point. Během distribuce operačního systému se na SMP ukládají user state data (pokud v sekvenci použijete krok migrace dat).
  </p>
  
  <p>
    System Health Validator Point (SHVP)<br />Tuto roli můžete použít pouze v případě, že používáte NPS (Network Policy Service), resp. NAP (Network Access Protection) technologii. SHVP je tedy možné nainstalovat pouze na Windows Server 2008 s NPS. Následně SHVP kontroluje zdraví NAP-podporujících klientů a reportuje výsledky. Protože tyto výstupy jsou dále zasílány do Active Directory Domain Services a replikovány do Systems Management kontejneru, musíte mít pro tuto roli rozšířené Active Directory schéma pro ConfigMgr. <br />Na základě této role, se pak dá použít automatická karanténa klientů do oddělené site, pokud nesplňují určité požadavky apod.</div>