---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2016.
keywords: ID-tjänst
title: Versionsinformation 2016
feature-set: Experience Cloud Services
feature: TK421
exl-id: f96b9869-6282-4090-b392-797608e25a51
source-git-commit: d027f7fca8cf62d6b5d80ec3c37049ddd1afdd70
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 1%

---

# Versionsinformation 2016 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2016.

Dessa ändringar registreras också i versionsinformationen [Experience Cloud](https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html?lang=sv).

## Version 1.10 {#section-7d719b3213344a46858835042e0214ed}

November 2016

>[!IMPORTANT]
>
>* Version 1.10 kräver [!UICONTROL AppMeasurement] 1.8.0.
>* Med Experience Cloud Identity Service Library 2.0.0+ startar ID-synkroniseringen för Adobe Media Optimizer som standard. Se [Förstå ID-synkronisering och matchningsfrekvenser](/help/introduction/match-rates.md).

**Korrigeringar och förbättringar**

* Lagt till instruktioner om hur ID-tjänsten ska implementeras i en serversidesmiljö.
* `Visitor.overwriteCrossDomainMCIDAndAID` har lagts till, en boolesk funktion som gör att du kan skriva över Experience Cloud och analys-ID:n i andra domäner som du äger. Se [Skriv över besökar-ID](../library/function-vars/overwrite-visitor-id.md#reference-9db13d637ce44fb6a8d519de5743ccde).

* `TS = UTC`-tidsstämpeln har lagts till som en egenskap för funktionen `visitor.appendVisitorIDsTo`. ID-tjänsten använder tidsstämpeln för att avgöra om ID:n i omdirigerings-URL:en ska användas baserat på ett 5-minuters åldersintervall. Se [Lägg till besökar-ID-funktion](../library/get-set/appendvisitorid.md#reference-ff167ef19e37433fb08ac2b5a86229ce).

* `Visitor.getLocationHint,` har lagts till en ny funktion som returnerar ett region-ID. Se [Hämta region-ID (platstips)](../library/get-set/getlocationhint.md#reference-a761030ff06c4439946bb56febf42d4c).

* `idSyncByURL` och `idSyncByDataSource`, två funktioner har lagts till som gör att du manuellt kan implementera en ID-synkronisering i iFrame för målpublicering. Se [ID-synkronisering via URL eller Data Source](../library/get-set/idsync.md#reference-b01b88c083434cf8abbeabd3c6956c48).

* Korrigerade ett fel som blockerade anropet för spårning av AppMeasurement om `disableThirdPartyCalls:true`.
* Ett fel som gjorde att ID-tjänsten inte kunde skicka Experience Cloud-ID (MID) över olika domäner har korrigerats.

## Version 1.9.0 {#section-04e1b4d4b10d40468f2116b8119998e7}

Oktober 2016

**Korrigeringar och förbättringar**

* Korrigerade ett fel som skickade unika användar-ID:n (AAMUID) i Audience Manager som Experience Cloud ID:n till ID-tjänsten.
* Om TTL (time-to-live) för en AMCV-cookie har gått ut, returnerar ID-tjänsten den informationen till servern så länge som cookien innehåller ett Experience Cloud-ID. Efter det här anropet gör ID-tjänsten ett asynkront anrop för att uppdatera cookien. Detta förbättrar prestandan eftersom ID-tjänsten inte behöver vänta på ett serversvar. Den kan använda befintliga AMCV-cookie-värden och sedan begära en uppdatering.
* ID-tjänsten synkroniserar automatiskt Experience Cloud ID:n (MID) med Adobe Media Optimizer och andra interna Adobe-domäner direkt på sidan. Automatisk synkronisering är aktiverat för alla befintliga och nya konton. Detta förbättrar matchningsfrekvensen för Media Optimizer. Gäller VisitorAPI.js version 1.8 eller senare. Se även [Om ID-synkronisering och matchningsfrekvenser](../introduction/match-rates.md#concept-e55cf228b90c457fbee8c3cb06b195ab).

**Ny och reviderad dokumentation**

**Nytt:** [Hämta region- och användar-ID från AMCV-cookien](../reference/regions.md#concept-15b2c8c894b846a48f1f61a353cfdf4e)

## Version 1.8.0 {#section-69f2eb5b246b4c7aafe116b7a2a5448a}

September 2016

**Korrigeringar och förbättringar**

`disableThirdPartyCalls` har lagts till som en valfri boolesk flagga som du kan ange i funktionen `Visitor.getInstance`. När `disableThirdPartyCalls= true` anropas inte andra domäner av ID-tjänsten. Som standard `disableThirdPartyCalls= false`. Se [disableThirdPartyCall](../library/function-vars/disablethirdpartycalls.md#reference-fba90b095e9746daad46e3abb790d18b).

## Version 1.7.0 {#section-f7d59104de6644fca3691480383d4644}

Augusti 2016

**Korrigeringar och förbättringar**

* `idSyncAttachIframeOnWindowLoad` har lagts till som en valfri boolesk flagga som du kan ange i funktionen `Visitor.getInstance`. När `idSyncAttachIframeOnWindowLoad= true` läses ID-tjänsten in iFrame för synkronisering av ID vid inläsning av fönster. Som standard läser ID-tjänsten in iFrame så snabbt som möjligt. Den här flaggan *ersätter* `idSyncAttachIframeASAP`, som är inaktuell. Se [Funktionsvariabler för Visitor.getInstance](../library/function-vars/function-vars.md).

* Funktioner som stöder spårning av [!DNL Experience Cloud]-ID:n i domäner, inbyggda appar och hybridappar har lagts till i webbövergångar. Se [Bifoga hjälpfunktion för besökar-ID](../library/get-set/appendvisitorid.md#reference-ff167ef19e37433fb08ac2b5a86229ce).

* Funktioner har lagts till i koden visitorAPI.js som avgör om ID-tjänsten har genererat besökarens [!DNL Experience Cloud]-ID på klient- eller serversidan eller om ID-anrop tog för lång tid. Se [Funktioner för uppföljning av timeout ](../library/get-set/timeout-functions.md#reference-912bae0f116540df8c5dc1c008656c23) och [Spåra generering av besökar-ID på klientsidan](../library/get-set/client-side-id.md#reference-8244dc6d832c4bbaaa97528096bcc2a6).

**Ny och reviderad dokumentation**

Reviderad: [Krav för identitetstjänsten Experience Cloud](../reference/requirements.md)

**Kända fel**

Kunder som använder [!DNL Audience Manager] DIL-kod och besökarAPI.js-kod på samma sida bör ange variabeln `secureDataCollection= false` för DIL. Se [secureDataCollection](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html).

## Version 1.6.0 {#section-3faaa14bf3934c6a99b8f79ee06fc0d2}

Juli 2016

>[!IMPORTANT]
>
>Version 1.6.0 av [!DNL Experience Cloud] ID-tjänsten *kräver* AppMeasurement för JavaScript version 1.6.2. Om du uppgraderar till ID-tjänstversion 1.6.0 måste du kontrollera att du använder rätt AppMeasurement-kodversion.

<table id="table_5472AAFA0DD2495DB8D92DEBE44A07A9"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Cross-Origin Resource Sharing (CORS) </p> </td> 
   <td colname="col2"> <p>CORS tillåter webbläsare att begära resurser från en annan domän än den aktuella domänen. Experience Cloud Identity Service stöder CORS-standarder för att möjliggöra resursbegäranden på klientsidan, från olika källor. ID-tjänsten återgår till JSONP-begäranden i webbläsare som inte stöder CORS. </p> <p>Se: </p> 
    <ul id="ul_15386385108F4E07824041DD6F2DC11E"> 
     <li id="li_DB8D5AA4A7004DE4AE9CBC31A389F5BD"> <a href="../reference/cors.md#concept-6c280446990d46d88ba9da15d2dcc758" format="dita" scope="local"> CORS-stöd i Experience Cloud Identity Service </a> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Korrigeringar och förbättringar**

* En `d_fieldgroup`-parameter har lagts till i ID-synkroniseringsanrop till `dpm.demdex.net`. Den nya parametern används för intern felsökning och felsökning.

* Ett rubrikattribut har lagts till iFrame för ID-tjänsten. Med en iFrame-titel kan skärmläsare ge sidinformation till användare som behöver hjälp med att interagera med onlineinnehåll. iFrame-rubrikattributet är inställt på `Adobe ID Syncing iFrame`.
* `idSyncAttachIframeASAP: true` har lagts till som en valfri flagga som du kan ange i funktionen `Visitor.getInstance`. När `true` läses ID-tjänsten in så snabbt som möjligt för iFrame för ID-synkronisering. Detta är avsett att förbättra matchningsfrekvensen för ID-synkronisering. Som standard läser ID-tjänsten in iFrame vid fönsterinläsning. Se [Funktionsvariabler för Visitor.getInstance](../library/function-vars/function-vars.md).

* Korrigerade ett fel med en callback-funktion som gjorde att AppMeasurementet fastnade i en oändlig slinga.
* Standardintervallet `loadTimeout` har ändrats till 30 000 millisekunder (från 500 millisekunder). Se [Funktionsvariabler för Visitor.getInstance](../library/function-vars/function-vars.md).

**Ny och reviderad dokumentation**

**Nytt**

* [Implementera identitetstjänsten Experience Cloud för analyser](../implementation-guides/setup-analytics.md#concept-9ebbea85cb844a15b557be572cd142fd)
* [Implementera identitetstjänsten Experience Cloud för Analytics, Audience Manager och Target](../implementation-guides/setup-aam-analytics-target.md#concept-e7e2dc0d0bbe481db93328b5604b4673)

**Reviderad**

* [Krav för identitetstjänsten Experience Cloud](../reference/requirements.md)
* [Testa och verifiera Experience Cloud Identity Service](../implementation-guides/test-verify.md)

## Version 1.5.7 {#section-735b4989a5744a42aeb2d97602dbda62}

Juni 2016

<table id="table_5D604D0820C84EC996ACB99126C8A3DF"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Ändringar av attributet <span class="codeph"> iframe.sandbox </span> </p> </td> 
   <td colname="col2"> <p>iFrame är nu inställt så att <span class="codeph"> iframe.sandbox='allow-scripts allow-same-origin'; </span>. </p> <p>Genom att endast tillåta dessa två tokens blir säkerheten bättre och ID-tjänsten får den grundläggande funktionalitet som krävs för synkronisering av ID. </p> <p>Attributet sandbox stöds inte i Internet Explorer version 9 eller tidigare. Mer information finns i avsnittet Attribut i den här <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe" format="https" scope="external"> iFrame-dokumentationen </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Kodning av Experience Cloud-ID (MID) </p> </td> 
   <td colname="col2"> <p>ID-tjänsten kodar det MID-värde som returneras från servern eller när det anges av funktionen <span class="codeph"> visitor.setMarketingCloudVisitorID() </span> . Mer information om MID finns i <a href="../introduction/cookies.md" format="dita" scope="local"> Cookies och Experience Cloud ID </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Korrigeringar**

Besökar-API:t tvingar inte längre till ett extra återsynkroniseringsanrop med Audience Manager när det inte finns något gammalt besökar-ID för Analytics.

## Version 1.5.x {#section-a62ae48275324058b57edf66ee5a579f}

Maj 2016

**Dokumentationsuppdateringar**

* [SDK-krav för Android och iOS](../reference/requirements.md#section-73b2446fba8e463888642c7d7dfd94f1)
* [Data Workbench och identitetstjänsten Experience Cloud](../reference/dwb.md#task-72df50a051944a47b01b0c0bc3d1e1d8)
* [Testa och verifiera Experience Cloud Identity Service](../implementation-guides/test-verify.md)

## Version 1.5.x {#section-0cfeef085cff4cbc8dff6cbc6fc32920}

April, 2016

**Dokumentationsuppdateringar**

[Implementera identitetstjänsten Experience Cloud för Target](../implementation-guides/setup-target.md#concept-9b5a802132574e1181927ddd00e5c5af)

## Version 1.5.4 {#section-1a44ba147fb3440ea7dec551faee3528}

Mars 2016

<table id="table_F4ED1F88709E4D3BA69C747879A4E18F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Funktion </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Stöd för avanmälan </p> </td> 
   <td colname="col2"> <p>ID-tjänsten <span class="keyword"> Experience Cloud </span> stöder avanmälningsbegäranden för besökare. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> Ändra ID-synkroniseringsintervall </p> </td> 
   <td colname="col2"> <p>Tjänsten <span class="keyword"> Experience Cloud ID </span> gör nu ID-synkroniseringsanrop på alla anrop till datainsamlingsservrarna. Tidigare gjorde ID-tjänsten endast en begäran vid det första anropet för att hämta ett <span class="keyword"> Experience Cloud </span>-ID. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Dokumentationsuppdateringar**

* [Implementera identitetstjänsten för Analytics](../implementation-guides/setup-analytics.md#concept-9ebbea85cb844a15b557be572cd142fd): Ny procedur som beskriver hur du konfigurerar ID-tjänsten med [!DNL Analytics].

* [Beslutspunkter för migrering av identitetstjänst för Experience Cloud ](../reference/analytics-reference/migration-decisions.md#concept-ba44803eea3c4cc185232a510cec0257) : Reviderad text för tydlighet. Att arbeta med en enda domän innebär att du kan migrera bort från en datainsamling med CNAME om du inte längre vill hantera den. Du behöver dock inte ändra om CNAME fungerar.

## Version 1.5.3 {#section-7c09ba2832bd4644a1ccc3aa83abe66a}

Januari 2016

**Dokumentationsuppdateringar**

<table id="table_C1A5DBED6B104C0FBA54EC663D3B0E86"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Ämne </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <a href="../reference/authenticated-state.md" format="dita" scope="local"> Kund-ID och autentiseringstillstånd </a> </p> </td> 
   <td colname="col2"> <p>Reviderad text. Kund-ID:n får endast skickas som icke-kodade värden. Kodnings-ID:n skapar dubbelkodade identifierare. </p> </td> 
  </tr> 
 </tbody> 
</table>
