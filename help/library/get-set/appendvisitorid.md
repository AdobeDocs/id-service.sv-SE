---
description: Med den här funktionen kan du dela en besökares Experience Cloud-ID över domäner när webbläsare blockerar cookies från tredje part. Om du vill använda den här funktionen måste du ha implementerat ID-tjänsten och äga käll- och måldomänerna. Finns i VisitorAPI.js version 1.7.0 eller senare.
keywords: ID-tjänst
title: appendVisitorIDsTo (spårning mellan domäner)
exl-id: 3e4f4e2c-e658-4124-bd0e-59c63127bdde
source-git-commit: f185ae10dac686b6986b171aef8a46a574484283
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# appendVisitorIDsTo (spårning mellan domäner){#appendvisitoridsto-cross-domain-tracking}

>[!TIP]
>
>Spårning av domäner fungerar inte som avsett om ECID avvisas från början (eller tidigare). Den kontrollerar inte befintliga ID:n som antingen skickades via URL eller som tidigare fanns i cookien, med tanke på att dessa var ID:n när medgivandet var inställt på&quot;NO&quot;.

Med den här funktionen kan du dela en besökares Experience Cloud-ID över domäner när webbläsare blockerar cookies från tredje part. Om du vill använda den här funktionen måste du ha implementerat ID-tjänsten och äga käll- och måldomänerna. Finns i VisitorAPI.js version 1.7.0 eller senare.

Innehåll:

<ul class="simplelist"> 
 <li> <a href="../../library/get-set/appendvisitorid.md#section-7251d88befd440b4b79520e33c5aa44a" format="dita" scope="local"> Spåra besökare över domäner när webbläsare blockerar cookies från tredje part </a> </li> 
 <li> <a href="../../library/get-set/appendvisitorid.md#section-62d55f7f986542b0b9238e483d50d7b0" format="dita" scope="local"> Lägg till exempel på kod för besökar-ID </a> </li> 
 </a> </li> 
</ul>

<!-- <li> <a href="../../library/get-set/appendvisitorid.md#section-168e313df6054af0a7e27b9fa0d69640" format="dita" scope="local"> Dynamic Tag Management (DTM) and SDK Support -->

## Spåra besökare i olika domäner när webbläsare blockerar cookies från tredje part {#section-7251d88befd440b4b79520e33c5aa44a}

ID-tjänsten skriver en cookie från första och tredje part till webbläsaren när en person besöker din webbplats (se [Cookies och Experience Cloud Identity Service](../../introduction/cookies.md) ). Den första partens cookie innehåller MID, ett unikt ID för den besökaren. Cookien från tredje part innehåller ett annat ID som används av ID-tjänsten för att generera MID. När en webbläsare blockerar denna cookie från tredje part kan ID-tjänsten inte:

* Generera om det unika ID:t för besökaren när de navigerar till en annan domän.
* Spåra besökare i olika domäner som ägs av organisationen.

Implementera ` Visitor.appendVisitorIDsTo( *`url`*)` om du vill ha hjälp med att lösa det här problemet. Med den här egenskapen kan ID-tjänsten spåra webbplatsbesökare i flera domäner även när deras webbläsare blockerar cookies från tredje part. Så här fungerar det:

* När en besökare bläddrar till dina andra domäner lägger ` Visitor.appendVisitorIDsTo( *`url`*)` till MID som en frågeparameter i URL-omdirigeringen från den ursprungliga domänen till måldomänen.
* ID-tjänstkoden på måldomänen extraherar MID från URL:en i stället för att skicka en begäran till Adobe för besökarens ID. Denna begäran innehåller cookie-ID från tredje part, som inte är tillgängligt i det här fallet.
* ID-tjänstkoden på målsidan använder det MID som skickades för att spåra besökaren.

Mer information finns i kodexemplet.

## Lägg till exempel på besökar-ID-kod {#section-62d55f7f986542b0b9238e483d50d7b0}

Följande exempelkod kan hjälpa dig att komma igång med funktionen `appendVisitorIDsTo`:

>[!TIP]
>
>Den här koden kan placeras i den anpassade kodredigeraren som är en del av Adobe Analytics-tillägget eller högst upp i [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=sv-SE).

```js
var adbeDomains = ["marketo.com", "figma.com", "workfront.com"];
var visitor = Visitor.getInstance("9E1005A551ED61CA0A490D45@AdobeOrg", {
  trackingServer: "sstats.adobe.com",
  trackingServerSecure: "sstats.adobe.com",
  marketingCloudServer: "sstats.adobe.com",
  marketingCloudServerSecure: "sstats.adobe.com"
});
adbeDomains.forEach(function(domain) {
  var domainRegex = RegExp(domain);
  if (!domainRegex.test(location.hostname)) {
    hrefSelector = '[href*="' + domain + '"]';
    document.querySelectorAll(hrefSelector).forEach(function(href) {
      href.addEventListener('mousedown', function(event) {
        var destinationURLWithVisitorIDs = visitor.appendVisitorIDsTo(event.currentTarget.href)
        event.currentTarget.href = destinationURLWithVisitorIDs.replace(/MCAID%3D.*%7CMCORGID/, 'MCAID%3D%7CMCORGID');
      });
    });
  }
});
```

<!-- >[!IMPORTANT]
>
>In order for the values passed in the URL via appendVisitorsIDsTo to be picked up, the [ovewriteCrossDomainMCIDAndAID](../function-vars/overwrite-visitor-id.md) variable must be set to true.

The following example can help you get started with ` Visitor.appendVisitorIDsTo( *`url`*)`. When implemented properly, your JavaScript code could look similar to the following example.

```js
//Code on Domain A 
var destinationURL = "www.destination.com"; 
 
//Call the ID service 
var visitor = Visitor.getInstance(...); 
 
//Append visitor IDs to the destination URL 
var destinationURLWithVisitorIDs = visitor.appendVisitorIDsTo(destinationURL); 
     //Result of appendVisitorIDsTo includes destination URL, Experience Cloud ID (MCMID), and Analytics ID (MCAID) 
     "www.destination.com?adobe_mc=MCMID=1234|MCAID=5678"
//Redirect to the destination
``` -->

<!-- ## Dynamic Tag Management (DTM) and SDK Support {#section-168e313df6054af0a7e27b9fa0d69640}

<table id="table_6E7152B4FD2B4C4D8C9477C68204C4FF"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Support for </th> 
   <th colname="col2" class="entry"> See </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>DTM</b> </p> </td> 
   <td colname="col2"> <p> <a href="https://helpx.adobe.com/dtm/kb/how-to-set-marketing-cloud-id-service-helper-function-in-adobe-d.html" format="https" scope="external"> Set the appendVisitorIDTo Function in DTM </a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>SDK</b> </p> </td> 
   <td colname="col2"> 
    <ul id="ul_9D7933FF68EE4C71BAE999B3747F8398"> 
     <li id="li_9036C76AAECC4E639C23020C0C9F2AF8"> <a href="https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/mc-methods.html?lang=sv-SE" format="https" scope="external"> Android ID Service Methods </a> </li> 
     <li id="li_E49D357905584674BFDFE348345B3849"> <a href="https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/mc-methods.html?lang=sv-SE" format="https" scope="external"> iOS ID Service Methods </a> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table> -->
