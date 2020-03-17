---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2016.
keywords: ID Service
seo-description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2016.
seo-title: Versionsinformation 2016
title: Versionsinformation 2016
uuid: 7a5a314a-3ff8-4561-9c64-6c10d2223887
translation-type: tm+mt
source-git-commit: f7f23d89649a888f5e9d8c94526b550fbda7045b

---


# Versionsinformation 2016 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service för 2016.

Dessa ändringar registreras också i versionsinformationen [för](https://marketing.adobe.com/resources/help/en_US/whatsnew/)Experience Cloud. I [föregående versionsinformation](https://marketing.adobe.com/resources/help/en_US/whatsnew/?f=c_legacy_releases.html) finns äldre [!DNL Experience Cloud] meddelanden.

## Version 1.10 {#section-7d719b3213344a46858835042e0214ed}

November 2016

>[!IMPORTANT]
>
>* Version 1.10 kräver [!UICONTROL AppMeasurement] 1.8.0.
>* Med Experience Cloud Identity Service Library 2.0.0+ börjar ID-synkroniseringen för Adobe Media Optimizer som standard. Se [Förstå ID-synkronisering och Matchningsfrekvens](/help/introduction/match-rates.md).


**Korrigeringar och förbättringar**

* Lagt till instruktioner om hur ID-tjänsten ska implementeras i en serversidesmiljö.
* Dessutom `Visitor.overwriteCrossDomainMCIDAndAID`är det en boolesk funktion som gör att du kan skriva över Experience Cloud- och Analytics-ID:n i andra domäner som du äger. Se [Skriv över besökar-ID](../library/function-vars/overwrite-visitor-id.md#reference-9db13d637ce44fb6a8d519de5743ccde).

* Tidsstämpel har lagts till som en egenskap för `TS = UTC` `visitor.appendVisitorIDsTo`funktionen. ID-tjänsten använder tidsstämpeln för att avgöra om ID:n i omdirigerings-URL:en ska användas baserat på ett 5-minuters åldersintervall. Se [Lägg till besökar-ID-funktion](../library/get-set/appendvisitorid.md#reference-ff167ef19e37433fb08ac2b5a86229ce).

* En ny funktion som returnerar `Visitor.getLocationHint,` ett region-ID har lagts till. Se [Hämta region-ID:n (platstips)](../library/get-set/getlocationhint.md#reference-a761030ff06c4439946bb56febf42d4c).

* Två funktioner har lagts till `idSyncByURL` och `idSyncByDataSource`två som gör att du manuellt kan implementera en ID-synkronisering i iFrame för målpublicering. See [ID Synchronization by URL or Data Source](../library/get-set/idsync.md#reference-b01b88c083434cf8abbeabd3c6956c48).

* Korrigerade ett fel som blockerade AppMeasurement-spårningsanropet om `disableThirdPartyCalls:true`.
* Ett fel som gjorde att ID-tjänsten inte kunde skicka Experience Cloud ID (MID) över olika domäner har korrigerats.

## Version 1.9.0 {#section-04e1b4d4b10d40468f2116b8119998e7}

Oktober 2016

**Korrigeringar och förbättringar**

* Korrigerade ett fel som skickade unika användar-ID:n (AAMUID) för Audience Manager som Experience Cloud-ID:n till ID-tjänsten.
* Om TTL (time-to-live) för en AMCV-cookie har gått ut, returnerar ID-tjänsten den informationen till servern så länge cookien innehåller ett Experience Cloud-ID. Efter det här anropet gör ID-tjänsten ett asynkront anrop för att uppdatera cookien. Detta förbättrar prestandan eftersom ID-tjänsten inte behöver vänta på ett serversvar. Den kan använda befintliga AMCV-cookie-värden och sedan begära en uppdatering.
* ID-tjänsten synkroniserar automatiskt Experience Cloud ID:n (MID:n) med Adobe Media Optimizer och andra interna Adobe-domäner direkt på sidan. Automatisk synkronisering är aktiverat för alla befintliga och nya konton. Detta förbättrar matchningsfrekvensen för Media Optimizer. Gäller VisitorAPI.js version 1.8 eller senare. Se även [Förstå ID-synkronisering och Matchningsfrekvens](../introduction/match-rates.md#concept-e55cf228b90c457fbee8c3cb06b195ab).

**Ny och reviderad dokumentation**

**Nytt:** Hämta region- och användar-ID [från AMCV Cookie](../reference/regions.md#concept-15b2c8c894b846a48f1f61a353cfdf4e)

## Version 1.8.0 {#section-69f2eb5b246b4c7aafe116b7a2a5448a}

September 2016

**Korrigeringar och förbättringar**

Tillagd `disableThirdPartyCalls` som en valfri boolesk flagga som du kan ange i `Visitor.getInstance` funktionen. När `disableThirdPartyCalls= true`detta inträffar kommer ID-tjänsten inte att göra anrop till andra domäner. Som standard `disableThirdPartyCalls= false`. Se [disableThirdPartyCall](../library/function-vars/disablethirdpartycalls.md#reference-fba90b095e9746daad46e3abb790d18b).

## Version 1.7.0 {#section-f7d59104de6644fca3691480383d4644}

Augusti 2016

**Korrigeringar och förbättringar**

* Tillagd `idSyncAttachIframeOnWindowLoad` som en valfri boolesk flagga som du kan ange i `Visitor.getInstance` funktionen. När `idSyncAttachIframeOnWindowLoad= true`ID-tjänsten läser in iFrame för synkronisering av ID vid inläsning av fönster. Som standard läser ID-tjänsten in iFrame så snabbt som möjligt. Den här flaggan *ersätter* `idSyncAttachIframeASAP`, som är inaktuell. Se [Funktionsvariabler](../library/function-vars/function-vars.md)för Visitor.getInstance.

* Lagt till funktioner som stöder spårnings-ID [!DNL Experience Cloud] över domäner, inbyggda appar och hybridappar för webbövergångar. Se [Bifoga hjälpfunktion](../library/get-set/appendvisitorid.md#reference-ff167ef19e37433fb08ac2b5a86229ce)för besökar-ID.

* Funktioner har lagts till i koden visitorAPI.js som avgör om ID-tjänsten har genererat klient- eller serversidan för besökarens [!DNL Experience Cloud] ID eller om ID-anrop tog för lång tid. Se [Funktioner](../library/get-set/timeout-functions.md#reference-912bae0f116540df8c5dc1c008656c23) för timeoutspårning och [Spåra generering](../library/get-set/client-side-id.md#reference-8244dc6d832c4bbaaa97528096bcc2a6)av besökar-ID på klientsidan.

**Ny och reviderad dokumentation**

Revised: [Requirements for the Experience Cloud Identity Service](../reference/requirements.md)

**Kända fel**

Kunder som använder [!DNL Audience Manager] DIL-kod och besökarAPI.js-kod på samma sida bör ange DIL-variabeln `secureDataCollection= false`. Se [secureDataCollection](https://marketing.adobe.com/resources/help/en_US/aam/?f=dil-secure-data-collection.html).

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

* En `d_fieldgroup` parameter har lagts till i ID-synkroniseringsanrop till `dpm.demdex.net`. Den nya parametern används för intern felsökning och felsökning.

* Ett rubrikattribut har lagts till iFrame för ID-tjänsten. Med en iFrame-titel kan skärmläsare ge sidinformation till användare som behöver hjälp med att interagera med onlineinnehåll. iFrame-rubrikattributet är inställt på `Adobe ID Syncing iFrame`.
* Tillagd `idSyncAttachIframeASAP: true` som en valfri flagga som du kan ange i `Visitor.getInstance` funktionen. När `true`ID-tjänsten läser in iFrame för ID-synkronisering så snabbt som möjligt. Detta är avsett att förbättra matchningsfrekvensen för ID-synkronisering. Som standard läser ID-tjänsten in iFrame vid fönsterinläsning. Se [Funktionsvariabler](../library/function-vars/function-vars.md)för Visitor.getInstance.

* Korrigerade ett fel med en callback-funktion som fick AppMeasurement att fastna i en oändlig slinga.
* Ändrade standardintervallet `loadTimeout` till 30 000 millisekunder (från 500 millisekunder). Se [Funktionsvariabler](../library/function-vars/function-vars.md)för Visitor.getInstance.

**Ny och reviderad dokumentation**

**Nytt**

* [Implementera Experience Cloud Identity Service för Analytics](../implementation-guides/setup-analytics.md#concept-9ebbea85cb844a15b557be572cd142fd)
* [Implementera Experience Cloud Identity Service för analyser, Audience Manager och Target](../implementation-guides/setup-aam-analytics-target.md#concept-e7e2dc0d0bbe481db93328b5604b4673)

**Reviderad**

* [Krav för Experience Cloud Identity Service](../reference/requirements.md)
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
   <td colname="col1"> <p>Ändringar i <span class="codeph"> attributet </span> iframe.sandbox </p> </td> 
   <td colname="col2"> <p>iFrame är nu inställt så att <span class="codeph"> iframe.sandbox='allow-scripts allow-same-origin'; </span>. </p> <p>Genom att endast tillåta dessa två tokens blir säkerheten bättre och ID-tjänsten får den grundläggande funktionalitet som krävs för synkronisering av ID. </p> <p>Attributet sandbox stöds inte i Internet Explorer version 9 eller tidigare. Mer information finns i avsnittet Attribut i den här <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe" format="https" scope="external"> iFrame-dokumentationen </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Kodning av Experience Cloud ID (MID) </p> </td> 
   <td colname="col2"> <p>ID-tjänsten kodar det MID-värde som returneras från servern eller när det anges av <span class="codeph"> funktionen visitor.setMarketingCloudVisitorID() </span> . Mer information om MID finns i <a href="../introduction/cookies.md" format="dita" scope="local"> Cookies och Experience Cloud ID </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Korrigeringar**

Besökar-API:t tvingar inte längre till ett extra återsynkroniseringsanrop med Audience Manager när det inte finns något gammalt besökar-ID för Analytics.

## Version 1.5.x {#section-a62ae48275324058b57edf66ee5a579f}

Maj 2016

**Dokumentationsuppdateringar**

* [SDK-krav för Android och iOS](../reference/requirements.md#section-73b2446fba8e463888642c7d7dfd94f1)
* [Data Workbench och Experience Cloud Identity Service](../reference/dwb.md#task-72df50a051944a47b01b0c0bc3d1e1d8)
* [Testa och verifiera Experience Cloud Identity Service](../implementation-guides/test-verify.md)

## Version 1.5.x {#section-0cfeef085cff4cbc8dff6cbc6fc32920}

April, 2016

**Dokumentationsuppdateringar**

[Implementera Experience Cloud Identity Service för Target](../implementation-guides/setup-target.md#concept-9b5a802132574e1181927ddd00e5c5af)

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
   <td colname="col2"> <p>Tjänsten <span class="keyword"> Experience Cloud </span> ID har stöd för begäran om att avanmäla besökare. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> Ändra ID-synkroniseringsintervall </p> </td> 
   <td colname="col2"> <p>Experience <span class="keyword"> Cloud ID- </span> tjänsten gör nu ID-synkroniseringsanrop till alla anrop till datainsamlingsservrarna. Tidigare gjorde ID-tjänsten endast en begäran vid första anropet för att få ett <span class="keyword"> Experience Cloud </span> ID. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Dokumentationsuppdateringar**

* [Implementera identitetstjänsten i Experience Cloud för analyser](../implementation-guides/setup-analytics.md#concept-9ebbea85cb844a15b557be572cd142fd) : Ny procedur som beskriver hur du konfigurerar ID-tjänsten med [!DNL Analytics].

* [Beslutspunkter](../reference/analytics-reference/migration-decisions.md#concept-ba44803eea3c4cc185232a510cec0257) för migrering av identitetstjänsten i Experience Cloud: Reviderad text för tydlighet. Att arbeta med en enda domän innebär att du kan migrera bort från en datainsamling med CNAME om du inte längre vill hantera den. Du behöver dock inte ändra om CNAME fungerar.

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
   <td colname="col1"> <p> <a href="../reference/authenticated-state.md" format="dita" scope="local"> Kund-ID:n och autentiseringstillstånd </a> </p> </td> 
   <td colname="col2"> <p>Reviderad text. Kund-ID:n får endast skickas som icke-kodade värden. Kodnings-ID:n skapar dubbelkodade identifierare. </p> </td> 
  </tr> 
 </tbody> 
</table>
