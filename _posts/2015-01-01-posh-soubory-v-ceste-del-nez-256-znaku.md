---
id: 834
title: 'posh: soubory v cestě delší než 256 znaků'
date: 2015-01-01T23:06:48+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=834
permalink: /2015/01/01/posh-soubory-v-ceste-del-nez-256-znaku/
categories:
  - Nezařazené
  - PowerShell
tags:
  - PowerShell
---
Dnes jsem trochu bojoval se synchronizací OneDrive souborů. Nakonec byl poblém v tom, že některé soubory jsem měl v tolika podadresářích, že už takhle dlouho cestu OneDrive nezvládl. Blbé bylo ale to, že OneDrive psal jen, že některé soubory mají příliš dlouhou cestu (více než 256 znaků), ale už nepsal o jaké soubory se jedná. Vyrobil jsem si tedy takový jednoduchý mikro skript v PowerShellu, abych je našel. Tady je, pokud ho budete jednou taky potřebovat (ať už na cokoli)…

> get-childitem D:\Onedrive -Recurse | foreach-object { 
> 
> &nbsp;&nbsp; if ($_.pspath.length -ge 256) { 
> 
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; write-host ‘Path Length:’ –f white –b black 
> 
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; write-host $_.pspath.length -f cyan -b black 
> 
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; write-host ‘File Path:’ –f white –b black 
> 
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; write-host $_.fullname -f yellow -b black 
> 
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; write-host 
> 
> &nbsp;&nbsp; } 
> 
> }

Ano, dalo by se to udělat do tabulky, ale takhle mi to stačilo 🙂

[<img title="posh-path-length" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="posh-path-length" src="/wp-content/uploads/2015/01/poshpathlength_thumb.png" width="658" height="173" />](/wp-content/uploads/2015/01/poshpathlength.png)
