---
description: Returnerar Experience Cloud Identity Service-regionens ID. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du måste ange region-ID för att kunna göra API-anrop på serversidan till Audience Manager.
keywords: ID Service
seo-description: Returnerar Experience Cloud Identity Service-regionens ID. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du måste ange region-ID för att kunna göra API-anrop på serversidan till Audience Manager.
seo-title: getLocationHint
title: getLocationHint
uuid: cdc312b7-d270-4a5c-a2bb-0fbb37f1e2f4
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# getLocationHint{#getlocationhint}

Returnerar Experience Cloud Identity Service-regionens ID. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du måste ange region-ID för att kunna göra API-anrop på serversidan till Audience Manager.

**Syntax:** ` var *`variabelnamn`* = visitor.getLocationHint()`

En lista med region-ID:n och motsvarande platser finns i [DCS-regions-ID:n, platser och värdnamn](https://docs.adobe.com/content/help/en/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html).

**Exempel på kod**

Funktionen för platstips läser region-ID:t från AMCV-cookien. Om region-ID:t redan har angetts i AMCV-cookien sker återanropet omedelbart. Om region-ID inte anges väntar funktionen på ett svar från servern innan region-ID skickas till återanropet. Koden kan se ut ungefär som i följande exempel.

```js
//callback function 
var callback = function ( 
<i>region ID here</i>){ 
//do whatever your function does with the region ID 
}; 
 
//Get the region ID 
visitor.getLocationHint(callback, true); 
```

