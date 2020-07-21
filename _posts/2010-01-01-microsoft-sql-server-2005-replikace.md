---
id: 33
title: 'Microsoft SQL Server 2005 &#8211; replikace'
date: 2010-01-01T09:38:00+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/01/01/microsoft-sql-server-2005-replikace
permalink: /2010/01/01/microsoft-sql-server-2005-replikace/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!326')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!326')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SQL Server
---
<div id="msgcns!6E7B9216726D07B8!326" class="bvMsg">
  <p>
    <a href="/wp-content/uploads/2010/10/sqlserver20055b45d7a276e27.png" rel="WLPP"><img style="border-bottom:0;border-left:0;display:inline;border-top:0;border-right:0;margin:0 15px 0 0;" title="sqlserver2005" border="0" alt="sqlserver2005" align="left" src="/wp-content/uploads/2010/10/sqlserver20055b45d7a276e27.png?w=290" width="240" height="66" /></a> &#8211; existuje i peer-to-peer (pres RPC zapouzdrene do HTTPS)
  </p>
  
  <p>
    &#8211; synchronizace db (synchronizovane db jsou vsechny online)
  </p>
  
  <p>
    &#8211; da se nastavit, ze nektere budou jen na read a nektere jen na write
  </p>
  
  <p>
    &#8211; lepsi je vyuzit replikaci na urovni filesystemu, ale to SQL neumi (melo by to byt na SQL 2008)
  </p>
  
  <p>
    &#8211; zajistuje autonomii serveru sql, prilblizuje data uzivatelum, redukuje locks na db
  </p>
  
  <p>
    &#8211; role replikacnich serveru
  </p>
  
  <p>
    &#8211; publisher &#8211; jeho db se zucastnuje replikace (~ sdili db)
  </p>
  
  <p>
    &#8211; distributor &#8211; kopiruje sdilene db na subsriber, muze byt interni (je na stejnem srv jako publisher) nebo externi (na samostatnem serveru)
  </p>
  
  <p>
    &#8211; subscriber &#8211; cil pro db
  </p>
  
  <p>
    &#8211; muze byt obousmerne tzn. publisher je i subscriber a opacne
  </p>
  
  <p>
    &#8211; typy replikace
  </p>
  
  <p>
    &#8211; snapshot &#8211; pri zmene jedne radky v tabulce se replikuje cela tabulka (dobre je to na to, ze se da prenest cela db)
  </p>
  
  <p>
    &#8211; snapshot agent &#8211; bezi na publisher srvru
  </p>
  
  <p>
    &#8211; tranactional&#8211; replikuji se i male zmeny (i jen radky), vyuziva t-log
  </p>
  
  <p>
    &#8211; log reader agent
  </p>
  
  <p>
    &#8211; merge &#8211; oboustranna
  </p>
  
  <p>
    &#8211; problem je ze pokud vznikne na obou srv stejne radky, tak dojde ke konfliktu (kvuli tomu vznika dat. typ GUID / pokud to ale nechci tak vyrobim sloupec ID serveru &#8211; aplikace pak musi resit rozeznani serveru, nebo to udelam na sql serveru pomoci triggeru)
  </p>
  
  <p>
    &#8211; merge agent
  </p>
  
  <p>
    &#8211; heterogeneous &#8211; replikace mezi sql serverem a jinym typem db serveru
  </p>
  
  <p>
    &#8211; articles &#8211; prenasene data &#8211; co publikovat (tabulky, sloupce,&#8230;)
  </p>
  
  <p>
    &#8211; publications &#8211; skupiny articles
  </p>
  
  <p>
    &#8211; distributor
  </p>
  
  <p>
    &#8211; subscriptions &#8211; odkud kam se ma udelat synchronizace
  </p>
  
  <p>
    &#8211; replikacni agenti jsou soucasti sluzby sql serveru a pouzivaji joby
  </p>
  
  <p>
    &#8211; mohu nastavit i replikaci pro napr. PDA pomoci compact edition sql
  </p>
  
  <p>
    &#8211; konfiguruje se pres SSMS server
  </p>
  
  <p>
    &#8211; replications &#8211; configure distribution&#8230; (timto se vytvori sys db distribution (sp_adddistributiondb))
  </p>
  
  <p>
    &#8211; slozku pro snapshot (vytovri se pres bulkcopy) dat na specialni disk, protoze pri jeho vzniku nastane mnoho I/O operaci
  </p>
  
  <p>
    &#8211; local publications &#8211; new publications&#8230;
  </p>
  
  <p>
    &#8211; mohu pouzit filter (~ SELECT s WHERE) &#8211; vyberu jen napr. urcite radky ze sloupce
  </p>
  
  <p>
    &#8211; snapshot &#8211; je tam proto, abych mohl prenest ty puvodni data, ale mohu nastavit i schedule
  </p>
  
  <p>
    &#8211; nastavuji ucty pro agenty &#8211; musi mit prava read k replikovanym datum / mohu to nastavit i na ucet SQL Agenta (jako bylo nativne v SQL 2000)
  </p>
  
  <p>
    &#8211; local subscriptions &#8211; new subscription &#8230;
  </p>
  
  <p>
    &#8211; nastvauji push (vyssi zatizeni distributora) nebo pull (~kontinualni replikace => vyskoa latence)
  </p>
  
  <p>
    &#8211; nadefinuji opet ucty
  </p>
  
  <p>
    &#8211; typ synchronizace
  </p>
  
  <p>
    &#8211; kontinualni
  </p>
  
  <p>
    &#8211; manualni
  </p>
  
  <p>
    &#8211; nemohu udelat subscriber na publikaci, ktera uz je prenasena
  </p>
</div>
