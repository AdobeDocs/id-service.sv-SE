---
description: Returnerar Experience Cloud Identity Service-regionens ID. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du behöver region-ID för att kunna göra serversides-API-anrop till Audience Manager.
keywords: ID-tjänst
title: getLocationHint
exl-id: 0213f828-a985-4201-8a38-0a4b170ed057
source-git-commit: 7ef084bc1add5a4ea8c7be738055b0c21e247eea
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# getLocationHint{#getlocationhint}

Returnerar Experience Cloud Identity Service-regionens ID. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du behöver region-ID för att kunna göra serversides-API-anrop till Audience Manager.

**Syntax:** `var *`variabelnamn`* = visitor.getLocationHint()`

En lista över region-ID:n och motsvarande platser finns i [DCS-region-ID:n, platser och värdnamn](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html).

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
