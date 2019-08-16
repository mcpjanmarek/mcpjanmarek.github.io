---
id: 269
title: Microsoft System Center Configuration Manager 2012 Beta 2 – přehled
date: 2011-04-17T21:13:57+02:00
author: Jan Marek
layout: post
guid: https://jmarek.wordpress.com/2011/04/17/microsoft-system-center-configuration-manager-2012-beta-2-prehled/
permalink: /2011/04/17/microsoft-system-center-configuration-manager-2012-beta-2-prehled/
jabber_published:
  - "1303067638"
  - "1303067638"
categories:
  - Nezařazené
  - SC Configuration Manager
tags:
  - Configuration Manager
  - Configuration Manager 2012
  - SCCM
  - SCConfigMgr
---
**Tento článek si můžete přečíst především také na stránkách školícího centra WBI Systems: <http://learning.wbi.cz>**

Na Microsoft Connectu je možné si po předchozí registraci stáhnout betu nejnovější verzi Configuration Manageru – nyní již také označovanou jako 2012. V tomto článku se podíváme na budoucnost deploymentu a change managementu z pohledu Microsoftu, kterými bude verze 2012 disponovat. Na úvod se probereme serverou infrastrukturou, přejdeme na změny v Desired Configuration Managementu a Reportingu, ale především zaostříme na inteligentní distribuci aplikací.

