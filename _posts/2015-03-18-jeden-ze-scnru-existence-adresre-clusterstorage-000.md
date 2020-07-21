---
id: 911
title: jeden ze scénářů existence adresáře clusterstorage.000
date: 2015-03-18T19:39:00+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=911
permalink: /2015/03/18/jeden-ze-scnru-existence-adresre-clusterstorage-000/
categories:
  - Failover Cluster
  - Hyper-V
  - Nezařazené
tags:
  - csv
  - Failover Cluster
  - Hyper-V
  - MPIO
  - WFC
---
Dnes jsem řešil takový zajímavý problém, který hezky demonstruje to, jak je důležité nehrát si s produkčním prostředím. 

Prostředí je velice jednoduché: dva Hyper-V servery v clusteru s iSCSI storagem. Konfigurace OS, sítí, Hyper-V atd. naprosto v pořádku a cluster prošel při formování bez ztráty kytičky. Za to musím zákazníka pochválit a ocenit ho dle Červeného trpaslíka hodnocením pět a půl pračky whirlpool.

Bohužel problém nastal ve chvíli, kdy si jeden z kolegů chtěl pohrát s clusterem a připojit si k němu další iSCSI pole. Protože mu to ale pořádně nešlo, tak si začal lehce hrát s kdečím. Finálem byla nemožnost zapnutí několika produkčních VMs z konkrétního CSV disku. Po bližším prozkoumání jsem našel na jednom z nodů adresář ClusterStorage.000, který seděl hned vedle správného ClusterStorage, a obsahoval data nespustitelných VM. Tento adresář (.000) vzniká typicky v případech, kdy cluster node nedokáže úplně jasně určit cestu, kterou se má připojit k datům.

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="/wp-content/uploads/2015/03/image_thumb.png" width="531" height="114" />](/wp-content/uploads/2015/03/image.png)

&nbsp;

Jak postupovat? Nejjednodušší způsob (než se začnete vrtat v clusterlogu) je spustit starý dobrý Cluster Validation test na tomto “vadném” CSVčku. V mém případě bylo výstupem následující.

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="/wp-content/uploads/2015/03/image_thumb1.png" width="1851" height="51" />](/wp-content/uploads/2015/03/image1.png)

A když jsem se pak mrknul na seriáky a signatury, tak byla opravdu vidět duplicita,

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="/wp-content/uploads/2015/03/image_thumb2.png" width="1028" height="412" />](/wp-content/uploads/2015/03/image2.png)

což jasně s pomocí tohoto screenshotu ukazuje na špatně nastavené (čtěte nenastavené) MPIO.

Jasně, není to nic moc převratného, ale myslím si, že je zajímavé vidět, jak na takto simple věc reaguje WFC.

