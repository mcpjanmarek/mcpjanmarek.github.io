---
id: 962
title: jak spustit v PowerShell skript, který má v cestě mezeru
date: 2015-08-13T10:29:16+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=962
permalink: /2015/08/13/jak-spustit-v-powershell-skript-ktery-ma-v-ceste-mezeru/
categories:
  - Nezařazené
  - PowerShell
---
Já se teda snažím vždycky vyhnout v názvech souborů a adresářů mezerám, ale kolega jmenovec to tu řešil a někdy se prostě může hodit jak na to&#8230;

Co chtěl udělat? Spustit skript přes Invoke-Expression v plné cestě. Takže třeba něco jako:

<pre>Invoke-Expression 'C:\users\Jan\Desktop\test script.ps1'</pre>

Tohle vám ale cestu nepobere&#8230;

<pre><span style="color: #ff0000;">C:\users\Jan\Desktop\test : The term 'C:\users\Jan\Desktop\test' is not recognized as the name of a cmdlet,...</span></pre>

Jak to teda udělat? Stačí přihodit magický znak &#8222;**&**&#8222;.

S proměnnou by to vypadalo takto:

<pre>$file = & 'C:\users\Jan\Desktop\test script.ps1'
Invoke-Expression $file</pre>

Bez proměnné, tedy napřímo do cmdletu, takto:

<pre>Invoke-Expression $(& 'C:\users\Jan\Desktop\test script.ps1')</pre>

Ještě jde použít escape znak &#8222;**\`**&#8220; před mezeru, což ručně se dá udělat třeba takhle:

<pre>Invoke-Expression 'C:\users\Jan\Desktop\test` script.ps1'</pre>

Vkládat to ale vždycky růčo do cesty je nuda a tak ještě možnost, jak automaticky nahrazovat takto:

<pre>Invoke-Expression $('C:\users\Jan\Desktop\test script.ps1'.replace(' ','` '))</pre>

That&#8217;s it!