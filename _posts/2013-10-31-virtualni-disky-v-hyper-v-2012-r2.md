---
id: 665
title: Virtuální disky v Hyper-V 2012 R2
date: 2013-10-31T08:00:54+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=665
permalink: /2013/10/31/virtualni-disky-v-hyper-v-2012-r2/
categories:
  - Hyper-V
  - Nezařazené
  - Windows Server 2012 R2
---
V tomto článku bych rád osvětlil možnosti virtuálních disků, jejich rozdíly a ve zkratce i určité výkonové srovnání. Výčet možných konfigurací cílím na Hyper-V 2012 R2, ačkoli mnoho z nich můžete provozovat i na starších verzích Hyper-V (2008, 2008 R2, 2012).

Data dostupná pro virtuální servery lze umístit dvěma nejzákladnějšími způsoby – na **fyzický disk** (dedikovaný pro konkrétní virtuální server), nebo na **virtuální disk** reprezentovaný souborem (VHD/VHDX) na file systému.

Využití fyzického disku (také označováno jako _passthrough disk_) bylo z historického pohledu nejvýkonnější variantou. Dnes je ale použití VHD(X) souboru výkonově identický s fyzickým diskem.

Tato konfigurace vyžaduje fyzický disk připojený jakýmkoli způsobem k Hyper-V serveru (DAS, SAN, apod.). Ve správci disků je nutné tento disk pouze inicializovat a přepnout do stavu offline.

[<img class="aligncenter size-full wp-image-667" alt="virtual-disks-in-hv-2012-r2-Capture1" src="/wp-content/uploads/2013/10/Capture1.png" width="258" height="100" />](/wp-content/uploads/2013/10/Capture1.png)

V tuto chvíli je disk viditelný v konfiguraci virtuálního serveru v Hyper-V.

<p style="text-align: center;">
  <a href="/wp-content/uploads/2013/10/Capture2.png"><img class="aligncenter  wp-image-668" alt="virtual-disks-in-hv-2012-r2-Capture2" src="/wp-content/uploads/2013/10/Capture2.png" width="439" height="415" /></a>
</p>

Následuje konfigurace logických jednotek standardním způsobem uvnitř virtuálního serveru.

Použití passthrough disku je možné i u vysoce dostupných virtuálních serverů v rámci Hyper-V clusteru a tím pádem není ani omezeno využití přesunu pomocí Live Migration atd.

