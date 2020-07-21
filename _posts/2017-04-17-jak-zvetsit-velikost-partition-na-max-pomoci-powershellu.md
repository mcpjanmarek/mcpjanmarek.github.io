---
id: 1691
title: Jak zvětšit velikost partition na max pomocí PowerShellu
date: 2017-04-17T13:24:40+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1691
permalink: /2017/04/17/jak-zvetsit-velikost-partition-na-max-pomoci-powershellu/
categories:
  - PowerShell
tags:
  - PowerShell
---
Rychlovka bez většího komentáře 🙂

<pre class="lang:ps decode:true " >[string]$FileSystemLabel = 'CSV3'

$PartitionMaxSize = Get-Volume -FileSystemLabel $FileSystemLabel | Get-Partition | Get-PartitionSupportedSize | Select-Object -ExpandProperty sizemax

Get-Volume -FileSystemLabel $FileSystemLabel | Get-Partition | Resize-Partition -Size $PartitionMaxSize</pre>
