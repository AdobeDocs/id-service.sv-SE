---
description: Returnerar region-ID för Experience Cloud Identity Service. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du behöver region-ID för att kunna göra API-anrop på serversidan till Audience Manager.
keywords: ID Service
seo-description: Returnerar region-ID för Experience Cloud Identity Service. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du behöver region-ID för att kunna göra API-anrop på serversidan till Audience Manager.
seo-title: getLocationHint
title: getLocationHint
uuid: cdc312b7-d270-4a5c-a2bb-0fbb37f1e2f4
translation-type: tm+mt
source-git-commit: e6d65f1bfed187d7440512e8f3c2de0550506c95

---


# getLocationHint{#getlocationhint}

Returnerar region-ID för Experience Cloud Identity Service. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du behöver region-ID för att kunna göra API-anrop på serversidan till Audience Manager.

**Syntax:** ` var *`variabelnamn`* = visitor.getLocationHint()`

En lista med region-ID:n och motsvarande platser finns i [DCS-regions-ID:n, platser och värdnamn](https://marketing.adobe.com/resources/help/en_US/aam/dcs-regions.html).

**Kodexempel**

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

