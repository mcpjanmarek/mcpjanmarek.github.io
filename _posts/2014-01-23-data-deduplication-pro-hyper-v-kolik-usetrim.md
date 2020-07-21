---
id: 724
title: 'Data Deduplication pro Hyper-V: Kolik ušetřím?'
date: 2014-01-23T19:41:03+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=724
permalink: /2014/01/23/data-deduplication-pro-hyper-v-kolik-usetrim/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2012
  - Windows Server 2012 R2
---
Windows Server 2012 přišel s funkcí Data Deduplication. Ve výchozím stavu není nainstalovaná, ale to je jen otázka minuty, navíc bez restartu.

[<img class="aligncenter  wp-image-726" alt="datadeduplication-roleservice" src="/wp-content/uploads/2014/01/datadeduplication-roleservice.png" width="645" height="264" />](/wp-content/uploads/2014/01/datadeduplication-roleservice.png)

Data Deduplication funguje stylem post-processing a proto, pokud ji necháte ve výchozím stavu deduplikovat soubory v IDLE stavu serveru, nesnižujete výkon při zápisu. Vzhledem k úspoře místa pomocí deduplikace &#8222;kousků&#8220; souborů (z angl. chunks) a tím pádem menšímu množství fyzicky procházených disků/míst na disku (v případě klasických HDD) se dokonce zvyšuje výkon při čtení!

Proč to nevyužít také pro virtuální disky u virtuálek na Hyper-V? Na Windows Server 2012 lehce unsupported záležitost, ale na 2012 R2 už naprosto podporováno. Bohužel v tuto chvíli jen pro virtuální stroje s klientským OS určené pro VDI (Virtual Desktop Infrastructure). Z praxe mohu potvrdit, že to ale funguje i pro klasické virtuálky.

Data Deduplication je podporována na lokálních (ne OS) discích, cluster discích a dokonce i na CSV (Cluster Shared Volumes).

Postupovat ale principem &#8222;instalace-test-případná_odinstalace&#8220; se nevyplatí, protože než server zdeduplikuje třeba vašich 5TB virtuálek, bude to nějakou dobu trvat a ve finále zjistíte, že to není úplně výhodné (deduplikace &#8222;sežere&#8220; samozřejmě taky nějakou RAMku a CPU čas).

Jak teda zjistit, kolik místa s deduplikací ušetřím, aniž bych ji musel instalovat a čekat? Stačí použít built-in příkazový nástroj DDPeval.

Použití je jednoduché:

> DDPeval D:\WBI-VMs
> 
> DDPeval D:\

Výsledkem je pak například takovýto report (jedná se o deduplikaci generovaných bin souborů, proto taková úspora :)) :

[<img class="aligncenter size-full wp-image-725" alt="ddpeval" src="/wp-content/uploads/2014/01/ddpeval.png" width="583" height="471" />](/wp-content/uploads/2014/01/ddpeval.png)

Jedna důležitá připomínka &#8211; použil jsem v příkladu ddpeval na konkrétním adresáři, ale Data Deduplication se zapíná na celé jednotce. Nejde tedy deduplikovat jen jeden adresář. Nástroj pouze dokáže reportovat, kolik toho ušetříte právě v tom jednom adresáři.

Zpráva davům: Nastavit Data Deduplication (tak, aby to jednak fungovalo a jednak bylo efektivní a ohleduplné k virtuálkám) není tak snadné jako to kliknout na disku obyčejného file serveru. A v případě Hyper-V Clusteru a CSV už je to úplně jiné kafe. O tom v nějakém z dalších článků 🙂 Abych Vás od toho ale úplně neodradil, tak tady je screenshot z jednoho z našich produkčních Hyper-V clusterů, kde je CSV jednotka s cca 200 virtuálkami a šetříme díky Data Deduplication takovýto prostor:

[<img class="aligncenter size-full wp-image-727" alt="datadeduplication-csv" src="/wp-content/uploads/2014/01/datadeduplication-csv.png" width="822" height="127" />](/wp-content/uploads/2014/01/datadeduplication-csv.png)

PS. Jestli chcete vědět více, tak přijďte na můj seminář na téma Data Management & Security. Více info <a href="http://learning.wbi.cz/kurzy/124-30-windows-server-2012-r2-data-management-security.aspx" target="_blank">zde</a>.
