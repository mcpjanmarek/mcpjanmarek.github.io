---
id: 816
title: hyper-v ve vm běžící na hyper-v
date: 2015-01-01T20:44:20+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=816
permalink: /2015/01/01/hyper-v-ve-vm-bezc-na-hyper-v/
categories:
  - Hyper-V
  - Nezařazené
tags:
  - Hyper-V
---
Dobře, dobře, dobře – poněkud pochybný název postu, ale výstižněji se mi to už napsat nepovedlo 🙂

Každopádně nebudu zde psát nic moc nového. Stav jaký je teď už trvá nějakou tu dobu. Bohužel se mi poslední dobou nakupilo mnoho otázek ohledně tohoto tématu.

Jde tedy provozovat Hyper-V ve virtuálním stroji, který běží na Hyper-V? Jednoduchá odpověď je NE. Oficiálně i plnohodnotně technicky NE. Celá situace se v angličtině popisuje jako “Nested Virtualization”

<!--more Přečtěte si více!-->

Uvnitř virtuálky lze Hyper-V roli sice nainstalovat (ale ne přes GUI, protože to si “hlídá” určité prerequisity) a dokonce jde i VM na vnořeném Hyper-V vytvořit, ale už ji nezapnete. Zároveň bývají také velké problémy se síťováním atd. atd. K čemu to tedy je dobré ve finále? Můžete si “osahat” Hyper-V Manager, podívat se na různá nastavení, vyrobit klidně i Hyper-V cluster, i replikovat VM pomocí Hyper-V Replica služby. To je ale vše a navíc s mnoha omezeními. Například, jak si chcete pořádně ozkoušet Live Migration, když tu provedete pouze s běžící VM, kterou ovšem na vnořeném Hyper-V nezapnete? To je jen jeden z mála příkladů.

Hyper-V bohužel dnes nepodporuje pokročilé maskování fyzických zařízení a proto takové nedostatky. I pro mne je to velké omezení, protože v opačném případě by mi pro odškolení Hyper-V kurzu stačil jeden fyzický stroj, na kterém bych **vše** zvirtualizoval. Jediná možnost je tedy skočit ke konkurenci a použít třeba víemvér vorkstejšnu.

V některém z dalších článků sepíšu, jak nested Hyper-V rozjet, abyste si mohli taky neoficiálně nepodporovaně zkoušet.

Mimochodem – už nás tuhle věc Microsoftu mnoho reportuje, tak snad se třeba jednou dočkáme, aby to šlo 🙂

