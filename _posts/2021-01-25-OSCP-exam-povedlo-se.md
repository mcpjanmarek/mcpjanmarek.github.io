---
title: OSCP exam - povedlo se!
author: Jan Marek
layout: post
---
Dnes jsem obdržel email s potvrzením, že jsem úspěšně složil OSCP exam. Rozhodně to nebyla sranda a když nad tím přemýšlím, tak se jednalo o asi nejtěžší exam, který jsem v životě dělal. Je to prostě kombinace hození do vody a tikajících hodin. Zlomit prostě 5 serverů za 24 hod. není úplná pohodička.

Když jsem dělal zkoušku poprvé (listopad 2020), tak se mi podařilo hacknout 2 z 5. Dělal jsem na tom skoro celých 24h - začínal jsem ve 4 ráno, jel v kuse bez spánku, jen s přestávkami.

Tento druhý pokus jsem si naplánoval na jednu odpoledne. Ani ne tak, že bych vyloženě chtěl, ale nebylo moc dobrých časů dostupných. Za hodinu jsem položil první server, za další hodinu další a za další další. Takže za první tři hodiny tři servery. Pak mi trvalo asi 3 další hodiny než jsem dostal usera na čtvrtém serveru, to bylo tedy cca 7 večer. A pak nastalo peklo s privesc. Našel jsem dva vektory, skrze které by to šlo, ale ani jeden mi pořádně nefungoval. Nakonec jsem se rozhodl jít víc jen po jednom z nich. Exploit na něj mi ale nefungoval, tak jsem pořád přemýšlel, zda je to správná cesta, nebo to je slepá ulička. Nakonec se ukázalo, že to slepá ulička není a problém byl v samotném exploitu. Našel jsem si asi pět webů s kompletním researchem zranitelnosti, snažil se ji pochopi a následně podle toho upravit kód exploitu. To se mi nakonec povedlo a ve tři ráno jsem rootnul čtvrtý server.

Tím jsem měl vyhráno a protože jsem už padal na hubu, tak jsem šel spát. Asi za 6 hodin jsem vstal a šel zkusit zlomit poslední server. Našel jsem initial, ale už jsem nevěděl kudy dál a protože se to točilo kolem webů, což naprosto nesnáším, tak jsem to vzdal (asi hodinu před koncem času) a šel psát report. Asi za 4 hodiny jsem měl report hotový a kolem páté odpoledne jsem ho uploadoval na OffSec.

Dostal asi 5x info, že teď budu čekat až 10 pracovních dní na výsledek. Naštěstí dnes, cca. po 24 hod. od uploadu reportu, mi přišel email, že passed.

V kostce ta zkouška je částečně strašně super a částečně prdelní (lepší slovo mě nenapadá). Každopádně to byla super zkušenost a rozhodně jsem se mraky toho naučil a jsem za to moc rád.

Velké díky všem, kteří mě podpořili a hlavně své ženě, která mi umožnila věnovat svůj čas na učení se (nejen na tuto zkoušku) a celou dobu ve mě věřila a podporovala mě (a že to bylo potřeba, protože po prvním examu to bylo dost demotivující - selhat po roce učení).

Ještě jedna poznámka na závěr, která se netýká jen této zkoušky - nedělej zkoušky jen pro ty zkoušky. Cílem je se něco naučit a ta zkouška by jen měla ověřit hlavně tobě, že ses to skutečně naučil a pochopil.
