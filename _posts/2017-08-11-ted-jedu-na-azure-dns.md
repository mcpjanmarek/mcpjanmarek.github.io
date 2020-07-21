---
id: 1743
title: Teď jedu na Azure DNS
date: 2017-08-11T21:19:12+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1743
permalink: /2017/08/11/ted-jedu-na-azure-dns/
categories:
  - Microsoft Cloud
  - Nezařazené
tags:
  - Azure
---
Včera jsem se pustil do přesunu hostovaného veřejného DNSka do Microsoft Azure. Kolega <a href="http://www.defense-ops.com" target="_blank" rel="noopener">Dan</a> mě na to upozornil, tak proč to nezkusit. Byl jsem naprosto mile překvapen, jak jednoduché to celé bylo.

V Azure portálu jsem si přidal z marketplacu DNS ZONE. Při vytváření stačí zadat DNS zone jméno a hotovka.

Pak už jen přidáváte jednotlivé DNS záznamy, které se jako objekty v Azure portálu jmenují Record Sety. Všechno je super přehledné a bezva rychlé.

Na konec jsem už jen rekonfiguroval směrování na správné NS u mého poskytovatele domény a netrvalo to ani těch klasických 24h a už jsem jel z Azure.

<img class=" size-full wp-image-1752 alignleft" src="/wp-content/uploads/2017/08/Azure-DNS-JanMarekEU.png" alt="Azure-DNS-JanMarekEU" width="859" height="673" srcset="/wp-content/uploads/2017/08/Azure-DNS-JanMarekEU.png 859w, /wp-content/uploads/2017/08/Azure-DNS-JanMarekEU-300x235.png 300w, /wp-content/uploads/2017/08/Azure-DNS-JanMarekEU-768x602.png 768w" sizes="(max-width: 859px) 100vw, 859px" />
