---
id: 24
title: Export AD Computers’ names
date: 2010-03-03T13:05:40+02:00
author: Jan Marek
layout: post
guid: 'http://jmarek.wordpress.com/2010/03/03/export-ad-computers%e2%80%99-names'
permalink: /2010/03/03/export-ad-computers-names/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!275')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!275')?authkey=EpZNAU0huAk%24"
categories:
  - Active Directory
  - Nezařazené
tags:
  - Active Directory
  - AD
  - dsquery
---
<div id="msgcns!6E7B9216726D07B8!275" class="bvMsg">
  You can very simply export all computers in AD to txt file for example like this:</p> 
  
  <div>
  </div>
  
  <div>
    this command exports 10000 computers
  </div>
  
  <div>
    <code>dsquery computer -limit 10000 &gt;C:computers.txt</code>
  </div>
  
  <div>
  </div>
  
  <div>
    next command exports 10000 computers&#8216; SAMIDs attributes of computers located in organization unit Workstations.
  </div>
  
  <div>
    <code>dsquery computer ou=workstations,dc=domain,dc=local -limit 10000 -o samid &gt;c:computers.txt</code>
  </div>
  
  <div>
  </div>
  
  <div>
    for more information run dsquery /? and for detailed informations about object do combine dsquery with dsget&#8230;
  </div>
</div>

