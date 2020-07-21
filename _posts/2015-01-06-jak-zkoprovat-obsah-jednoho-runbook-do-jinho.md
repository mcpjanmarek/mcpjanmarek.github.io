---
id: 866
title: jak zkopírovat obsah jednoho runbook do jiného
date: 2015-01-06T22:43:42+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=866
permalink: /2015/01/06/jak-zkoprovat-obsah-jednoho-runbook-do-jinho/
categories:
  - Nezařazené
  - SC Orchestrator
tags:
  - SCOR
---
Vlastně jde o banální věc, ale existují tři způsoby, jak to udělat.

  1. Udělat export celého runbooku a pak provést jeho import. Tím získáme kopii. To funguje perfektně vždy.
  2. Označit myší aktivity uvnitř runbooku a přes klasický copy/paste přenést do druhého runbooku.
  3. Použít Select/Copy/Paste z menu Runbook Designer konzole.

Možnost 2 a 3 má dost rozdílný vliv na výsledek 🙂

Nejdřív tedy bod 2 aneb klasika copy/paste.

[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb.png" width="829" height="488" />](http://janmarek.eu/wp-content/uploads/2015/01/image.png) 

A jak vypadá výsledek po vložení do nového runbooku?

[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb1.png" width="574" height="269" />](http://janmarek.eu/wp-content/uploads/2015/01/image1.png) 

No tak to je dost peklo 🙁

Jak to tedy zkopírovat tak, aby byl ponechán layout? Použít volby z menu. Tady je postup:

1. Označit zdrojový runbook. Celý runbook a ne klikat do jeho obsahu!

&nbsp;[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb2.png" width="324" height="126" />](http://janmarek.eu/wp-content/uploads/2015/01/image2.png) 

2. V menu zvolit Edit – Select All

[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb3.png" width="351" height="170" />](http://janmarek.eu/wp-content/uploads/2015/01/image3.png) 

3. V menu zvolit Edit – Copy

[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb4.png" width="339" height="170" />](http://janmarek.eu/wp-content/uploads/2015/01/image4.png) 

4. Označit koncový runbook. Opět celý runbook a ne klikat do jeho obsahu! 

5. V menu zvolit Edit – Paste

[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://janmarek.eu/wp-content/uploads/2015/01/image_thumb5.png" width="226" height="173" />](http://janmarek.eu/wp-content/uploads/2015/01/image5.png) 

Tenhle postup funguje dle očekávání. A to se vyplatí :)))