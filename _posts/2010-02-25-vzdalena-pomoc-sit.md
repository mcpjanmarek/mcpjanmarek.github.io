---
id: 1185
title: 'Vzdálená pomoc &#8211; síť'
date: 2010-02-25T10:32:34+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/02/25/remote-assistance-networking
permalink: /2010/02/25/vzdalena-pomoc-sit/
categories:
  - Nezařazené
  - Uncategorized
---
<div id="msgcns!6E7B9216726D07B8!255" class="bvMsg">
  <div>
    Pokud máte bránu firewall mezi klientem a počítačem (s instalovanou konzolou configmgr) může očekávat nějaké problémy s připojení programu Vzdálená pomoc.
  </div>
  
  <div>
  </div>
  
  <div>
    Komunikace mezi nimi začíná na portu RPC. Říkají, že každé jiné číslo portu na kterém začnou relaci vzdálené pomoci. Tento port je dynamicky vybrán z řady do 1024. Tak je třeba otevřít číslo portu RPC 135 a pak všechny porty až 1024. To může zvýšit riziko v infrastruktuře, takže další možnost je omezit rozsah dynamických portů RPC na klienty změnou klíče registru HKEY LMsoftwaremicrosoftrpcinternetports. Potom můžete omezit odchozí komunikaci z počítače, konzole na klientovi pouze tyto porty. Ale jiným způsobem (od klienta k serveru), je třeba ponechat otevřené pro všechny porty. Pokud změníte na druhou stranu může kromě problémů s dalšími službami (pro ex. AD).
  </div>
</div>

