---
id: 1970
title: Problém se sdílenou složkou ve VirtualBox
date: 2019-07-03T14:11:30+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/?p=1970
permalink: /2019/07/03/problem-se-sdilenou-slozkou-ve-virtualbox/
categories:
  - Nezařazené
tags:
  - VirtualBox
---
Už několikrát jsem na to narazil a pokaždé to zapomenu, takže spíše poznámka pro mne. Pokud sdílíte složku z hostitele do VM ve VirtualBox a uvnitř VM nepoužíváte přímo root účet, tak narazíte na problém s právy.

Stačí jen uživatele přidat do správné skupiny a hned to jede:

<blockquote class="wp-block-quote">
  <p>
    sudo usermod -aG vboxsf <userlogin>
  </p>
</blockquote>