Jako úplně první – změny v konzoly. Microsoft přešel z MMC na Outlook Based Interface, který obdobně využívají další System Center produkty. S tímto se zároveň přejde na Role Based Access Control, tudíž uvidíte jen ty položky, ke kterým máte práva. To přinese z velké míry také jednodušší konfiguraci oprávnění než tomu bylo dosud.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="1" border="0" alt="1" src="http://janmarek.eu/wp-content/uploads/2011/04/1_thumb.png" width="244" height="171" />](http://janmarek.eu/wp-content/uploads/2011/04/1.png)

Serverová část Configuration Manageru by měla být vydaná pouze v x64 verzi. Remote Distribution Point Share, ale bude samozřejmě možné provozovat i na x32 platformě. Tímto vás, ale pravděpodobně hned napadne otázka migrace z verze 2007. Vzhledem k rozdílnosti funkcí a samotné infrastruktury půjde rozhodně o side-by-side migraci. Bude ji možné provést na konkrétních stanicích, přičemž budou zmigrovány aplikace a další konfigurace (DCM politiky apod.) a na závěr samotný klient. Na export/import nástrojích Microsoft pracuje a měly by být vydány současně s verzí 2012.

Stejně jako verze 2007, tak i 2012 potřebuje ke své plné funkčnosti rozšíření schéma Active Directory. Objekty se ovšem nezměnily, proto je možné použít k LDF soubor z verze 2007 – více na <http://technet.microsoft.com/en-us/library/bb632388.aspx>. Obecné systémové požadavky ale můžeme vyvodit z bety. Jako operační systém pro serverovou část použijte Windows Server 2008 R2. Pro databázi můžete použít Microsoft SQL Server 2008 SP1. 

<u>Hierarchie</u>

**Central Administration Site** použijete pouze v případě, že máte více jak jeden Primary Site server. CAS je vždy vrcholem celé Configuration Managerem hierarchie. Ve verzi 2012 již ale neobhospodařuje klienty, ale pouze shromažďuje informace z podřízených site. Instaluje se vždy jako první, pokud je tedy potřeba. 

**Primary Site** je serverem, který obhospodařuje velké množství stanic, které jsou k němu připojeny rychlou linkou. Jeho nadřízenou site je vždy CAS a podřízenými mohou být pouze Secondary Site servery. Zajišťuje databázovou replikaci na další site. PS je také zodpovědná za Active Directory discovery.

**Secondary Site** se využívá pro správu malého množství stanic, které jsou odděleny od PS pomalou linkou. Slouží tedy jako „proxy“ s PS. Protože se zúčastňuje replikace objektů, vyžaduje přítomnost SQL Serveru (pokud není k dispozici je automaticky nainstalován SQL Server Express). Instalace SS může být vyvolána vzdáleně z PS. Při její instalaci jsou automaticky nainstalovány role Proxy Management Point a Distribution Point.

Největší zajímavostí z pohledu site je replikace objektů, která bude nově založena na SQL replikaci a ne na File Based replikaci. Samozřejmě, že na Distribution pointy budou stále balíčky posílány „souborově“. Při použití Branch Distribution Pointu je možnost přenosu po oddělěných Senderech a tím tedy bude možné nakonfigurovat parametry přenosu mezi body. Lepší bude i použití Distribution Point Group. Pokud budete mít aplikaci odeslanou na tuto skupinu, tak při přidání dalšího Distribution pointu do skupiny bude aplikace přenesena i na něj.

Nastavení **Client Agents** (HW inventura, SW inventura, Remote Tools, atd.) se konfiguruje na úrovni CAS, ale nově je možné je nastavit na úrovni collection a tím tedy nakonfigurovat každého klienta nejoptimálněji.

&#160;

[<img style="background-image:none;padding-left:0;padding-right:0;display:inline;padding-top:0;border-width:0;" title="2" border="0" alt="2" src="http://janmarek.eu/wp-content/uploads/2011/04/2_thumb.png" width="244" height="163" />](http://janmarek.eu/wp-content/uploads/2011/04/2.png)

**Desired Configuration Management** bude nově používat Auto Remediation. Tzn., že pokud stanice nebude odpovídat stanovené konfiguraci, bude možné na ní automaticky provést nápravu. Nápravné kroky musíte ale stále vyrobit sami.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="3" border="0" alt="3" src="http://janmarek.eu/wp-content/uploads/2011/04/3_thumb.png" width="238" height="244" />](http://janmarek.eu/wp-content/uploads/2011/04/3.png)

Reporting ve verzi 2012 bude operovat pouze nad SQL Server **Reporting Services**. Standardní webové reporty, které bylo doteď ještě možné používat, již nebudou dostupné.

Ve verzi 2012 se poměrně zásadně mění pohled na distribuci aplikací a to na tzv. „**User Centric Computing**“. V praxi to znamená, že aplikace bude cestovat s uživatelem bez ohledu na to, se kterou stanicí pracuje v aktuální chvíli a kde. Kromě balíčků ve 2012 najdete i Aplikace. Nově tedy přibudou tzv. **Requirement Rules**, které budou stanovovat, jakou aplikaci, ale především jakým distribučním způsobem, kam distribuovat. Úmyslně jsem použil slovo distribuovat a ne instalovat, protože aplikace může být na stanici doručena i jinými metodami. Jako první uvedu streaming virtualizované aplikace (který je podporován už nyní ve verzi 2007 R2), který nabídne uživateli aplikaci prakticky okamžitě a aplikace se natahuje uživateli po blocích, které aktuálně potřebuje využívat. Další možností je Remote Desktop Service aplikace, která fyzicky běží v datacenteru. Poslední možností je zmiňovaná fyzická instalace aplikace na stanici.

Pomocí výše uvedených **Requirement Rules** je možné nasadit uživateli jednu aplikaci všemi způsoby. Pokud tedy bude uživatel na korporátní síti, bude pracovat s aplikací virtualizovanou a pokud přejde např. domů k své stanici, která má připojení pouze do internetu, je mu ta samá aplikace nabídnuta před Remote Desktop Services.

[<img style="background-image:none;border-bottom:0;border-left:0;padding-left:0;padding-right:0;display:inline;border-top:0;border-right:0;padding-top:0;" title="4" border="0" alt="4" src="http://janmarek.eu/wp-content/uploads/2011/04/4_thumb.png" width="244" height="171" />](http://janmarek.eu/wp-content/uploads/2011/04/4.png)

Samozřejmě je zde možnost přiřazení uživatele k jeho stanici, kterou používá každý den a tím lépe specifikovat deployment. K dispozici jsou i přiřazení typu uživatel pracující na více stanicích, či stanice používaná více uživateli. Metoda přiřazování se nazývá **User Device Affinity.**

Podporou pro uživatele bude např. **Software Catalog** – webový katalog, kde si budou moci vybrat aplikaci a zadat požadavek na její deployment. Následně pak ve svém lokálním **Software Center** zvolit preferované metody doručení aplikace na stanici.

Závěrem lze tedy říci, že je opravdu na co se těšit a ConfigMgr 2012 tak bude dalším System Center produktem, který bude velice zásadní měnit pohled na správu prostředí.