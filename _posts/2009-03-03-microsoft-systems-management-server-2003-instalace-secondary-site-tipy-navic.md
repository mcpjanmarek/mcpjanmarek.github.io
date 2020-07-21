---
id: 28
title: Microsoft Systems Management Server 2003 – instalace secondary site + tipy navíc
date: 2009-03-03T13:34:00+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2009/03/03/microsoft-systems-management-server-2003-%e2%80%93-instalace-secondary-site-tipy-navic'
permalink: /2009/03/03/microsoft-systems-management-server-2003-instalace-secondary-site-tipy-navic/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!338')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!338')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - Systems Management Server
---
<div id="msgcns!6E7B9216726D07B8!338" class="bvMsg">
  <pre><a href="http://janmarek.eu/wp-content/uploads/2010/10/sms20035b45d.png" rel="WLPP"><img style="border-bottom:0;border-left:0;display:inline;border-top:0;border-right:0;margin:0 15px 0 0;" title="sms2003" border="0" alt="sms2003" align="left" src="/wp-content/uploads/2010/10/sms20035b45d.png?w=300" width="240" height="59" /></a></pre>
  
  <p>
    1. instalace OS na nový Windows Server + aplikace nejnovějších WSUS patchů
  </p>
  
  <p>
    2. konfigurace IP adresy
  </p>
  
  <p>
    3. přidání serveru do domény
  </p>
  
  <p>
    4. instalace IIS (přes Add/remove components windows (BITS, Common Files, IIS Manager, Active Server Pages, WebDAV a WWW Service)
  </p>
  
  <p>
    5. pokud byla instalace IIS provedena až po instalaci .NET Frameworku, je zapotřebí přeregistrovat ASP.NET (pomocí "aspnet_regiis.exe -i" konkrétního .NETu)
  </p>
  
  <p>
    6. povolit ASP.NET v IIS Web Extensions
  </p>
  
  <p>
    7. do lokální skupiny Administrators na novém serveru, přiřadit local system účet již exstujícího Primary Serveru
  </p>
  
  <p>
    8. do lokální skupiny Administrators na novém serveru, přiřadit doménovou skupinu "SMS Admins"
  </p>
  
  <p>
    9. přiřadit účet nového serveru do lokální skupiny SMS_SiteSystemToSiteServerConnection_kódprimarysite na Primary Serverunvsms
  </p>
  
  <p>
    10. pokud je Primary server zároveň i SQL Site Serverem (má na sobě i SQL databázi SMS) &#8211; přiřadit účet nového serveru do lokální skupiny SMS_SiteSystemToSQLConnection_kódprimarysite na Primary Serveru
  </p>
  
  <p>
    11. pokud není Primary Server zároveň i SQL Site Serverem (SQL databáze SMS je na jiném Site Serveru) &#8211; přiřadit účet nového serveru do lokální skupiny SMS_SiteSystemToSQLConnection_kódprimarysite na SQL Site Serveru (který je nositelem SQL databáze SMS)
  </p>
  
  <p>
    12. local systém účtu nového serveru přidat práva Active Directory Schema Admins (nejlépe jej přidat do doménové skupiny "SMS Schema Admins", kterým dát práva Active Directory Schema Admins)
  </p>
  
  <p>
    13. instalace SMS Secondary Site z instalačních CD SMS2003
  </p>
  
  <p>
    14. aplikace nejnovějšího servicepacku na SMS2003
  </p>
  
  <p>
    15. případná instalace patche International Client SMS2003 (pro podporu např. češtiny)
  </p>
  
  <p>
    16. do nově vzniklé lokální skupiny "SMS_SiteSystemToSiteServerConnection_kódnovéhosecondaryserveru" na novém serveru, přiřadit local system účet již existujícího Primary Serveru
  </p>
  
  <p>
    17. do nově vzniklé lokální skupiny "SMS_SiteToSiteConnection_kódnovéhosecondaryserveru" na novém serveru, přiřadit local system účet již existujícího Primary Serveru
  </p>
  
  <p>
    18. do lokální skupiny "Distributed COM Users" na novém serveru, přiřadit všechny doménovou skupiny, které mají určitá práva ke konzoli SMS2003
  </p>
  
  <p>
    19. v konzole SMS2003 v nastavení Primary Site -> Site Settings -> Adresses -> zde vytvořit adresu pro nový secondary server
  </p>
  
  <p>
    20. v konzole SMS2003 nakonfigurovat nový secondary server
  </p>
  
  <p>
    21. odeslat stávající balíčky na nový secondary server (pokud je na něm role Distribution Point)
  </p>
  
  <p>
    Troubleshooting Flowcharts k SMS 2.0
  </p>
  
  <p>
    &#8211; troubleshooting flowcharts pro Systems Management Server 2.0, použitelné i pro SMS 2003
  </p>
  
  <p>
    <a href="http://technet.microsoft.com/en-us/library/cc879043">http://technet.microsoft.com/en-us/library/cc879043</a>
  </p>
  
  <p>
    utilitky zdarma od 1E pro SMS
  </p>
  
  <p>
    &#8211; utilitky jsou sice psány pro SMS 2.0, ale jsou použitelné i pro SMS 2003 i SCCM 2007
  </p>
  
  <p>
    1E Free Tools<br /> <a href="http://1e.com/Downloads/FreeTools/Index.aspx">http://1e.com/Downloads/FreeTools/Index.aspx<br /> </a>
  </p>
  
  <p>
    &#8211; určitě stojí za zkoušku
  </p>
  
  <p>
    URL pro otestování/troubleshooting Management Pointu
  </p>
  
  <p>
    Často potřebujete nějaký základní test, jak od klienta zjistit zda běží (správně) role Management Pointu na SMS Site serveru, nebo zda na něj klient vůbec vidí? Vyzkoušejte následující dva linky.
  </p>
  
  <p>
    http://nazev_sms_serveru/sms_mp/.sms_aut?mplist &#8211; vrátí seznam distribučních bodů ve formátu XML<br /> http://nazev_sms_serveru/sms_mp/.sms_aut?mpcert &#8211; vrátí certifikát daného Management Pointu
  </p>
  
  <p>
    Tyto linky samozřejmě otestují i funkčnost IIS komponenty, ASP.NET atd.<br /> Funkční pro SMS 2003 i pro SCCM 2007.<br /> Bližší info je možné získat na webu Microsoftu http://technet.microsoft.com/cs-cz/library/cc180191(en-us).aspx !pozor! na několika místech v tomto článku, jsou výše uvedené linky napsané špatně!!!
  </p>
  
  <p>
    SMS Health Monitoring Tool
  </p>
  
  <p>
    Výborný nástroj pro monitoring zdraví klientů distribučního systému Microsoft Systems Management Server 2003:
  </p>
  
  <p>
    http://technet.microsoft.com/en-us/sms/bb676776.aspx &#8211; v SCCM 2007 je již částečně intergrována jakožto role Fallback Status Point.
  </p>
</div>

