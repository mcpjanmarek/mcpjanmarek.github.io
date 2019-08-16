---
id: 1192
title: Řadiče domény správně registrován ve službě DNS?
date: 2010-02-25T10:33:43+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/02/25/dcs-properly-registered-in-dns
permalink: /2010/02/25/radice-domeny-spravne-registrovan-ve-sluzbe-dns/
categories:
  - Nezařazené
  - Uncategorized
---
<div id="msgcns!6E7B9216726D07B8!258" class="bvMsg">
  <div>
    Chcete mít jistotu s DC SRV registrace záznamu DNS?
  </div>
  
  <div>
    Spusťte příkaz NSLOOKUP, změňte typ SRV (set querytype = srv) a spusťte dotaz pro konkrétní doménu pomocí _LDAP. Například:
  </div>
  
  <div>
    _ldap._tcp.DC._msdcs.Domain.suffix nebo _ldap._tcp.dc._msdcs.subdomain.domain.suffix.
  </div>
  
  <div>
  </div>
  
  <div>
    Nikdy nepodceňujte to! Správně nakonfigurovaný server DNS je základní věci pro mnoho dalších služeb.
  </div>
</div>