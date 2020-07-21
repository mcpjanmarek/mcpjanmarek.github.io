---
id: 563
title: Automatické propsání snapshotu při smazání VM na Hyper-V 2012
date: 2013-03-15T18:27:21+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=563
permalink: /2013/03/15/automaticke-propsani-snapshotu-pri-smazani-vm-na-hyper-v-2012/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2012
---
Právě jsem zjistil velice, ale velice, zvláštní chování VM při jejím smazání.

Při smazání VM přes Hyper-V Manager dojde pouze k odstranění konfiguračních souborů VM a případně souborů reprezentujících cache virtuální RAM. VHD, resp. VHDX soubory se nesmažou. To není to překvapující samozřejmě.

Ale! Pokud smažete VM, která měla jeden či více snapshotů a obsahovala tedy několik diferenčních VHD(X) souborů, pak se okamžitě spustí jejich merge. A co mi na tom vadí? Jednak nepotřebuji, aby se merge prováděl, když už mě VM nezajímá (proto ji mažu), ale hlavně nemůžu tyto VHD(X) soubory smazat, protože jsou zamknuté službou Hyper-V, protože probíhá právě zmiňovaný merge. Musím tedy čekat až se merge dokončí. Jeho průběh můžete sledovat narůstajícím parent diskem VM.

Podle mě dost nešťastně nastavený proces&#8230;

