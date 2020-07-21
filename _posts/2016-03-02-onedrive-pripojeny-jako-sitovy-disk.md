---
id: 1100
title: OneDrive připojený jako síťový disk
date: 2016-03-02T21:29:47+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1100
permalink: /2016/03/02/onedrive-pripojeny-jako-sitovy-disk/
categories:
  - Microsoft
  - Nezařazené
tags:
  - OneDrive
---
Od Windows 10 máme &#8222;skvělý&#8220; nový engine OneDrivu, který neumí on-demand stáhnout soubor z cloudu a musíte si tedy navolit, které složky chcete synchronizovat. Problém je v tom, že složky/soubory, které nesynchronizujete, neuvidíte na disku vůbec. Škoda, tuhle funkci jsem měl v předchozí verzi rád.

Já si teda ještě mapuji svůj OneDrive jako network drive. Jak na to?

  1. Přihlašte se přes onedrive.com na svůj onedrive.
  2. Klikněte vlevo v navigaci na Soubory (Files)
  3. Nyní by URL měla vypadat nějak takto: <span style="color: #0000ff;"><em>https://onedrive.live.com/?id=root&cid=<strong>00AAB3D7DDF12AF7</strong></em></span>
  4. Vykopírujte si z URL to poslední ID. V mém příkladu tedy <span style="color: #0000ff;"><em><strong>00AAB3D7DDF12AF7</strong></em></span>
  5. Teď klasicky ve File Exploreru namapujte nový disk svými OneDrive credentials pomocí cesty: <span style="color: #0000ff;"><em>https://d.docs.live.net/<strong>00AAB3D7DDF12AF</strong></em></span>

A je to. Enjoy!

