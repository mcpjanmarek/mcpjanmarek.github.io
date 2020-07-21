---
id: 377
title: Migrace objektů mezi doménami pomocí LDIFDE
date: 2012-02-21T15:49:16+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/?p=377
permalink: /2012/02/21/migrace-objektu-mezi-domenami-pomoci-ldifde/
jabber_published:
  - "1329835759"
  - "1329835759"
publicize_results:
  - 'a:1:{s:7:"twitter";a:1:{i:76316228;a:2:{s:7:"user_id";s:11:"mcpjanmarek";s:7:"post_id";s:18:"171969765210984448";}}}'
  - 'a:1:{s:7:"twitter";a:1:{i:76316228;a:2:{s:7:"user_id";s:11:"mcpjanmarek";s:7:"post_id";s:18:"171969765210984448";}}}'
categories:
  - Active Directory
  - Nezařazené
tags:
  - base64
  - ldf
  - technet microsoft
---
Pokud byste rádi přenesli objekty (user, group,..) mezi doménami exportem/importem pomocí nástroje LDIFDE, tak se vám může stát, že DN objektů budou obsahovat tzv. offensive znaky. V tomto případě nebudou tyto atributy ve výsledném LDF souboru v plaintextu, ale zakódované jako base64. Není tedy pak úplně jednoduché připravit takový soubor pro import, protože už vám nestačí jen notepad a funkce Najít-Nahradit&#8230;

Vytvořil jsem tedy powershell skript, který projde takovýto soubor, najde všechny base64 encoded DN atributy, rozkóduje je, změní název domény, zakóduje a zapíše zpět do souboru. Ten pak může použít pro import.

Skript jsem publikoval na Technet Gallery a je k dispozici zde: <http://gallery.technet.microsoft.com/scriptcenter/Powershell-script-to-33887eb2>
