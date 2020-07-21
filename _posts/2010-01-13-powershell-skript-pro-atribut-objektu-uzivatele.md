---
id: 42
title: Powershell skript pro atribut objektu uzivatele
date: 2010-01-13T09:07:45+02:00
author: Jan Marek
layout: post
guid: http://jmarek.wordpress.com/2010/01/13/powershell-skript-pro-atribut-objektu-uzivatele
permalink: /2010/01/13/powershell-skript-pro-atribut-objektu-uzivatele/
spaces_1d3f038117de6df561f7bf0516bb226c_permalink:
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!249')?authkey=EpZNAU0huAk%24"
  - "http://cid-6e7b9216726d07b8.users.api.live.net/Users(7961117391414167480)/Blogs('6E7B9216726D07B8!242')/Entries('6E7B9216726D07B8!249')?authkey=EpZNAU0huAk%24"
categories:
  - Active Directory
  - Nezařazené
---
<div id="msgcns!6E7B9216726D07B8!249" class="bvMsg">
  <div>
    <h2>
      <font size="2">Skript pro zobrazeni urciteho atributu uzivatele v AD (napr. pro Telephone Notes atribut pouzijte INFO, tedy: </p> 
      
      <p>
        <font color="#ffff00" size="2" face="Verdana">return &aduser.info</font>)</font></h2> 
        
        <div>
          <p>
            <code><em><font color="#ffff00" size="2" face="Verdana">function get-ldapuser ($username, $querydc) &#123;<br />$domain = new-object DirectoryServices.DirectoryEntry ("LDAP://$querydc)<br />$searcher = new-object DirectoryServices.DirectorySearcher($domain)<br />$searcher.filter = "(&(objectclass=user)(samaccountname=$username))"<br />$searcher.findone().getDirectoryEntry()<br />&#125;</font></em></p>
<p><font color="#ffff00" size="2" face="Verdana">$prefdc = "DCServerName.DomainName.com"<br />$lookupid = "loginname"<br />$aduser = get-ldapuser $lookupid $prefdc</font></p>
<p><font color="#ffff00" size="2" face="Verdana">return &aduser.nameoftheobjectattribute</font></p>
</div>
</div>
</div>
