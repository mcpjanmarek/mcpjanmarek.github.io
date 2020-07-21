---
id: 327
title: Unsupported stavy virtuálního stroje v SC Virtual Machine Manageru
date: 2011-10-25T17:16:39+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/2011/10/25/unsupported-stavy-virtulnho-stroje-v-sc-virtual-machine-manageru/
permalink: /2011/10/25/unsupported-stavy-virtulnho-stroje-v-sc-virtual-machine-manageru/
jabber_published:
  - "1319555799"
  - "1319555799"
categories:
  - Nezařazené
  - SC Virtual Machine Manager
tags:
  - SCVMM
---
**Tento článek si můžete přečíst především také na stránkách školícího centra WBI Systems: <http://learning.wbi.cz>**

Při správě vašeho virtuálního prostředí pomocí System Center Virtual Machine Manager 2008 (dále jen SCVMM) se můžete setkat se stavy virtuálního stroje (VM) informujících o Unsupported Cluster Configuration. Pojďme se na ně podívat.

### Non-CSV cluster disk

Od vzniku Hyper-V, tedy OS Windows Server 2008, je samozřejmě možné poskytovat vysoce dostupné virtuální stroje (HAVM). Ovšem jediné možnost migrace, která byla dostupná, byla Quick Migration (uložení-kopírování/přepnutí_disku-obnova). Jedním z kroků bylo právě „přepnutí“ LUNu, změna vlastníka, na cílový nod clusteru. Pro zajištění této operace je nutné zajistit, aby disky každého virtuálního stroje byly uloženy na samostnaném LUN, odpovídajícím cluster disku.

Do této situace se samozřejmě můžeme dostat ještě dnes s verzí R2, která nabízí možnosti využití funkcionality Cluster Shared Volume, která není ve výchozím stavu ale povolena.

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border:0;" title="noncsv" src="/wp-content/uploads/2011/10/noncsv_thumb.png" alt="noncsv" width="240" height="169" border="0" />](/wp-content/uploads/2011/10/noncsv.png)

### Non-cluster disk

Situace nejčastěji vzniká při vytváření clusteru až po vytvoření VM na standalone Hyper-V serverech. Dochází k tomu, že je konfigurována HAVM, která má ovšem diskový subsystém uložený na lokálním disku nodu clusteru. Tato konfigurace zabraňuje přesunu VM ať již metodou Quick či Live Migration.

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border:0;" title="noncluster" src="/wp-content/uploads/2011/10/noncluster_thumb.png" alt="noncluster" width="240" height="173" border="0" />](/wp-content/uploads/2011/10/noncluster.png)

### Cluster resources

Tento problém je vázaný pouze na clustery provozované na Windows Server 2008 a spravované pomocí SCVMM 2008. HAVM se skládá z různých cluster resources. Cluster resource představuje jednotlivé komponenty HAVM, které pro svůj běh potřebuje. Jedná se o samotný objekt HAVM, její konfiguraci a fyzické cluster disky, na kterých je uložený její diskový prostor (odstavec víš máš diskový subsystém) a konfigurace. Pouze právě tyto 3 cluster resources jsou podporované správou SCVMM 2008. Veškeré jiné ji uvádějí do unsupported cluster stavu (např. third-party řešení pro replikaci úložiště při multi-site clusterech, geo-clusterech atd.)

### ISO

Ve verzi SCVMM 2008 je detekován unsupported stav také v případě, kdy HAVM má připojený ISO soubor do virtuální mechaniky. Problém se vyskytuje jak při použití lokálních ISO image, tak u souborů z VMM library resp, UNC cest. Tento problém byl vyřešen ve verzi SCVMM 2008 R2.

_Pozn.: V aktuální verzi SCVMM 2012 Release Candidate se opět znovu projevuje tento syndrom._

### Virtual Networks

Jedním z nejdůležitějších bodů cluster řešení je „naprosto shodná konfigurace všech nodů clusteru“! Disky, velikost RAM, sítě, instalované patche a další a další konfigurace je právě validována při vytváření clusteru. Tento validátor ovšem nekontroluje dost důkladně pojmenování virtuálních/síťových adaptérů. Nejčastěji se proto stává, že jste při konfiguraci virtuálních sítí v Hyper-V manageru udělali překlep při pojmenování. Pro SCVMM, který je závislý na tomto jménu, je pak HAVM, která využívá tuto nekonzistentní konfiguraci, v unsupported stavu. Tomuto můžete předejít důkladnou kontrolou nebo konfigurací virtuálních sítí až po vytvoření clusteru z SCVMM. Řešení problému je jednoduché – upravit názvy.