Druhým způsobem, jak zajistit diskový prostor pro virtuální server, je použití zmiňovaných VHD, nebo VHDX, souborů. VHD (z angl. _Virtual Hard Disk_). Formát VHD je používán velmi dlouho od svého zrození společností Connectix v jejich produktu Virtual PC, později koupeno společností Microsoft a to do technologií Microsoft Virtual PC a Microsoft Virtual Server. Maximální velikost VHD souboru je 2040GB. Kompletní vnitřní strukturu najdete popsanou v rámci Microsoft Open Specification Promise např. [zde](http://technet.microsoft.com/en-us/library/bb676673.aspx).

Formát VHDX byl zrozen na platformě Windows Server 2012, resp. pod technologií Hyper-V 2012. Tento formát využívá částečně shodnou strukturu s VHD s rozdílem přidané interní sekce logu (pro ochranu dat) a metadata. Disk se vyznačuje větší velikostí logického sektoru až na 4KB (oproti 512B u VHD) a celkovou velikostí až 64TB. Kompletní specifikace je opět k dispozici např. [zde](http://www.microsoft.com/en-us/download/details.aspx?id=34750). Svými dalšími vlastnostmi je samozřejmě VHDX nejlepší volbou ať už z pohledu poskytované ochrany dat, velikosti, funkcí ale i výkonu a kapacity.

V Hyper-V si lze stále vybrat z obou možností – VHD nebo VHDX formátu a to především pro potřeby zpětné kompatibility.

[<img class="aligncenter size-full wp-image-669" alt="virtual-disks-in-hv-2012-r2-Capture3" src="/wp-content/uploads/2013/10/Capture3.png" width="505" height="119" />](/wp-content/uploads/2013/10/Capture3.png)

Samotné virtuální disky VHD(X) se dělí ještě dále do typů:

  * Fixed Size
  * Dynamically Expanding
  * Differencing

[<img class="aligncenter size-full wp-image-670" alt="virtual-disks-in-hv-2012-r2-Capture4" src="/wp-content/uploads/2013/10/Capture4.png" width="508" height="231" />](/wp-content/uploads/2013/10/Capture4.png)

Fixed Size je typ disku, který zajišťuje nejvyšší výkon, a velikost zvolená při vytváření disku je ihned alokována na fyzickém file systému. Vyrobíme-li například 10GB Fixed Size VHDX soubor, zapíšeme do něj 225MB dat, tak na fyzickém file systému bude VHDX soubor zabírat 10GB prostoru. Výkon získává právě díky nepřítomnosti jakékoli funkce dynamického přidělování diskového prostoru. Je také ale jasnou volbou pro infrastruktury s potřebami vysoké bezpečnosti vzhledem k „přepsání“ všech stávajících „magnetických“ dat na využitém fyzickém diskovém úložišti.

<p style="text-align: center;">
  <a href="/wp-content/uploads/2013/10/Capture5.png"><img class="aligncenter  wp-image-671" alt="virtual-disks-in-hv-2012-r2-Capture5" src="/wp-content/uploads/2013/10/Capture5.png" width="317" height="185" /></a>
</p>

Dynamically Expanding disk se již na základě svého pojmenování chová dynamicky a místo je na fyzickém úložišti alokováno na základě množství dat zapsaného do VHDX souboru. Vyrobíme-li opět 10GB Dynamically Expanding VHDX soubor a zapíšeme do něj 225MB dat, tak na fyzickém file systému bude zabírat cca 228MB prostoru (velikost nebude přesně 225MB vzhledem k vnitřní struktuře VHDX souboru, především z důvodu velikosti header části). Dynamické disky se tedy hodí pro úsporu diskového prostoru, ale vyznačují se mírně menším výkonem než Fixed Size disky a mají také určitá omezení (např. možnosti zálohování pomocí komponenty Data Protection Manager produktu System Center 2012).

<p style="text-align: center;">
  <a href="/wp-content/uploads/2013/10/Capture6.png"><img class="aligncenter  wp-image-672" alt="virtual-disks-in-hv-2012-r2-Capture6" src="/wp-content/uploads/2013/10/Capture6.png" width="317" height="185" /></a>
</p>

Differencing (rozdílový) disk je vlastně dynamickým diskem, ale zároveň je použit pro zapsání (a čtení) dat rozdílových oproti nadřazenému (parent) disku. Rozdílový disk tedy nemůže nikdy existovat pouze sám o sobě, ale vždy minimálně v páru s parent diskem. Celý koncept vám pravděpodobně připomíná funkci snapshotů/checkpointů a to je správná úvaha, protože právě zde se rozdílové disky používají automaticky (v tomto případě mají soubory koncovku AVHD(X)).

Vezměme například scénář, kdy potřebujeme velice rychle vyrobit 20 identických virtuálních serverů, které všechny používají uvnitř operační systém Windows Server 2008 R2. Pokud byste použili pro každý virtuální server dynamický disk a vzhledem k opravdové velikosti zapsaných dat (řekněme 9GB per virtuální server), celkem by těchto 20 virtuálních serverů zabralo cca 180GB (20 x 9GB). Pokud byste ovšem využili rozdílových disků, pak byste pouze vyrobili jeden zdrojový (parent/nadřazený) disk s instalací Windows Server 2008 R2 operačního systému a 20 differencing disků, vše by zabralo pouze cca 10GB! (1x 9GB + 20x 50MB). Počítal jsem cca 50MB rozdílových dat po provedení sysprepu a další konfigurace. To je samozřejmě značná úspora prostoru, ale bohužel na úkor výkonu a vzniklých omezení. I přesto je tento koncept hojně využíván u testovacích prostředí a VDI.

Takto vytvoření rozdílový disk se ale zároveň může stát parent diskem pro další rozdílové disky. Takto se můžeme dostat na velké množství navzájem závislých disků a vytváříme tzv. Differencing Chain (řetěz rozdílových disků). Ve všech případech ale platí velmi zásadní pravidlo – nikdy neměníme jakýmkoli způsobem parent disk – docházelo by k nekonzistenci.

<p style="text-align: center;">
  <a href="/wp-content/uploads/2013/10/Capture7.png"><img class="aligncenter  wp-image-673" alt="virtual-disks-in-hv-2012-r2-Capture7" src="/wp-content/uploads/2013/10/Capture7.png" width="613" height="227" /></a>
</p>

U Windows Server 2012 R2 ještě navíc přichází další novinka v podobě sdíleného VHDX souboru (Shared VHDX). V tomto případě je umožněno více virtuálním serverům zapisovat/číst data z jednoho VHDX souboru. Tato konfigurace je výhodná pro formování clusterů uvnitř virtuálních serverů.

[<img class="aligncenter size-full wp-image-674" alt="virtual-disks-in-hv-2012-r2-Capture8" src="/wp-content/uploads/2013/10/Capture8.png" width="438" height="188" />](/wp-content/uploads/2013/10/Capture8.png)

Velice zajímavou funkcí je také omezení výkonu VHD(X) souboru a to per každý soubor (virtuální disk). Můžeme tak zajistit adekvátní výkon jednotlivým poskytovaným službám/zákazníkům a zároveň snižujeme riziko vzájemného ovlivňování výkonu. Máme k dispozici tedy minimální (garantovaný) výkon v IOPS a maximální (limitní výkon) v IOPS.

[<img class="aligncenter size-full wp-image-675" alt="virtual-disks-in-hv-2012-r2-Capture9" src="/wp-content/uploads/2013/10/Capture9.png" width="432" height="190" />](/wp-content/uploads/2013/10/Capture9.png)

Jak vidíte správná volba adekvátního typu virtuálního disku je velmi důležitá a má vliv na mnoho faktorů, ať už je to prostý výkon, či kompatibilita (resp. omezení) s dalšími systémy.
