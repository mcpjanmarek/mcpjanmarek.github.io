---
layout: post
title: Problém se sdílenou složkou ve VirtualBox!
---

Už několikrát jsem na to narazil a pokaždé to zapomenu, takže spíše poznámka pro mne. Pokud sdílíte složku z hostitele do VM ve VirtualBox a uvnitř VM nepoužíváte přímo root účet, tak narazíte na problém s právy.

Stačí jen uživatele přidat do správné skupiny a hned to jede:

sudo usermod -aG vboxsf <userlogin>