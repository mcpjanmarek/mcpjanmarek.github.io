---
id: 342
title: Windows Server 8 (DevEd) DC Instalace
date: 2011-10-27T13:07:34+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/2011/10/27/windows-server-8-deved-dc-instalace/
permalink: /2011/10/27/windows-server-8-deved-dc-instalace/
jabber_published:
  - "1319713659"
  - "1319713659"
categories:
  - Active Directory
  - Nezařazené
  - Windows Server 2012
tags:
  - Active Directory
  - AD
  - ADDS
  - Windows Server 2012
---
<div class="wlWriterHeaderFooter" style="float:none;margin:0;padding:4px 0;">
  <a href="http://www.facebook.com/widgets/like.php?href=https://jmarek.wordpress.com/2011/10/27/windows-server-8-deved-dc-instalace/">http://www.facebook.com/widgets/like.php?href=https://jmarek.wordpress.com/2011/10/27/windows-server-8-deved-dc-instalace/</a>
</div>

Včera jsem si kvůli připravované konferenci WBI viz. [http://learning.wbi.cz/kurzy/59-30-wbi-knowit-2011.aspx](http://learning.wbi.cz/kurzy/59-30-wbi-knowit-2011.aspx "http://learning.wbi.cz/kurzy/59-30-wbi-knowit-2011.aspx") instaloval doménový řadič na Windows Server 8 DE. A rád bych se s vámi podělil o zkušenost.

DCPROMO příkaz nefunguje! Po jeho spuštění na vás vyskočí hláška,že je nutné provést instalaci doménových služeb pomocí Server Manageru… OK, provedl jsem tedy instalaci ADDS a spustil znovu DCPROMO. Neee! Opět to nefunguje! Výsledkem je opět hláška, která tentokrát poukazuje na nutnost konfigurace opět pomocí Server Manageru (WinSrvMgr). Znovu tedy zpět do WinSrvMgr a nastalo hledání, kde je odkaz na vyvolání konfigurace DC (na Windows Server 2008 R2 se vám zobrazil odkaz hned na úvodní stránce konfigurace Rolí). Vše se skrývalo pod malou událostní ikonkou. Po jejím spuštění se načetl wizard:

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="1" border="0" alt="1" src="/wp-content/uploads/2011/10/1_thumb.png" width="244" height="172" />](/wp-content/uploads/2011/10/1.png)

Wow! Nový wizard, nová grafika! A co možnosti konfigurace? Většina zůstala stejná. Ovšem DFL a FFL nabízí novou položku **Windows Server 8.** Zkusme to tedy.

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="2" border="0" alt="2" src="/wp-content/uploads/2011/10/2_thumb.png" width="244" height="171" />](/wp-content/uploads/2011/10/2.png)[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="3" border="0" alt="3" src="/wp-content/uploads/2011/10/3_thumb.png" width="244" height="172" />](/wp-content/uploads/2011/10/3.png)

Celou konfiguraci můžete po dokočení provést pomocí Powershell skriptu resp. commandletu Install-ADDSForest, který je nový. Že by tedy odzvonilo unattended souboru u DCPROMO?

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="4" border="0" alt="4" src="/wp-content/uploads/2011/10/4_thumb.png" width="244" height="178" />](/wp-content/uploads/2011/10/4.png)

Následuje kontrola konfigurace pomocí Prerequisite Checku, který ale u mě nedopadl dobře.

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="5" border="0" alt="5" src="/wp-content/uploads/2011/10/5_thumb.png" width="244" height="172" />](/wp-content/uploads/2011/10/5.png)

Všimněte si řádky **The Specified value ‘5’ is not valid for the argument ‘DomainLevel’.** Což pravděpodobně znamená, že sice můžete zvolit DFL Windows Server 8, ale systém na to není ještě připraven. Zpět tedy na Windows Server 2008 R2 a problém vyřešen.

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="6" border="0" alt="6" src="/wp-content/uploads/2011/10/6_thumb.png" width="244" height="171" />](/wp-content/uploads/2011/10/6.png)

Wizard už je skoro u konce, kliknutím na Install se provede odpovídající operace, jejíž průběh je poměrně detailně zobrazován.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="7" border="0" alt="7" src="/wp-content/uploads/2011/10/7_thumb.png" width="244" height="172" />](/wp-content/uploads/2011/10/71.png)

To je tedy pár změn v instalaci doménového řadiče na WS8. A pokud vás zajímá, proč jsem to vůbec celé “klikal”, pak nezapomeňte dorazit na nasí dvoudenní konferenci, viz výše!
