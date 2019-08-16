---
id: 359
title: Audit členství ve skupině Domain Admins
date: 2011-11-17T15:40:28+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/?p=359
permalink: /2011/11/17/audit-clenstv-ve-skupine-domain-admins/
jabber_published:
  - "1321540828"
  - "1321540828"
categories:
  - Active Directory
  - Nezařazené
tags:
  - Active Directory
  - AD
  - ADDS
---
<div class="wlWriterHeaderFooter" style="float:none;margin:0;padding:4px 0;">
  <a href="http://www.facebook.com/widgets/like.php?href=https://jmarek.wordpress.com/2011/11/17/audit-clenstv-ve-skupine-domain-admins/">http://www.facebook.com/widgets/like.php?href=https://jmarek.wordpress.com/2011/11/17/audit-clenstv-ve-skupine-domain-admins/</a>
</div>

Zjistil jsem, že to není úplně moc známá věc a proto ji tu zde uvádím. Na doménách W2k3 a W2k8 je by default nastaven auditing např. na skupinu Domain Admins. Když mrknete na Security záložku – Advanced – Auditing, tak uvidíte hned první pravidlo, ve kterém se povoluje audit akce Write Members. Výsledkem při modifikaci členů ve skupině jsou pak 3 (případně 4) události. Každá kromě informací níže obsahuje i informace o uživateli, který změnu provedl (sekce Subject).

První s Event ID 4662 (An operation was performed on an object) ukazující na změnu v konfiguraci security na skupině.

Dále následuje Event s ID 4737 (A security-enabled global group was changed) obsahující informaci o změně členství ve skupině a její původní členy.

Poslední událost s ID 4728 (A member was added to a security-enabled global group), který poskytuje informace o přidaném uživateli do skupiny. Pokud v rámci jedné modifikace členství přidáte více uživatelů, pak v eventlogu uvidíte odpovídající počet událostí s event ID 4728.

Pro doplnění ještě dodám, že samozřejmě i odebrání uživatele ze skupiny je logováno. A to událostí s ID 4729 (A member was removed from a security-enabled global group).

Obrázek ukazuje události nejprve o odebrání uživatele ze skupiny (ID 4662,4737 a 4729) a po chvíli přidání dvou uživatelu do skupiny (ID 4662,4737 a dvakrát 4728).

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="audit_domain_admins_membership" border="0" alt="audit_domain_admins_membership" src="http://janmarek.eu/wp-content/uploads/2011/11/audit_domain_admins_membership_thumb.jpg" width="580" height="294" />](http://janmarek.eu/wp-content/uploads/2011/11/audit_domain_admins_membership.jpg)