---
id: 716
title: Dynamic Access Control a Device Claims
date: 2014-01-23T18:43:48+02:00
author: Jan Marek
layout: post
guid: http://janmarek.eu/blog/?p=716
permalink: /2014/01/23/dynamic-access-control-a-device-claims/
categories:
  - Nezařazené
  - Windows 8
  - Windows 8.1
  - Windows Server 2012
  - Windows Server 2012 R2
---
Dnes jsem se začal trochu více do hloubky šťourat v Dynamic Access Control. Konfigurace Resource Properties a Claims pro uživatele podle atributu v Active Directory fungovala okamžitě a bez problémů. Měl jsem tedy chuť vyzkoušet Device Claim.

Všude v Microsoft prezentacích se popisuje krásný příklad, kdy povolujete přístup pouze z určitého zařízení (příklad obsahuje podmínku Device.Managed = True). Tak jsem se rozhodl si udělat Device Claim s identifikací země stanice (takže atribut Country (c) na Computer objektu).

[<img class="aligncenter size-full wp-image-718" src="/wp-content/uploads/2014/01/dac1-computer.png" alt="dac1-computer" width="464" height="140" />](/wp-content/uploads/2014/01/dac1-computer.png)

[<img class="aligncenter size-full wp-image-717" src="/wp-content/uploads/2014/01/dac1-car.png" alt="dac1-car" width="916" height="497" />](/wp-content/uploads/2014/01/dac1-car.png)

Protože tedy kvůli tomu potřebuji řešit i Device Claim, tak jsem přes Group Policy povolil politiku &#8222;Computer Polices &#8211; Administrative Templates &#8211; System &#8211; Kerberos &#8211; Kerberos Client support for claims, compound authentication and Kerberos Armoring&#8220;. GPupdate na stanici a hned se to chytlo. Ze stanice ze země, která neodpovídala pravidlu, jsem přístup nedostal. Takže funkční scénář.

[<img class="aligncenter size-full wp-image-721" src="/wp-content/uploads/2014/01/dac1-kerbarmor-enabled.png" alt="dac1-kerbarmor-enabled" width="227" height="163" />](/wp-content/uploads/2014/01/dac1-kerbarmor-enabled.png)

Co takhle to zkusit ale ze stanice, která je na stejné síti, ale není členem domény. Takže Windows 8.1 klient, přihlášení pod Microsoft Accountem a test na UNC cestu toho file sharu. Samozřejmě se to zeptalo na credentials a následně to přístup nedalo. Takže taky super funkční.

Protože jsem ale ještě pak trochu modifikoval tu doménovou politiku, tak se mi podařilo dostat do situace, kdy jsem podporu pro Claims, apod. vypnul.

[<img class="aligncenter size-full wp-image-720" src="/wp-content/uploads/2014/01/dac1-kerbarmor-disabled.png" alt="dac1-kerbarmor-disabled" width="241" height="167" />](/wp-content/uploads/2014/01/dac1-kerbarmor-disabled.png)

Zkusil jsem to v tu chvíli ze stroje mimo doménu a na share jsem se dostal! Asi je to tak správně, protože si to v mám politice zapnout, ale pak mi přijde, že je to celé takové pochybné. Dám tu ještě pár hodin a pak to budu akceptovat jako vlastnost 🙂

UPDATE: Po dalších třiceti minutách jsem na to přišel. Není to tou politikou, ale jen pravidlem, což dává samozřejmě smysl. Když udělám Central Access Rule bez Device Claimu, tak se z nedoménové stanice na share dostanu a když s Device Claimem, tak samozřejmě ne. Chovalo se mi to předtím blbě, protože jsem občas zapomněl udělat gpupdate asi 🙂 Tady jsou pro zajímavost ještě screenshoty z Effective Accessu. První bez device claimu a druhý s device claimem.

[<img class="aligncenter size-full wp-image-719" src="/wp-content/uploads/2014/01/dac1-effectiveaccess-userclaim.png" alt="dac1-effectiveaccess-userclaim" width="605" height="569" />](/wp-content/uploads/2014/01/dac1-effectiveaccess-userclaim.png)[<img class="aligncenter size-full wp-image-722" src="/wp-content/uploads/2014/01/dac1-effectiveaccess-userclaim-and-devicelaim.png" alt="dac1-effectiveaccess-userclaim-and-devicelaim" width="773" height="737" />](/wp-content/uploads/2014/01/dac1-effectiveaccess-userclaim-and-devicelaim.png)
