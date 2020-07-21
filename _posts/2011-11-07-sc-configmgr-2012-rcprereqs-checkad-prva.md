---
id: 355
title: SC ConfigMgr 2012 RC–prereqs check–AD práva
date: 2011-11-07T14:31:51+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/2011/11/07/sc-configmgr-2012-rcprereqs-checkad-prva/
permalink: /2011/11/07/sc-configmgr-2012-rcprereqs-checkad-prva/
jabber_published:
  - "1320672712"
  - "1320672712"
categories:
  - Nezařazené
  - SC Configuration Manager
tags:
  - SCCM
  - SCCM2012
---
<div class="wlWriterHeaderFooter" style="float:none;margin:0;padding:4px 0;">
  <a href="http://www.facebook.com/widgets/like.php?href=https://jmarek.wordpress.com/2011/11/07/sc-configmgr-2012-rcprereqs-checkad-prva/">http://www.facebook.com/widgets/like.php?href=https://jmarek.wordpress.com/2011/11/07/sc-configmgr-2012-rcprereqs-checkad-prva/</a>
</div>

Jedním z důležitých nastavení před samotnou instalaci SCCM site, je dát účtu site serveru práva na container System Management v AD, aby mohl po instalace MP zapsat patřičné záznamy. Když instalujete větší SCCM hierarchii s hodně site servery, hodí se nastavit oprávnění na doménovou skupinu a přidat všechny site servery jako její členy.

V RC SCCM 2012 ovšem udělali očividně v prerequisite checkeru kontrolu “natvrdo” a proto při použití dom.skupiny je výsledkem Warning. Není se ovšem čeho bát, protože i tak má ůčet práva a proto bude vše fungovat. Je to ale bod, kterého se může člověk leknout…

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="sccm2012rc_prereq" border="0" alt="sccm2012rc_prereq" src="http://janmarek.eu/wp-content/uploads/2011/11/sccm2012rc_prereq_thumb.png" width="244" height="184" />](http://janmarek.eu/wp-content/uploads/2011/11/sccm2012rc_prereq.png)