---
description: getMarketingCloudVisitorID returnerar besökar-ID:t för Experience Cloud.
keywords: ID-tjänst
title: getMarketingCloudVisitorID
exl-id: bd81cc0b-0511-492d-beb8-8ba2fe5d4323
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# getMarketingCloudVisitorID{#getmarketingcloudvisitorid}

getMarketingCloudVisitorID returnerar besökar-ID:t för Experience Cloud.

**Syntax:** ` var *`variabelnamn`* = visitor.getMarketingCloudVisitorID()`

Den här metoden används vanligtvis med anpassade lösningar som kräver att besökar-ID läses. Den används inte av en standardimplementering. `getMarketingCloudVisitorID` fungerar även med återanropsfunktioner som ska läsas [!DNL Analytics] ID:n och för in dem till ditt system eller din applikation.

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
>Om du är en [!DNL Analytics] kund, även söka efter och skicka [!DNL Analytics] ID till din funktion. Du vill till exempel att båda identifierarna ska skickas när besökar-ID:t skickas i ett dolt formulärelement till ett program på serversidan som använder API:t för datainfogning. I så fall bör du samla in och returnera [!DNL Experience Cloud] och [!DNL Analytics] besökar-ID. Se [Hämta Analytics-besökar-ID](../../library/get-set/getanalyticsvisitorid.md).
