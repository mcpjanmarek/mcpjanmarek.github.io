---
id: 1203
title: Exportovat jména AD počítače
date: 2010-03-03T13:05:40+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/03/03/export-ad-computers%e2%80%99-names'
permalink: /2010/03/03/exportovat-jmena-ad-pocitace/
categories:
  - Nezařazené
  - Uncategorized
---
<div id="msgcns!6E7B9216726D07B8!275" class="bvMsg">
  Všechny počítače v AD můžete velmi jednoduše exportovat do txt souboru například takto:</p> 
  
  <div>
  </div>
  
  <div>
    Tento příkaz exportuje 10000 počítačů
  </div>
  
  <div>
    <code>dsquery počítač-limit 10000 video C:computers.txt</code>
  </div>
  
  <div>
  </div>
  
  <div>
    Následující příkaz exportuje 10000 počítače SAMIDs atributy počítače v organizační jednotce pracovních stanic.
  </div>
  
  <div>
    <code>dsquery ou počítač = pracovních stanic, dc = domain, dc = local - samid limit 10000 -o video c:computers.txt</code>
  </div>
  
  <div>
  </div>
  
  <div>
    Další informace spustit dsquery /? a pro podrobnější informace o objektu kombinovat například s dsget&#8230;
  </div>
</div>
