---
description: getMarketingCloudVisitorID returnerar besökar-ID:t för Experience Cloud.
keywords: ID Service
seo-description: getMarketingCloudVisitorID returnerar besökar-ID:t för Experience Cloud.
seo-title: getMarketingCloudVisitorID
title: getMarketingCloudVisitorID
uuid: 93e16220-b5b3-4d81-9189-30031bc15129
translation-type: tm+mt
source-git-commit: 4a5fbc971dc950c65e5c8f92dffdfe5dde528b54
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# getMarketingCloudVisitorID{#getmarketingcloudvisitorid}

getMarketingCloudVisitorID returnerar besökar-ID:t för Experience Cloud.

**Syntax:** ` var *`variabelnamn`* = visitor.getMarketingCloudVisitorID()`

Den här metoden används vanligtvis med anpassade lösningar som kräver att besökar-ID läses. Den används inte av en standardimplementering. `getMarketingCloudVisitorID` fungerar även med callback-funktioner för att läsa ID: [!DNL Analytics] n och föra in dem i ditt system eller program.

```js
//callback function 
var useMarketingCloudID = function(id){ 
     //whatever your function does with the Experience Cloud ID 
}; 
 
//get the Experience Cloud ID and pass it to the function 
var mcID = visitor.getMarketingCloudVisitorID(useMarketingCloudID)
```

>[!TIP]
>
>Om du är kund ska du också söka efter och skicka [!DNL Analytics] [!DNL Analytics] ID:t till din funktion. Du vill till exempel att båda identifierarna ska skickas när besökar-ID:t skickas i ett dolt formulärelement till ett program på serversidan som använder API:t för datainfogning. I så fall bör du samla in och returnera [!DNL Experience Cloud] - och [!DNL Analytics] besökar-ID:n. Se [Hämta Analytics-besökar-ID](../../library/get-set/getanalyticsvisitorid.md).

