---
id: 1902
title: 'ROBOCOPY: Kopírování souborů včetně ACL'
date: 2018-10-03T20:00:10+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1902
permalink: /2018/10/03/robocopy-kopirovani-souboru-vcetne-acl/
categories:
  - Nezařazené
tags:
  - Robocopy
  - Tools
  - Windows
---

Poměrně často to na kurzech řeším a proto zde publikuji pro referenci.

{% highlight console %}
robocopy "D:\zdroj" "E:\cíl" /R:1 /w:0 /e /purge /zb /xo /copy:DATSO /v /log+:$LogFile /tee
{% endhighlight %}

/R – počet opakování, pokud se soubor nepovede zkopírovat

/W – prodleva v sekundách mezi pokusy o opakované kopírování

/e – kopíruje včetně podadresářů, i prázdných

/xo - nepřenáší starší soubory v případě konfliktu (dobré, pokud se kopírují několikrát stejná data)

/copy: &#8211; definuje co všechno se se soubory přenáší

  * D – vlastní soubor
  * A – atributy
  * T – časová značka
  * S – NTFS práva
  * O – informace o vlastníkovi

/v – verbose výstup včetně všech vynechaných a přeskočených souborů

/log+ - výstup je zaznamenán do logu, který se při opakovaném spuštění nepřepisuje, ale doplňuje

/tee – výstup je vypisován současně na konzoli i do logu
