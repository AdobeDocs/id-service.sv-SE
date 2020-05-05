---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2017.
keywords: ID Service
seo-description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2017.
seo-title: Versionsinformation 2017
title: Versionsinformation 2017
uuid: 79452df0-49db-42b8-96fe-01aa7629fbb5
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# 2017 Release Notes {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2017.

Dessa ändringar registreras också i versionsinformationen [för](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)Experience Cloud.

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
   <td colname="col2"> <p>Detta är ett asynkront API som returnerar identifierare för Analytics, ID-tjänsten, avanmälan av datainsamling, geografisk plats och metadatablockinnehåll som standard. Du kan också styra vilka ID:n du vill returnera med den valfria uppräkningen <span class="codeph"> visitor.FIELDS</span> . Se <a href="../library/get-set/getvisitorvalues.md#reference-b8c9e17c170c4291829a792df46ce279" format="dita" scope="local"> getVisitorValues</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Felkorrigeringar och andra ändringar**

* Korrigerade ett Chrome-relaterat fel som gjorde att ID-tjänsten utlöste ett fel när användaren klickade på bakåtknappen i webbläsaren.
* ID-tjänsten utlöser nu synkronisering igen när region-ID:t i händelsesvaret ändras.
* Lagt till ny dokumentation, [Content Security Policies och Experience Cloud Identity Service](/help/reference/csp.md#concept-968c423a7392479db0a0d821ae9783e3), som förklarar hur du vitlistar anrop till Adobe-domäner som används av ID-tjänsten.

## Version 2.4 {#section-f4d1608dd8894f558a92b82e83321200}

Augusti 2017

<table id="table_D9623D34F4444B038F7835750932C8AA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> isCoopSafe</span> </p> </td> 
   <td colname="col2"> <p>En valfri boolesk konfiguration som avgör om ID-tjänsten skickar (eller inte skickar) data till Adobe Experience Cloud Device Co-op. Se <a href="../library/function-vars/coopsafe.md#reference-7fbed36f38a048d1a5883c53d430ddf4" format="dita" scope="local"> isCoopSafe</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Reviderad dokumentation**

Uppdaterade och reviderade [vanliga frågor](/help/faq-intro/faq-intro.md) och svar som inkluderar olika vanliga frågor och svar för olika [!DNL Experience Cloud] lösningar.

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
   <td colname="col2"> <p>När den läggs till i funktionen <span class="codeph"> Visitor.getInstance</span> kan du med den här konfigurationen åsidosätta standardintervallet för SDID (Supplemental Data ID) när du skickar ID:t från en sida till en annan. Du använder <span class="codeph"> sdidParamExpiry</span> med hjälpfunktionen <span class="codeph"> appendSupplimentalDataTo</span> . Se <a href="../library/function-vars/sdidparamexpiry.md#reference-cef3fd03c43b4772b2422e220b40a458" format="dita" scope="local"> didParamExpiry</a>. </p> </td> 
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
   <th colname="col1" class="entry"> Ämne </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <a href="../faq-intro/faq.md" format="dita" scope="local"> Vanliga frågor </a> </p> </td> 
   <td colname="col2"> <p>Avsnittet <span class="keyword"> Analytics</span> har uppdaterats med information om hur du söker efter serverinformation för spårning. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Dokumentationsuppdateringar för april {#section-df3e5a85448c4001a6791517520ae06e}

<table id="table_ADC2636240654C69B8B6A45849024540"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Ämne </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <a href="../library/function-vars/subdomain-config.md#reference-8ad017b3e5d24d34b3da25e8f8a56196" format="dita" scope="local"> auditionManagerServer och auditionManagerServerSecure </a> </p> </td> 
   <td colname="col2"> <p>Lagt till länkar till <span class="keyword"> Audience Manager</span> -dokumentation som beskriver anrop till domänen <span class="codeph"> demdex.net</span> . </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <a href="../library/function-vars/subdomain-config.md" format="dita" scope="local"> Förstå ID-synkronisering och matchningsfrekvenser </a> </p> </td> 
   <td colname="col2"> <p>Reviderad <span class="keyword"> Media Optimizer</span> -sektion som beskriver anropet till <span class="codeph"> cm.eversttech.net</span>. Detta är den automatiska ID-synkronisering som ID-tjänsten utför med <span class="keyword"> Media Optimizer</span>. Den här funktionen släpptes i januari 2017. Se <a href="../release-notes/notes-2017.md#section-0ceac6007c1241b58ad607e2b76b2b7e" format="dita" scope="local"> version 2.0</a> nedan. </p> </td> 
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
   <td colname="col2"> <p>Den här egenskapen anger det behållar-ID som används av <span class="keyword"> Audience Manager</span> för ID-synkroniseringar. Se <a href="/help/library/function-vars/idsyncontainerid.md" format="https" scope="external"> idSyncContainerID</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID-tjänst-API-metod, <span class="codeph">appendSupplementalDataIDTo(<span class="varname"> URL</span>,<span class="varname"> SDID</span>)</span></p> </td> 
   <td colname="col2"> <p>Den här publika metoden bifogar <span class="wintitle"> SDID</span> (Additional Data ID) som en frågesträngsparameter till en omdirigerings-URL. Se <a href="../library/get-set/appendsupplementaldataidto.md#reference-65d09de6fde0418f8c62fa79304a755d" format="dita" scope="local"> appendSupplementalDataIDTo</a>. (MCID-285) </p> </td> 
  </tr> 
 </tbody> 
</table>

**Korrigeringar**

Korrigerade ett fel som gjorde att ID-tjänsten gjorde redundanta serveranrop för ett ID i stället för att använda det ID som lagrats i AMCV-cookien. (MCID-296)

**Ny dokumentation**

[Använda DNS-förhämtning med olika Experience Cloud-lösningar och -tjänster](https://docs.adobe.com/content/help/en/core-services/interface/more-resources/dns-prefetch.html)

## Version 2.0 {#section-0ceac6007c1241b58ad607e2b76b2b7e}

Januari 2016

>[!IMPORTANT]
>
>ID-tjänstkoden v2.0 synkroniserar automatiskt ID:n med Adobe Media Optimizer som standard. Det innebär att du ser ett samtal från sidan till `cm.eversttech.net`, vilket är en äldre [!DNL Media Optimizer] domän som styrs av [!DNL Adobe]. Se även [Förstå ID-synkronisering och Matchningsfrekvens](../introduction/match-rates.md#concept-e55cf228b90c457fbee8c3cb06b195ab).

**Korrigeringar och förbättringar**

* Korrigerade ett fel som förhindrade AppMeasurement från att göra spårningsanrop till Analytics. (MCID-254, MCID-256, MCID-286)
* Korrigerade ett fel som förhindrade att ID-tjänsten misslyckades direkt om en besökare hade aktiverat en annonsblockerare och den blockeraren konfigurerades för att exkludera domänen demdex.net. Detta är ett sällsynt och ovanligt fel eftersom de flesta annonsblockeringsverktyg inte blockerar domänen demdex.net. (MCID-233)
* Korrigerade ett fel som orsakats av interaktioner mellan ID-tjänstkoden och ett anpassat skript på en kunds webbplats. Det här problemet hindrade Internet Explorer 9 från att läsa in webbsidor. (MCID-206)

## Föregående år {#section-aaabe2b7b0f04641b24acffc11cd7d2e}

Versionsinformation för äldre ID-tjänst.
