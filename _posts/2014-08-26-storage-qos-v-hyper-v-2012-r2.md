---
id: 776
title: Storage QoS v Hyper-V 2012 R2
date: 2014-08-26T10:09:00+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=776
permalink: /2014/08/26/storage-qos-v-hyper-v-2012-r2/
categories:
  - Hyper-V
  - Nezařazené
tags:
  - Hyper-V
---
Windows Server 2012 R2 uvedený v loňském roce přinesl mnoho novinek. Velké množství bylo cíleno především na potřeby virtualizace serverů. Vyberme dnes jednu z mnoha, která ale může mít zásadní vliv na alokaci zdrojů a může být řešením mnoha výkonnostních otázek. Jedná se o Storage Quality of Service (QoS), tedy zajištění a řízení výkonu virtuálního disku v Hyper-V. 

### Komponenty

Na Hyper-V 2012 R2 lze provozovat obrovské množství operačních systémů. Je potřeba je ale rozdělit do dvou skupin – na podporované (nativní) OS a ostatní (legacy). Nativní OS (tedy plně podporovaný, funkcionálně i výkonově testovaný) je systém, který díky přítomnosti integračních služeb provádí optimalizované, efektivní a „chytré“ I/O operace skrze virtuální datovou sběrnici (VMBus). Na jednom konci této sběrnice, uvnitř virtuálního systému (tzv. child partition), běží služba Virtualization Service Client (VSC) a na konci druhém, uvnitř fyzického operačního systému, běží služba Virtualization Service Provider (VSP). Samotná sběrnice je komponenta, která běží čistě v paměti, a proto může zajistit vysoký výkon. 

[<img title="clip_image001" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="clip_image001" src="/wp-content/uploads/2014/12/clip_image001_thumb.png" width="244" height="168" />](/wp-content/uploads/2014/12/clip_image001.png) 

Každý virtuální systém (VM) má svou vlastní sadu komponent VSC-VMBUS-VSB. Ve skutečnosti pak ještě každá VM má 4 různé VSC a VSP – síť, úložiště, video a zařízení na dalších rozhraních. My se teď více zaměříme na úložiště. VSC úložiště reprezentuje ovladač storvsc.sys a VPS storvsp.sys. Tahle informace se hodí, když například řešíte příčiny BSoD (Blue Screen of Death) J. Zároveň jsou tyto dva ovladače klíčové pro veškeré diskové I/O operace a tedy i pro QoS. 

Storage QoS má dvě možnosti konfigurace, kromě samotného povolení funkcionality. Obě se nastavují v pokročilé konfiguraci každého virtuálního disku. 

[<img title="clip_image003" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="clip_image003" src="/wp-content/uploads/2014/12/clip_image003_thumb.jpg" width="244" height="158" />](/wp-content/uploads/2014/12/clip_image003.jpg) 

### Minimum IOPS

První možností je nastavení hodnoty tzv. Mimimum IOPS, tedy jakési rezervace výkonu pro daný virtuální disk. Nejedná se o hodnotu, která by reálně „ořezávala“ výkon ostatních disků pro zajištění výkonu toho konkrétního, ale o jakousi minimální hranici výkonu, kterou je nutné zajistit. 

[<img title="clip_image004" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="clip_image004" src="/wp-content/uploads/2014/12/clip_image004_thumb.png" width="25" height="6" />](/wp-content/uploads/2014/12/clip_image004.png)[<img title="clip_image005" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="clip_image005" src="/wp-content/uploads/2014/12/clip_image005_thumb.png" width="244" height="92" />](/wp-content/uploads/2014/12/clip_image005.png) 

Co se tedy stane, když nastavíme hodnotu větší než je fyzický diskový subsystém schopen poskytnout? Hyper-V kontinuálně sleduje vyžadované množství IOPS uvnitř VM a také množství IOPS, které má systém ještě volné pro jiné VM. Pokud tento poměr klesá, tak je pomocí Storage IO balanceru realokován výkon. Pokud se již systém dostane do stavu, kdy nemůže zajistit požadovaný výkon, vygeneruje WMI (Windows Management Instrumentation) Event. Tuto událost lze sledovat buď obečejnou WMI Notification Query (např. dotazem přes PowerShell, nebo WMI Testerem) nebo nástrojem pro dohled &#8211; System Center 2012 R2 Operations Manager. Okamžitě jsme tedy informováni o nedostatku výkonu a můžeme ihned reagovat (přerozdělením výkonu, přesunutím disku na rychlejší diskové pole, přidáním fyzických disků do diskového pole). 

[<img title="clip_image007" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="clip_image007" src="/wp-content/uploads/2014/12/clip_image007_thumb.jpg" width="155" height="244" />](/wp-content/uploads/2014/12/clip_image007.jpg) 

### Maximum IOPS

Druhou možností konfigurace je limitace maximální diskového výkonu (IOPS). Celý proces je v tomto případě plně v režii StorVSP.sys a omezování výkonu je tedy prováděno na úrovni fyzického OS. Stejně jako u Minimum IOPS lze zde nastavit hodnotu 0 pro neomezený výkon (na Hyper-V 2012 R2 tedy až 2mio IOPS). 

[<img title="clip_image009" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="clip_image009" src="/wp-content/uploads/2014/12/clip_image009_thumb.jpg" width="244" height="119" />](/wp-content/uploads/2014/12/clip_image009.jpg) 

Obrázek výše ukazuje neomezenou konfiguraci Maximum IOPS. Vzhledem k rychlosti fyzického disku jsme tedy na cca 50tis. IOPS. 

[<img title="clip_image011" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="clip_image011" src="/wp-content/uploads/2014/12/clip_image011_thumb.jpg" width="244" height="119" />](/wp-content/uploads/2014/12/clip_image011.jpg) 

Obrázek výše ukazuje konfiguraci Maximum IOPS omezenou na 2000 IOPS. Rekonfiguraci je možné provádět za běhu VM a limitace výkonu je provedena okamžitě. 

Maximum IOPS je tedy skvělou možností, jak plnohodnotně řídit přidělený výkon a minimalizovat možnost omezení výkonu jiných služeb. Je ovšem také velmi důležitou funkcí v případě Hyper-V clusteru. V případě běhu dvou VM na stejném nodu clusteru s disky na stejném cluster disku (CSV, sdíleném všemi nody clusteru) bude plně fungovat Minimum IOPS a Hyper-V je schopno realokovat výkon. V případě přesunu jedné z VM na jiný node clusteru ale Hyper-V nemůže sledovat zajištění výkonu disku, protože se jedná o informaci udržovanou vždy pouze v rámci jednoho serveru. Aby tedy druhá VM příliš nezatěžovala sdílený cluster disk (CSV) je klíčové použít právě limitaci Maximum IOPS. 

V operačním systému Windows totiž neexistuje žádná funkce Storage QoS na úrovni CSV, celého clusteru či fyzického disku. Lze případně použít funkce dostupné na vašem externím diskovém poli, nebo produkty třetích stran. Hyper-V Storage QoS je tedy skvělým pomocníkem.
