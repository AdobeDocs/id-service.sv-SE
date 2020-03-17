---
description: Returnerar det eventuella äldre analys-ID som lagrats i s_vi-cookien innan Experience Cloud Identity Service implementerades. Den returnerar en tom sträng om en besökare aldrig har tilldelats ett analys-ID.
keywords: ID Service
seo-description: Returnerar det eventuella äldre analys-ID som lagrats i s_vi-cookien innan Experience Cloud Identity Service implementerades. Den returnerar en tom sträng om en besökare aldrig har tilldelats ett analys-ID.
seo-title: getAnalyticsVisitorID
title: getAnalyticsVisitorID
uuid: 6bb8ddfc-9fc1-4105-b377-d9b4d247a0f8
translation-type: tm+mt
source-git-commit: c4c0b791230422f17292b72fd45ba5689a60adae

---


# getAnalyticsVisitorID{#getanalyticsvisitorid}

Returnerar det eventuella äldre analys-ID som lagrats i s_vi-cookien innan Experience Cloud Identity Service implementerades. Den returnerar en tom sträng om en besökare aldrig har tilldelats ett analys-ID.

**Syntax**`var analyticsID = visitor.getAnalyticsVisitorID()`

Den här funktionen används vanligtvis med anpassade lösningar som kräver att besökar-ID läses. Den används inte av en standardimplementering. `getAnalyticsVisitorID` fungerar även med callback-funktioner för att läsa ID: [!DNL Analytics] n och föra in dem i ditt system eller program.

**Exempelkod**

```js
//callback function 
var useAnalyticsVisitorID = function(id){ 
     //whatever your function does with the Experience Cloud ID 
}; 
 
//get Analytics ID and pass it to the function 
var analyticsID = visitor.getAnalyticsVisitorID(useAnalyticsVisitorID)
```

>[!TIP]
>
>Om du är kund ska du också söka efter och skicka [!DNL Analytics] [!DNL Analytics] ID:t till din funktion. Du vill till exempel att båda identifierarna ska skickas när besökar-ID:t skickas i ett dolt formulärelement till ett program på serversidan som använder API:t för datainfogning. I så fall bör du samla in och returnera [!DNL Experience Cloud] - och [!DNL Analytics] besökar-ID:n. Se [getMarketingCloudVisitorID](../../library/get-set/getmcvid.md).

**Parametern&quot;aid&quot; är ett äldre värde**

Parametern visas i en frågesträng under två olika villkorsuppsättningar. `aid`

**Fall 1**

Parametern visas i en frågesträng när: `aid`

* ID- [!DNL Experience Cloud] tjänsten har distribuerats korrekt.
* Användaren som besöker en webbplats har ett befintligt [!DNL Analytics] ID lagrat i sin [s_vi-cookie](https://marketing.adobe.com/resources/help/en_US/whitepapers/cookies/?f=cookies_analytics.html).

**Fall 2**

Parametern visas i en frågesträng när din organisation använder en `aid` respitperiod [](../../reference/analytics-reference/grace-period.md) innan ID-tjänsten har implementerats fullständigt. Om den användare som besöker webbplatsen är ny och du inte använder någon respitperiod får besökaren parametern `mid` ( [!DNL Experience Cloud] ID).

>[!MORELIKETHIS]
>
>* [Analytics-cookies](https://marketing.adobe.com/resources/help/en_US/whitepapers/cookies/cookies_analytics.html)

