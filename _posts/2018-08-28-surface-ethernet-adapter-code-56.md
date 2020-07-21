---
id: 1858
title: 'Surface Ethernet Adapter &#8211; Code 56'
date: 2018-08-28T08:57:18+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1858
permalink: /2018/08/28/surface-ethernet-adapter-code-56/
categories:
  - Windows 10
tags:
  - Surface Pro
  - Windows 10
---
Dnes se mi už snad po padesáté projevil problém s USB Ethernet síťovkou k mému Surface Pro s Windows 10 1803, tak se s vámi o něj v krátkosti podělím.

Situace je následující. Nainstalujete si čistý OS na Surface a připojíte USB Ethernet a vše jede jak má. Krása. Po čase používání OS zase připojíte USB Ethernet a nic. V Network Connections vůbec síťovku nevidíte a v device manager je s vykřičníkem a errorem 56.

<blockquote class="wp-block-quote">
  <p>
    Windows is still setting up the class configuration for this device. (Code 56)
  </p>
</blockquote>

Jak z toho ven? Udělal jsem kernel debug toho ovladače a našel jsem, že v kolizi při volání CheckPoint VPN klienta. Když jsem ručně schodil driver CheckPoint VPN, tak se hned USB Ethernet rozjel.

Takže co s tím? Odinstalovat CheckPoint VPN klienta. A jak to řešit dlouhodobě? V mém případě mám virtuálku, kde mám všechny tyhle ošklivé VPN interfaces.__