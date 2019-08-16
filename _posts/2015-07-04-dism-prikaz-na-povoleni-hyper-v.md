---
id: 975
title: DISM příkaz na povolení hyper-V
date: 2015-07-04T17:07:37+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=975
permalink: /2015/07/04/dism-prikaz-na-povoleni-hyper-v/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2012
  - Windows Server 2012 R2
tags:
  - Hyper-V
---
Pokud už musíte použít DISM tool na povolení Hyper-V role ve Windows Server, tak dejte pozor na to, že název funkce je case-sensitive! Dnes jsem zažil opět další z tisíce připomínek, že přes DISM to prostě nejde… Jde, ale musí se to pořádně napsat�<img class="wlEmoticon wlEmoticon-winkingsmile" style="border-style: none;" src="http://janmarek.eu/wp-content/uploads/2015/09/wlEmoticon-winkingsmile.png" alt="Winking smile" /> 

Když si vylistujete všechny features pomocí:

<pre>dism /online /get-features</pre>

tak uvidíte, že Hyper-V role je schovaná pod **<u>M</u>icrosoft-<u>H</u>yper-<u>V</u>** názvem.

K povolení tedy musíte dodržet velká a malá písmena, tedy:

<pre>dism /online /enable-feature /featurename:Microsoft-Hyper-V</pre>

Radši to ale přes DISM vůbec nedělejte a použite místo toho PowerShell…