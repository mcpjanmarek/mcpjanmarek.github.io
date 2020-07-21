---
id: 27
title: 'Remote Assistance &#8211; networking'
date: 2010-02-25T10:32:34+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/02/25/remote-assistance-networking
permalink: /2010/02/25/remote-assistance-networking/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!255')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!255')?authkey=EpZNAU0huAk%24"
categories:
  - Nezařazené
  - Uncategorized
tags:
  - networking
---
<div id="msgcns!6E7B9216726D07B8!255" class="bvMsg">
  <div>
    If you&#8217;ve got a firewall between the client and a computer (with configmgr console installed) you may expect some problems with establishing remote assistance connection.
  </div>
  
  <div>
  </div>
  
  <div>
    Communication between them starts on the RPC port. They say each others&#8216; port number on which they start a Remote Assistance session. This port is dynamically selected from a range up from 1024. So, you need to open the RPC port number 135 and then all ports up from 1024. This can raise a risk in your infrastructure, so other option is to limit RPC dynamic ports range on clients by modification the registry key HKEY LMsoftwaremicrosoftrpcinternetports. Then you can limit the outbound communication from computer with console to client to only these ports. But in the other way (from client to server) you need to leave it opened for all ports. If you modify the other way you may except problems with other services (for ex. AD).
  </div>
</div>