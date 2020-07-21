---
id: 1727
title: PowerShell a barvy ve Wordu
date: 2017-08-10T12:28:45+02:00
author: Jan Marek
layout: post
guid: http://janmarekwww.azurewebsites.net/?p=1727
permalink: /2017/08/10/powershell-a-barvy-ve-wordu/
categories:
  - PowerShell
tags:
  - PowerShell
---
V rámci některých našich projektů pracujeme se zápisem dat automatizovaně do Microsoft Word dokumentu. V rámci zápisu dat do tabulek občas potřebujeme i obarvovat některé buňky. Barvy se ve Wordu ale nepoužícají u Cell objektů v RGB ale ve formátu Microsoft Access, nebo taky wdColor. Napsal jsem teda mikrofunkci, která převede RGB na wdColor. Třeba se vám to bude taky někdy hodit.

<pre class="lang:ps decode:true ">function Convert-RGB2WDColor {
     [cmdletbinding()]
     param(
     [Parameter(Mandatory=$true)][int]$Red,
     [Parameter(Mandatory=$true)][int]$Green,
     [Parameter(Mandatory=$true)][int]$Blue
     )
     $WDColor = [long] ($blue + ($green * 256) + ($red * 65536))
     return $WDColor

}

Convert-RGB2WDColor -Red 255 -Green 255 -Blue 255</pre>

&nbsp;
