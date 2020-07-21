---
id: 955
title: 'Windows Store error #800F7003'
date: 2015-07-30T10:34:16+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=955
permalink: /2015/07/30/windows-store-error-800f7003/
categories:
  - Nezařazené
  - WBI Systems
  - Windows 8.1
---
Kdyby vám náhodou našla nainstalovat žádná appka z Windows Store na Windows 10, tak si upravte v cestě:

**HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folder**

registrový klíč: **CACHE**

na hodnotu: **%USERPROFILE%\AppData\Local\Microsoft\Windows\Temporary Internet Files**

Mělo by to teda pak vypadat takhle:

[<img class="aligncenter size-full wp-image-956" src="/wp-content/uploads/2015/07/error-803f7003-fix-regedit.png" alt="error-803f7003-fix-regedit" width="1010" height="146" />](/wp-content/uploads/2015/07/error-803f7003-fix-regedit.png)Tohle mi zafungovalo btw. i na Windows 8.1&#8230;

&nbsp;
