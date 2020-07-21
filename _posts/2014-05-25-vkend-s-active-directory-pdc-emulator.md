---
id: 802
title: 'víkend s: Active directory: PDC emulator'
date: 2014-05-25T13:17:00+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=802
permalink: /2014/05/25/vkend-s-active-directory-pdc-emulator/
categories:
  - Active Directory
  - Nezařazené
tags:
  - Active Directory
  - AD
  - ADDS
  - PDC
---
Active Directory od verze 2000 podporuje multi-master replikační model. Tzn., že ve finále jsou si téměř všechny DC rovny a poskytují všechny služby, ale… některé funkce jsou raději poskytovány pouze konkrétním řadičem v doméně či ve forestu. Tyto funkce alias role se nazývají FSMO (Flexible Single Master Operations) a řadiče, které hostují takové role se nazývají Operations Masters.

Existuje pět různých FSMO rolí. Dvě z nich procesují služby na úrovni forestu a zbylé tři na úrovni domény.

Forestové FSMO role jsou

  * Schema Master
  * Domain Naming Master

Doménové FSMO role jsou

  * Infrastructure Master
  * RID Master
  * PDC Emulator

Pojďme se nyní podívat na PDC emulator (PDCe). V první řadě PDCe poskytuje “legacy” specifické funkce pro Primary Domain Controller z důvodů zpětné kompatibility- Můžete se ně blíže mrknout třeba <a href="http://msdn.microsoft.com/en-us/library/cc237121.aspx" target="_blank">tady</a>. Kromě těchto samozřejmě poskytuje i další. Když si změníte heslo na konkrétním DC, je tahle změna preferovaně replikována na DC, které hostuje PDCe FSMO roli. Takže když vaše přihlašování selže kvůli špatnému heslu, DC přesměruje váš autentizační požadavek na PDCe, kde se zvaliduje vaše nejaktuálnější heslo. Když DC s PDCe zjistí, že opravdu zadáváte špatně heslo, původní DC vás informuje zprávou o použití nesprávného hesla.

Jestilže používáte funkci zamykání účtů (Account Lockout) ke zvýšení bezpečnosti, PDCe je místo, kde jsou počítány neúspěšné pokusy při zadání špatného hesla. Kdyby tomu tak nebylo, tzn. každé DC by počet pokusů udržovalo samostatně a až následně replikovalo, tak by měl útočník více pokusů k brute-force útoku.

