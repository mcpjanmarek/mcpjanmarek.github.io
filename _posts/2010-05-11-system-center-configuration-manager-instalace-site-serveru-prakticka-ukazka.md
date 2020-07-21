---
id: 19
title: System Center Configuration Manager – instalace site serveru – praktická ukázka
date: 2010-05-11T09:31:54+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/05/11/system-center-configuration-manager-%e2%80%93-instalace-site-serveru-%e2%80%93-prakticka-ukazka'
permalink: /2010/05/11/system-center-configuration-manager-instalace-site-serveru-prakticka-ukazka/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!296')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!296')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SC Configuration Manager
---
<div id="msgcns!6E7B9216726D07B8!296" class="bvMsg">
  <p>
    <img style="display:inline;margin:0 15px 10px 0;" alt="System Center Configuration Manager" align="left" src="http://i.microsoft.com/global/systemcenter/en/us/PublishingImages/SysCnt-ConfigMgr_80.png" width="310" height="80" />Dnešním článkem bych vám chtěl přiblížit samotnou instalaci systému na jednom konkrétním scénáři. Chtěl bych poukázat na to, že se jedná o moje zjištění a zkušenost a ne o kuchařku „Tak takhle to nainstalujte“.
  </p>
  
  <p>
    Naše společnost bude mít centrální pobočku v Brně a oblastní v Praze. Tyto dvě lokality komunikují poměrně pomalou linkou. V Brně máme 1000 klientských stanic a 20 serverů a v Praze 100 stanic (samozřejmě s operačními systémy Windows). Klientské stanice nebudou vyžadovat rozdílnou konfiguraci intervalů pro software a hardware inventuru, ale na servery a stanice v Praze bychom rádi instalovali z odděleného distribučního bodu a samotné klienty také z Prahy. Celkově potřebujeme zajistit distribuci aplikací a to s využitím virtualizovaných aplikací a samozřejmě HW a SW inventarizaci z důvodu distribuce aplikací, přehledu modelů stanic atd. K dispozici máme rychlé disky na SAN a tři identické servery s quad-core procesory a celkem 32GB RAM v osmi modulech po 4GB.
  </p>
  
  <p>
    V tomto scénáři bych použil jednu primární site (BR1), která bude spravovat klientské stanice v Brně, jednu jí podřízenou sekundární site (BR2) pro servery v Brně a jednu sekundární site (PRG) v Praze pro správu klientů tam. Paměti bych osadil takto: BR1 site – 16GB, BR2 – 4GB a PRG – 4GB. A ještě nám 8GB zbylo. Na server, který bude hostovat site BR1 bych zároveň nainstaloval i samotnou databázi ConfigMgr s využitím MS SQL Server 2005 SP3 Standard Edition, a použil bych osm disků na SAN (1.HDD = 40GB pro OS, 2.HDD = 25GB pro ConfigMgr instalaci, 3.HDD = 5GB pro ConfigMgr logy, 4.HDD = 10GB pro SQL databázový soubor, 5. HDD = 10GB pro SQL soubor transakčního logu, 6.HDD = velikost dle balíčků – pro zdrojový share balíčků, 7.HDD = 5GB pro TEMP DB SQL a 8.HDD = velikost dle balíčků – pro distribuční bod). Pro BR2 a PRG bych použil dva HDD (1 pro OS a 1 pro ConfigMgr instalaci).
  </p>
  
  <p>
    Na všechny site servery nainstalujeme roli Web Server (IIS 7, Windows Authentication, URL Authorization), features BITS a Remote Differential Compression, WebDav pro IIS7 (musí se následně povolit a dokonfigurovat) a po instalaci ConfigMgr site serveru role Distribution Point (DP) a Management Point. Na BR1 bude navíc role Fallback Status Point, Server Locator Point a Reporting Point. Všechny site budou Protected dle Boundary, které bych konfiguroval nejlépe dle Active Directory site (které budou pro jednotlivé lokality).
  </p>
  
  <p>
    Zde je v bodech uvedeno, na co bych v konfiguraci dal pozor především (nutno konfigurovat více):
  </p>
  
  <p>
    &#8211; BR1
  </p>
  
  <p>
    o Vytvořit jednotlivé Address pro podřízené BR2 a PRG a konfigurovat tok dat<a href="http://janmarek.eu/wp-content/uploads/2010/10/15b85d.png" rel="WLPP"><img style="border-bottom:0;border-left:0;display:inline;margin-left:0;border-top:0;margin-right:0;border-right:0;" title="1" border="0" alt="1" align="right" src="http://janmarek.eu/wp-content/uploads/2010/10/15b85d.png?w=211" width="314" height="445" /></a>
  </p>
  
  <p>
    o Konfigurovat Boundary dle AD site pro hlavní lokalitu
  </p>
  
  <p>
    o Client Agents – intervaly inventarizace a aktualizace politik na klientech
  </p>
  
  <p>
    o Client Installation – Client Pust instalallation – doporučuji použít parametry viz. <a href="http://technet.microsoft.com/en-us/library/bb680980.aspx">http://technet.microsoft.com/en-us/library/bb680980.aspx</a>
  </p>
  
  <p>
    o Component Configuration – Software Distribution – nastavit úložiště balíčků na distrubčním bodu (8.HDD)
  </p>
  
  <p>
    oDiscovery Methods – použít Active Directory System Discovery
  </p>
  
  <p>
    o Na roli DP povolit streaming virtuálních aplikací
  </p>
  
  <p>
    &#8211; BR2 a PRG
  </p>
  
  <p>
    o Konfigurovat Boundary dle AD site pro BR2 a PRG
  </p>
  
  <p>
    o Client Installation – Client Pust instalallation (viz. výše)
  </p>
  
  <p>
    o Discovery Methods – použít Active Directory System Discovery na konkrétní OU
  </p>
  
  <p>
    o Na roli DP povolit streaming virtuálních aplikací
  </p>
  
  <p>
    
  </p>
  
  <p align="justify">
    <a href="http://janmarek.eu/wp-content/uploads/2010/10/25b45d.png" rel="WLPP"><img style="border-bottom:0;border-left:0;display:inline;border-top:0;border-right:0;margin:0 20px 0 0;" title="2" border="0" alt="2" align="left" src="http://janmarek.eu/wp-content/uploads/2010/10/25b45d.png?w=257" width="315" height="350" /></a> Jak jste si určitě všimli, pro distribuci samotných klientů ConfigMgr jsem použil metodu Client Push Installation (s discovery pomocí AD System Discovery). Samozřejmě, že je možné např. využít i Software Distribution deployment v Group Policy. Pro instalaci se použije ccmsetup.msi, který najdete v instalačním adresáři ConfigMgr na site serveru v podadresáři bini386. Dále je zásadní použít ADM template ConfigMgr2007Installation.adm pro nastavení instalačních parametrů, který naleznete na instalačním médiu ConfigMgr v adresáři ToolsConfigMgrAdmTemplates. A abychom vyhověli našemu scénáři, je nutne v parametrech použít minimálně /mp: a v něm nastavit pro příslušnou politiku příslušný management point odkud stahovat zdrojové soubory.
  </p>
  
  <p>
    V průběhu instalace celého systému ConfigMgr i klientů (ale i při následné správě) stále kontrolujte stav serverů a komponent v konzole ConfigMgr v položce System Status – Site Status.
  </p></p>
</div>