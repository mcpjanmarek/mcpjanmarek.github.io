---
id: 140
title: Chyba v zapisu na HP EVA 4400 pres QLogic karty
date: 2011-01-06T14:29:24+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=140
permalink: /2011/01/06/chyba-v-zapisu-na-hp-eva-4400-pres-qlogic-karty/
jabber_published:
  - "1294320564"
  - "1294320564"
tagazine-media:
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:8:"17238236";s:7:"blog_id";s:8:"16623371";s:9:"mod_stamp";s:19:"2011-01-06 13:30:21";}'
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:8:"17238236";s:7:"blog_id";s:8:"16623371";s:9:"mod_stamp";s:19:"2011-01-06 13:30:21";}'
categories:
  - HP
  - Nezařazené
---
Poslednich par dni jsem registroval pomalejsi zapis souboru na FC pole HP EVA 4400 z HP ziletek BL460c G6, ktere jsou osazeny Qlogic kartou QMH2562 8Gb. Vzal jsem tedy jeden vetsi VHD soubor (mel asi 8GB) a zkusil ho rucne nakopirovat na disk presentovany z pole. Nasledovalo rychle zapsani celeho souboru do pameti Windows (na ziletkach bezi Windows Server 2008 R2 samozrejme 🙂 ) a na pozadi probihal zapis souboru na pole. Pres resource manager jsem ovsem zjistil ze zapis probiha rychlost 4060ms!!! Coz je opravdu obrovske cislo! Spolu s kolegou z dodavatelske firmy jsme po kontrole celeho nastaveni EVA, HBA karet a vseho mozneho zjistili, ze je na webu HP k dispozici novejsi driver pro QLogic kartu. Ja mel na ziletkach verzi 9.1.8.17. Z webu jsme stahli tedy verzi 9.1.8.28 (z 30.srpna 2010) a po jeji aplikaci problem vyresen! Opetovny pokus se zapsanim souboru na disk z pole probehl rychlost 62ms.

Cim to je, ze HP Smart Start CD for EVA, ktere mam z 1.11.2010 neobsahuje uz tento novejsi driver?! 🙂 HP nas zkousi, jak jsme asi pozorni 😉