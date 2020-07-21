---
id: 25
title: DCs properly registered in DNS?
date: 2010-02-25T10:33:43+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/02/25/dcs-properly-registered-in-dns
permalink: /2010/02/25/dcs-properly-registered-in-dns/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!258')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!258')?authkey=EpZNAU0huAk%24"
categories:
  - Active Directory
  - Nezařazené
tags:
  - Active Directory
  - AD
---
<div id="msgcns!6E7B9216726D07B8!258" class="bvMsg">
  <div>
    Do you want to be sure with DC SRV record registration in DNS?
  </div>
  
  <div>
    Run NSLOOKUP command, change type to SRV (set querytype=srv) and then run query for particular domain using _LDAP. For example:
  </div>
  
  <div>
    _ldap._tcp.dc._msdcs.domain.suffix or _ldap._tcp.dc._msdcs.subdomain.domain.suffix.
  </div>
  
  <div>
  </div>
  
  <div>
    Never underestimate that! Properly configured DNS server is the basic stuff for many other services!
  </div>
</div>
