---
id: 590
title: Problém s vytvořením nového Hyper-V Switche po ugradu na WS 2012 R2
date: 2013-10-26T10:31:55+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=590
permalink: /2013/10/26/problem-s-vytvorenim-noveho-hyper-v-switche-po-ugradu-na-ws-2012-r2/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2012 R2
---
Pokud jste se rozhodli provést inplace upgrade vašeho Hyper-V serveru na Windows Server 2012 R2, pak si dejte pozor na jeden drobný zádrhel.

Předpokládejme, že máte Windows Server 2012 fyzický server s rolí Hyper-V, kde provozujete několik virtuálních počítačů. Řekněme, že tyto virtuální počítače po dobu upgradu přesunete na jiný server. Na Hyper-V serveru tedy máte pro externí komunikaci VM vytvořený externí virtuální switch. Ten je samozřejmě namapován na fyzický adaptér.

Pokud tento virtuální switch před upgradem neodeberete, pak po upgradu při pokusu o vytvoření nového switche, na stejném adaptéru dostanete chybovou hlášku, že tento adaptér je už použit pro jiný virtuální switch. Ale přitom vy žádný jiný nemáte!

[<img class="alignleft size-full wp-image-609" alt="error-create-virtual-eth-switch-adapter-is-already-bound-to-the-ms-vswitch-protocol" src="/wp-content/uploads/2013/10/error-create-virtual-eth-switch-adapter-is-already-bound-to-the-ms-vswitch-protocol.png" width="367" height="247" />](/wp-content/uploads/2013/10/error-create-virtual-eth-switch-adapter-is-already-bound-to-the-ms-vswitch-protocol.png)

Co s tím? Odmapovat Hyper-V extensible switch rozhraní z NIC není jednoduchý úkon a ani nevím, jestli řešení, na které jsem přišel je podporované Microsoftem a proto tedy zbývá odinstalovat Hyper-V roli a nainstalovat ji zpět&#8230;. nebo tedy smažte virtuální switche před upgradem 😉
