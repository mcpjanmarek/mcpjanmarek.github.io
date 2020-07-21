---
id: 39
title: Microsoft SQL Server 2005 – správa souborů a databází
date: 2010-01-01T09:21:00+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/01/01/microsoft-sql-server-2005-%e2%80%93-sprava-souboru-a-databazi'
permalink: /2010/01/01/microsoft-sql-server-2005-sprava-souboru-a-databazi/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!308')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!308')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - SQL Server
---
<div id="msgcns!6E7B9216726D07B8!308" class="bvMsg">
  <p>
    <a href="http://janmarek.eu/wp-content/uploads/2010/10/sqlserver20055b45d1ddbc9b9.png" rel="WLPP"><img style="display:inline;border-width:0;margin:0 10px 0 0;" title="sqlserver2005" border="0" alt="sqlserver2005" align="left" src="/wp-content/uploads/2010/10/sqlserver20055b45d1ddbc9b9.png?w=290" width="240" height="66" /></a> -IIS uzira SQL RAM, protoze SQL sio kontroluje volnou RAM a kdyz ji je malo tak si snizi pamet, ovsem tu uvolnenou si IIS ukradne a tak je to zacyklene, az je buffer SQL na minimu a pak jde vykon dolu, po restartu serveru se SQL vizualne zrychli, ale to je tim, ze IIS uvolnilo pamet&#8230; zacne ovsem znovu proces kradeni RAM
  </p>
  
  <p>
    &#8211; BUFFER je jen jeden v MS SQL
  </p>
  
  <p>
    &#8211; LDF davat na nejrychlejsi disky na ZAPIS (nejlepsi by bylo RAID01, kompromisem je RAID1 nebo RAID5)<br />&#8211; MDF/NDF davat na nejrychlejsi disky na CTENI<br />&#8211; na SAN je to resene aplikaci nad SANkou, takze dnes se prakticky ani nevi v jakem modu ktery disk jede (system nastavuje co nejvyssi rychlost a zaroven co nejvyssi redundanci)<br />&#8211; podivat se na performance citace PHYSICALDISK-AVERAGE DISK SEC/TRANSFER a PHYSICALDISK-AVERAGE DISK QUEUE LENGHT (max. 2) a SQL SERVER BUFFER CACHE-BUFFERCACHEHITRATIO(max. 90%)-pokud je vic, tak je malo RAM<br />&#8211; pokud nebudu zalohovat db, tak ldf poroste az zaplni disk<br />&#8211; kolik zabira co mista v db, tak ji v SSMS vyberu a kliknu na Report (vola metadata ze schemy SYS)<br />&#8211; filegroups &#8211; seskupuji nekolik mdf/ndf &#8211; pouziva se ke zvyseni performace a napr. pro archivaci, protoze filegroup mohu nastavit read-only <br />&#8211; schema &#8211; pomaha pouze prekladat relativni jmena k tabulka<br />&#8211; indexy &#8211; pokud je fragmentace nad 30%, tak rebuildovat<br />&#8211; transaction log file &#8211; limitovat velikost na 50% celkove velikosti db<br />&#8211; jako admin mohu vse spravovat pres SSMS, nebo pres prikazy (views, sp, metadata/dynamicmetadata pohledy) tim, ze jako admin mam prava SELECT * SYS, ve ktere jsou prave tyto objekty ulozene</div>

