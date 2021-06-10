---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2018.
keywords: ID-tjänst
title: Versionsinformation 2018
exl-id: ad3cccf1-2753-4ac9-a68c-15b2d62bbc1a
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Versionsinformation 2018 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2018.

## Version 3.3 {#section-3202c8d5457a45a5b5f4b4c838d44de3}

<table id="table_201417BD540E4EE69911AABE9BF77509"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Artikelbeskrivning </th> 
   <th colname="col2" class="entry"> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Ökad säkerhet för AMCV-cookies </p> </td> 
   <td colname="col2"> <p>Under en intern säkerhetssökning upptäcktes att cookies som används för sessionshantering inte kan ange korrekta attribut när DTM-biblioteket används. Detta kan leda till att cookie-information delas av misstag. För att lösa detta har vi infört en konfiguration som gör det möjligt för kunden att ställa in AMCV-cookien som säker. Se <a href="/help/library/function-vars/securecookie.md" format="https" scope="external"> secureCookie</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Version 3.2 {#section-ae2fee1c152e405faa4eb395f960e2f6}

<table id="table_6546F5C74E4742E4B5E9793BCEAB66FA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Artikelbeskrivning </th> 
   <th colname="col2" class="entry"> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Ökad säkerhet för AMCV-cookies </p> </td> 
   <td colname="col2"> <p>Under en intern säkerhetssökning upptäcktes att cookies som används för sessionshantering inte kan ange korrekta attribut när DTM-biblioteket används. Detta kan leda till att cookie-information delas av misstag. För att lösa detta har vi infört en konfiguration som gör det möjligt för kunden att ställa in AMCV-cookien som säker. Se secureCookie. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Integrationskod och id måste vara tal eller strängar som inte är tomma </p> </td> 
   <td colname="col2"> <p>Korrigerade ett problem med validering av "setCustomerID" när data innehåller en integration "code" eller "id" som varken är ett tal eller en sträng som inte är tom. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ECID JS är tillgängligt i Git-rapporten </td> 
   <td colname="col2"> ECID JS finns nu i Git-rapporten för alla Experience Cloud-kunder på https://github.com/Adobe-Marketing-Cloud/id-service/releases. </td> 
  </tr> 
 </tbody> 
</table>

## Version 3.1.2 {#section-3cba186f74fe4f2186a9ca2e5e0a2514}

<table id="table_9FA4E20C996746A2A4219C9A0F759AD1"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Artikelbeskrivning </th> 
   <th colname="col2" class="entry"> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Orealistisk topp i det unika besökarantalet </p> </td> 
   <td colname="col2"> <p>I och med lanseringen av Experience Cloud Identity Service 3.1.0 har vi hittat ett problem som skapade en orealistisk topp i det unika besökarantalet när den här versionen implementerades. Detta beteende visas endast med den senaste versionen av ECID, v3.1.0, och om en användare har valt alternativet"Tillåt endast från aktuell webbplats" i sekretessinställningarna för en Safari. Version 3.1.2 åtgärdar det här problemet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Version 3.1.0 {#section-a20c8278bf9643018965330415091e53}

>[!NOTE]
>
>Vi rekommenderar att du snarast uppgraderar från version 3.1.0 till den senaste versionen. Se beskrivningen av version 3.1.2. Det senaste paketet finns i Adobe Experience Platform Launch, DTM och AppMeasurement.

<table id="table_512039AFC4D34038B8F116B71EEEE7F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Artikelbeskrivning </th> 
   <th colname="col2" class="entry"> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Cookie inställd på felaktig domän </p> </td> 
   <td colname="col2"> <p>Vi har åtgärdat ett fel där den tillfälliga Visitor-cookien angav en cookie i standardcookie-domänen i stället för att ange den i domänen som anges i konfigurationen (initConfig). </p> </td> 
  </tr> 
 </tbody> 
</table>

## Version 3.0 {#section-5fcaef66e8b343238abeb10048dc5747}

<table id="table_7E9224D6CC924A2DB5119171C9DC5443"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Artikelbeskrivning </th> 
   <th colname="col2" class="entry"> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Tråd som genererar flera ID-synkroniseringsbegäranden </p> </td> 
   <td colname="col2"> <p><b>Iframe</b> </p> <p>För kunder som utför flera ID-synkroniseringar blockeras gränssnittet i vissa fall på grund av kontinuerliga CPU-beräkningar. Vi introducerar trådgenerering som separerar begäranden om ID-synkronisering med 100 msek vardera. </p> <p>Den här förändringen förbättrar prestanda för kunder som använder Visitor 2.3.0+ och DIL 6.10+. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Lagt till möjlighet att inaktivera tredjepartssamtal </td> 
   <td colname="col2"> <p><b>JavaScript - 3.0.0</b> </p> <p>Adobe har bytt namn på följande konfigurationer så att tredjepartssynkroniseringsanrop kan inaktiveras. </p> <p>idSyncDisableSyncs till disableIdSyncs </p> <p>idSyncDisable3rdPartySyncing to disableThirdPartyCookies </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Stöd för Internet Explorer </p> </td> 
   <td colname="col2"> <p>ID-tjänsten stöder inte längre Internet Explorer 6, 7, 8 och 9. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Uppdatera till getInstance-dokumentation </p> </td> 
   <td colname="col2"> <p>En varning har lagts till i besökarfunktionen om att funktionen inte instansieras med var visitor = new Visitor. </p> </td> 
  </tr> 
 </tbody> 
</table>
