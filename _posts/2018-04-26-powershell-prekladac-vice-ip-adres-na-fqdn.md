---
id: 1838
title: PowerShell překladač více IP adres na FQDN
date: 2018-04-26T12:44:30+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1838
permalink: /2018/04/26/powershell-prekladac-vice-ip-adres-na-fqdn/
categories:
  - PowerShell
tags:
  - PowerShell
---
<pre class="lang:ps decode:true ">$IPAddresses = '8.8.8.8','127.0.0.1'

foreach ($IP in $IPAddresses)
{
	"$IP `t`t $([System.Net.Dns]::GetHostByAddress($IP).HostName)"
}</pre>

&nbsp;

