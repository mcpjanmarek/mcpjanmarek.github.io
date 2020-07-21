---
id: 34
title: Microsoft SQL Server 2005 – High Availability
date: 2010-01-01T09:36:00+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/01/01/microsoft-sql-server-2005-%e2%80%93-high-availability'
permalink: /2010/01/01/microsoft-sql-server-2005-high-availability/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!323')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!323')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SQL Server
---
<div id="msgcns!6E7B9216726D07B8!323" class="bvMsg">
  <p>
    <u><a href="http://janmarek.eu/wp-content/uploads/2010/10/sqlserver20055b45d1541290c.png" rel="WLPP"><img style="border-bottom:0;border-left:0;display:inline;border-top:0;border-right:0;margin:0 15px 0 0;" title="sqlserver2005" border="0" alt="sqlserver2005" align="left" src="/wp-content/uploads/2010/10/sqlserver20055b45d1541290c.png?w=290" width="240" height="66" /></a> Server Failover Clustering</u>
  </p>
  
  <p>
    &#8211; Microsoft Cluster Service (vyzaduje domenu)
  </p>
  
  <p>
    &#8211; daji se udelat i ve 2 domenach (ale musi byt v jednom forestu, nebo musi mit obousmerny trust) &#8211; best practice je mit je v jedne domene (nejlepe aby je overoval jeden DC)
  </p>
  
  <p>
    &#8211; je pouze na OS Enterprise a na SQL Standard a Enterprise (v 1 licenci 2 cluster nody)
  </p>
  
  <p>
    &#8211; na W2K3 max. 8 cluster nods
  </p>
  
  <p>
    &#8211; podminky: supported hw, identicke nody v clusteru (vse!!! ~ hw i sw), sdilene disky (se SCSI identifikaci, = fibre channel (limitovan delkou ~ max. 10/100km), = iSCSI (sitove SCSI))
  </p>
  
  <p>
    &#8211; postup: nainstaluji cluster service na jeden nod, pote na druhy, pak vytvorim pouze 1 cluster resource grooup (s netbios name, IP adress, min. 1 shared HDD)
  </p>
  
  <p>
    &#8211; pri presunu clusteru se presouvaji i sys db
  </p>
  
  <p>
    &#8211; protoze ale startuji i sluzby SQL a dela se restore, tak presun cluster nodu trva dlouho (dle MS do 2 s, ve skutecnosti i 2-3min.)
  </p>
  
  <p>
    nebo
  </p>
  
  <p>
    <u></u>
  </p>
  
  <p>
    <u>Database Mirroring</u>
  </p>
  
  <p>
    &#8211; kazdy cluster nod ma svuj HDD
  </p>
  
  <p>
    &#8211; pouze mezi 2 sql servery (principal &#8211; mirror)
  </p>
  
  <p>
    &#8211; pri presunu clusteru se nepresouvaji sys db a userdb, ktere nemaji full recovery model
  </p>
  
  <p>
    &#8211; presun clusteru je prakticky okamzity
  </p>
  
  <p>
    &#8211; az od SQL SP1
  </p>
  
  <p>
    &#8211; identicke verze SQL vyzaduje (pouze witness muze mit jinou)
  </p>
  
  <p>
    &#8211; vznikla puvodne z log shippingu (backup-restore t-logu zpusob pomoci jobu)
  </p>
  
  <p>
    &#8211; pouziva tzv. listener a pomoci neho si vymenuji db data (rozdil oproti replikaci je to, ze ten druhy server neni aktivni (=> neplatim dalsi licenci), neco jako active/passive)
  </p>
  
  <p>
    &#8211; ten neaktivni sql server se nazyva "Hot Standby"
  </p>
  
  <p>
    &#8211; 3rezimy:
  </p>
  
  <p>
    &#8211; high availability (vyuziva 3. server, tzv. Witness (svedek), ktery kontroluje stav mirroringu a pripadne zbudi standby server)
  </p>
  
  <p>
    => automaticky failover
  </p>
  
  <p>
    &#8211; high protection
  </p>
  
  <p>
    &#8211; high performance
  </p>
  
  <p>
    &#8211; nastavuji cele pres SSMS pres wizard (pres TSQL: CREATE ENDPOINT) &#8211; na kazdem serveru to musim udelat
  </p>
  
  <p>
    &#8211; vyzadovan FQDN (name+suffix)
  </p>
  
  <p>
    &#8211; pokud nemam witness server, tak mohu udelat presun manualne pomoci ALTER DATABASE (pokud nemam aktualni data, neprobehl presun dat posledni, tak se da spustit i FORCE)
  </p>
  
  <p>
    &#8211; vyhodou je to, ze pokud aplikace pouziva SQLAgenta nebo .NET2.0 (a vyssi), tak se aplikace automaticky prepoji na funkcni SQL serverv mirroru
  </p>
  
  <p>
    &#8211; pri nastavovani musim byt dbo a sysadmin
  </p>
  
  <p>
    -1. udelam backup db z principal
  </p>
  
  <p>
    -2. udelam restore db na mirroru s option NORECOVERY (non-operational)
  </p>
  
  <p>
    -3. na principal dam Database &#8211; properties &#8211; mirroring &#8211; configure security &#8211; nakonci dat DO NOT START
  </p>
  
  <p>
    -4. po dokonceni wizardu si dat pozor na to co se doplnilo do principal, mirror, witness &#8211; musi tam byt FQDN !!!
  </p>
  
  <p>
    -5. Start mirroring
  </p>
  
  <p>
    &#8211; behem mirroringu se tsql provadi i nad mirrorovanou db (ta se zmeni do stavu Synchronizing), v tuto chvili si neda do principal db zapisovat; to se da az mirror db nahlasi ze Synchronized (rezim Full Safety) &#8211; presne info na <a href="http://download.microsoft.com/download/4/7/a/47a548b9-249e-484c-abd7-29f31282b04d/DBM_Best_Pract.doc">http://download.microsoft.com/download/4/7/a/47a548b9-249e-484c-abd7-29f31282b04d/DBM_Best_Pract.doc</a> , ktere uvadi best practice
  </p>
  
  <p>
    &#8211; tzn. zjistit jako mam sirku pasma, zajistit si ji pote pomoci QOS a pote zajistit nizkou latency
  </p>
  
  <p>
    &#8211; po zruseni mirroringu se nesmazou endpointy (musi se odstranit rucne DROP ENDPOINT nebo pres SSMS delete endpoint)
  </p></p>
</div>

