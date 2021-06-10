---
description: Returnerar Experience Cloud Identity Service-regionens ID. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du måste ange region-ID för att kunna göra API-anrop på serversidan till Audience Manager.
keywords: ID-tjänst
title: getLocationHint
exl-id: 0213f828-a985-4201-8a38-0a4b170ed057
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# getLocationHint{#getlocationhint}

Returnerar Experience Cloud Identity Service-regionens ID. Ett region-ID (eller platstips) är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Du måste ange region-ID för att kunna göra API-anrop på serversidan till Audience Manager.

**Syntax:** ` var *`variabelnamn`* = visitor.getLocationHint()`

En lista över region-ID:n och motsvarande platser finns i [DCS Region-ID:n, platser och värdnamn](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html).

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
