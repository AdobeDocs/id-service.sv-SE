---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2017.
keywords: ID-tjänst
title: Versionsinformation 2017
exl-id: 0b51d3b1-e405-4473-9e1a-f89a55250e5e
source-git-commit: 384b292413bbc7e43ade97e442ab7195f3b26c7a
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 3%

---

# Versionsinformation 2017 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2017.

Dessa ändringar registreras också i [Versionsinformation om Experience Cloud](https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html?lang=sv).

>[!NOTE]
>
>Det finns inga kundvända versionsinformation eller kodändringar för mars, april, maj och oktober 2017. För dessa månader förblev ID-tjänstkoden oförändrad vid v2.1.

## Version 2.5 {#section-27b441509124493f80984ed09bd9e88b}

September 2017

<!--
<p>
<note type="important">
ID service support for Internet Explorer 6, 7, and 8 is deprecated and will be discontinued in a future release.
</note> </p>
-->

<table id="table_FD24C06C7B3547C3A7673C46B1852A35"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> getVisitorValues</span> </p> </td> 
   <td colname="col2"> <p>Detta är ett asynkront API som returnerar identifierare för Analytics, ID-tjänsten, avanmälan av datainsamling, geografisk plats och metadatablockinnehåll som standard. Du kan också styra vilka ID:n du vill returnera med det valfria <span class="codeph"> besökare.FÄLT</span> enum. Se <a href="../library/get-set/getvisitorvalues.md#reference-b8c9e17c170c4291829a792df46ce279" format="dita" scope="local"> getVisitorValues</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Felkorrigeringar och andra ändringar**

