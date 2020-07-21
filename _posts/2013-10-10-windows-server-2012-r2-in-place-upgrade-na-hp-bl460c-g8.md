---
id: 576
title: Windows Server 2012 R2 In-Place Upgrade na HP BL460c G8
date: 2013-10-10T12:06:26+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=576
permalink: /2013/10/10/windows-server-2012-r2-in-place-upgrade-na-hp-bl460c-g8/
categories:
  - HP
  - Nezařazené
  - Windows Server 2012 R2
---
Vzhledem k blížící se naší konferenci na 2012 R2 produkty (více info <a href="http://learning.wbi.cz/kurzy/112-30-it-pro-academy-the-2012-r2-era-begins-now.aspx" target="_blank">zde</a>) jsem se pustil do budování labů. Aktuálně všechny naše servery běží na Windows Server 2012 a bylo tedy nutné alespoň jeden povýšit na Windows Server 2012 R2. Nejsem sice příliš zastánce in-place upgradů, ale vzhledem k času jsem se uchýlil k nejrychlejší variantě. Chvíli jsem sice bojoval s licenčním číslem, ale nakonec se upgrade rozeběhl. Na zmiňovaném serveru byla nainstalována role Hyper-V a dokonce i feature Failover Clustering. Blade je připojen k FC SAN a proto má na sobě i MPIO. Měl jsem ale trochu obavu spíše z ovladačů. Po spuštění upgradu se server asi 15x restartoval, což mě lehce znervózňovalo.

Každopádně nakonec se celý proces dokončil. Server zůstal v doméně, reaguje po přihlášení úplně bleskově a nevypadá to, že by chyběl nějaký ovladač.

Pokud tedy přemýšlíte, jestli vám na tomto hardwaru bude fungovat in-place upgrade, pak mohu potvrdit, že ano&#8230;