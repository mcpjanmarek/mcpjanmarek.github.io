---
id: 1105
title: Jak vzdáleně povolit PowerShell Remoting
date: 2016-03-09T14:23:32+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=1105
permalink: /2016/03/09/jak-vzdalene-povolit-powershell-remoting/
categories:
  - Nezařazené
  - PowerShell
---
Anglicky by ten titulek zněl ještě líp &#8211; How to remotely enable PowerShell Remoting 🙂

Samozřejmě to nejlépe uděláte přes GPO například. Pokud to ale potřebujete ihned, tak můžete použít PSEXEC (ať žije Mark! :))

<pre class="theme:classic lang:batch decode:true ">psexec.exe \\clientpc1 powershell.exe "Enable-PSRemoting -Force"</pre>

A pak už to valí a můžete třeba přes Enter-PSSession jít na CLIENTPC1 a powershellit.