* Korrigerade ett Chrome-relaterat fel som gjorde att ID-tjänsten utlöste ett fel när användaren klickade på bakåtknappen i webbläsaren.
* ID-tjänsten utlöser nu synkronisering igen när region-ID:t i händelsesvaret ändras.
* Lagt till ny dokumentation, [Skyddsprofiler för innehåll och Experience Cloud Identity Service](/help/reference/csp.md#concept-968c423a7392479db0a0d821ae9783e3)som förklarar hur du vitlistar anrop till Adobe-domäner som används av ID-tjänsten.

<!-- ## Version 2.4 {#section-f4d1608dd8894f558a92b82e83321200}

August, 2017

<table id="table_D9623D34F4444B038F7835750932C8AA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Feature </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> isCoopSafe</span> </p> </td> 
   <td colname="col2"> <p>An optional, Boolean configuration that determines if the ID service sends (or does not send) data to the Adobe Experience Cloud Device Co-op. See <a href="../library/function-vars/coopsafe.md#reference-7fbed36f38a048d1a5883c53d430ddf4" format="dita" scope="local"> isCoopSafe</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Revised Documentation**

Updated and revised the [FAQs](/help/faq-intro/faq-intro.md) to include separate FAQs for different [!DNL Experience Cloud] solutions. -->

## Version 2.3 {#section-ae7b1cb1e52e4ca5a46b453a3ba1f571}

Juli 2017

<table id="table_1448040D09B94A74883A694FCF91EB33"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> sdidParamExpiry</span> </p> </td> 
   <td colname="col2"> <p>När de läggs till i <span class="codeph"> Visitor.getInstance</span> kan du med den här konfigurationen åsidosätta standardintervallet för SDID (Supplemental Data ID) när du skickar det ID:t från en sida till en annan. Du skulle använda <span class="codeph"> sdidParamExpiry</span> med <span class="codeph"> appendSupplimentalDataTo</span> hjälpfunktion. Se <a href="../library/function-vars/sdidparamexpiry.md#reference-cef3fd03c43b4772b2422e220b40a458" format="dita" scope="local"> sdidParamExpiry</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> resetState</span> </p> </td> 
   <td colname="col2"> <p>Den här funktionen är främst avsedd för A4T-kunder för att hjälpa till att lösa problem som rör arbete med ID:n på enstaka sidor/skärmar eller appar. Se <a href="../library/get-set/resetstate.md#reference-47fc00ae139042d795d78244d9970139" format="dita" scope="local"> resetState</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Felkorrigeringar och andra ändringar**

* Korrigerade ett fel i VisitorAPI.js v2.2 som förhindrade ID-tjänsten och Target från att fungera tillsammans i Internet Explorer.
* Reviderad kod som förbättrar hur ID-tjänsten skickar data till iFrame för målpublicering. Detta minskar processoranvändningen.

## Version 2.2 {#section-b7dee2495c29470e9b3a3132ec1fd951}

Releasedatum: Juni 2017

<table id="table_7E412383E89D46759B00FE7328C9946F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <a href="../library/function-vars/whitelistdomain.md#reference-999899ff7b5b429a8824c9db7a379808" format="dita" scope="local"> whitelistParentDomain och whitelistIframeDomains </a> </p> </td> 
   <td colname="col2"> <p>Med dessa konfigurationer kan olika instanser av ID-tjänstkod som implementeras i en iFrame och på den överordnade sidan kommunicera med varandra. De är utformade för att lösa problem med två specifika användningsfall där du kan styra den överordnade sidan/domänen eller inte, och där du har ID-tjänstkoden inläst i iFrame för en domän som du har kontroll över. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Dokumentationsuppdateringar för maj {#section-1d36b91bb7a140ce8a145251ffac9f2f}

<table id="table_CD031A716A694E8FA89695C9B614BC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Hjälpavsnitt </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <a href="../faq-intro/faq.md" format="dita" scope="local"> Vanliga frågor och svar </a> </p> </td> 
   <td colname="col2"> <p>Uppdaterade <span class="keyword"> Analyser</span> med information om hur du hittar information om spårningsservern. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Dokumentationsuppdateringar för april {#section-df3e5a85448c4001a6791517520ae06e}

<table id="table_ADC2636240654C69B8B6A45849024540"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Hjälpavsnitt </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <a href="../library/function-vars/subdomain-config.md#reference-8ad017b3e5d24d34b3da25e8f8a56196" format="dita" scope="local"> auditionManagerServer och auditionManagerServerSecure </a> </p> </td> 
   <td colname="col2"> <p>Lagt till länkar till <span class="keyword"> Audience Manager</span> dokumentation som beskriver anrop till <span class="codeph"> demdex.net</span> domän. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <a href="../library/function-vars/subdomain-config.md" format="dita" scope="local"> Förstå ID-synkronisering och matchningsfrekvenser </a> </p> </td> 
   <td colname="col2"> <p>Reviderad <span class="keyword"> Media Optimizer</span> för att beskriva samtalet till <span class="codeph"> cm.eversttech.net</span>. Detta är den automatiska ID-synkronisering som ID-tjänsten utför med <span class="keyword"> Media Optimizer</span>. Den här funktionen släpptes i januari 2017. Se <a href="../release-notes/notes-2017.md#section-0ceac6007c1241b58ad607e2b76b2b7e" format="dita" scope="local"> Version 2.0</a> nedan. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Version 2.1 {#section-5e666dc47c2f4f92999e92697d75799e}

Releasedatum: Februari 2017

**Funktioner**

<table id="table_1F7E1CF091604D22B1D9F3F1AE4DB2D7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> API-egenskap för ID-tjänst, <span class="codeph"> idSyncContainerID</span></p> </td> 
   <td colname="col2"> <p>Den här egenskapen anger behållar-ID som används av <span class="keyword"> Audience Manager</span> för ID-synkronisering. Se <a href="/help/library/function-vars/idsyncontainerid.md" format="https" scope="external"> idSyncContainerID</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID-tjänst-API-metod, <span class="codeph">appendSupplementalDataIDTo()<span class="varname"> URL</span>,<span class="varname"> SDID</span>)</span></p> </td> 
   <td colname="col2"> <p>Den här publika metoden lägger till <span class="wintitle"> Kompletterande data-ID</span> (SDID) som frågesträngsparameter till en omdirigerings-URL. Se <a href="../library/get-set/appendsupplementaldataidto.md#reference-65d09de6fde0418f8c62fa79304a755d" format="dita" scope="local"> appendSupplementalDataIDTo</a>. (MCID-285) </p> </td> 
  </tr> 
 </tbody> 
</table>

**Korrigeringar**

Korrigerade ett fel som gjorde att ID-tjänsten gjorde redundanta serveranrop för ett ID i stället för att använda det ID som lagrats i AMCV-cookien. (MCID-296)

**Ny dokumentation**

[Använda DNS-förhämtning med olika Experience Cloud-lösningar och -tjänster](https://experienceleague.adobe.com/docs/core-services/interface/more-resources/dns-prefetch.html)

## Version 2.0 {#section-0ceac6007c1241b58ad607e2b76b2b7e}

Januari 2017

>[!IMPORTANT]
>
>ID-tjänstkoden v2.0 synkroniserar automatiskt ID:n med Adobe Media Optimizer som standard. Det innebär att du ser ett samtal från sidan till `cm.eversttech.net`, som är ett arv [!DNL Media Optimizer] domänen styrs av [!DNL Adobe]. Se även [Förstå ID-synkronisering och matchningsfrekvenser](../introduction/match-rates.md#concept-e55cf228b90c457fbee8c3cb06b195ab).

**Korrigeringar och förbättringar**

* Korrigerade ett fel som förhindrade AppMeasurement från att göra spårningsanrop till Analytics. (MCID-254, MCID-256, MCID-286)
* Korrigerade ett fel som förhindrade att ID-tjänsten misslyckades direkt om en besökare hade aktiverat en annonsblockerare och den blockeraren konfigurerades för att exkludera domänen demdex.net. Detta är ett sällsynt och ovanligt fel eftersom de flesta annonsblockeringsverktyg inte blockerar domänen demdex.net. (MCID-233)
* Korrigerade ett fel som orsakats av interaktioner mellan ID-tjänstkoden och ett anpassat skript på en kunds webbplats. Det här problemet hindrade Internet Explorer 9 från att läsa in webbsidor. (MCID-206)

## Föregående år {#section-aaabe2b7b0f04641b24acffc11cd7d2e}

Versionsinformation för äldre ID-tjänst.
