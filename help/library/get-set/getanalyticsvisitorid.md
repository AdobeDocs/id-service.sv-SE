---
description: Returnerar det eventuella gamla analys-ID:t som sparades i s_vi-cookien innan Experience Cloud Identity Service implementerades. Den returnerar en tom sträng om en besökare aldrig har tilldelats ett analys-ID.
keywords: ID-tjänst
title: getAnalyticsVisitorID
exl-id: 82973de4-4257-4aab-9268-4ab124a01ee2
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# getAnalyticsVisitorID{#getanalyticsvisitorid}

Returnerar det eventuella gamla analys-ID:t som sparades i s_vi-cookien innan Experience Cloud Identity Service implementerades. Den returnerar en tom sträng om en besökare aldrig har tilldelats ett analys-ID.

**Syntax** `var analyticsID = visitor.getAnalyticsVisitorID()`

Den här funktionen används vanligtvis med anpassade lösningar som kräver att besökar-ID läses. Den används inte av en standardimplementering. `getAnalyticsVisitorID` fungerar även med callback-funktioner för att läsa  [!DNL Analytics] ID:n och föra in dem i ditt system eller program.

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
>Om du är [!DNL Analytics]-kund söker du efter och skickar även [!DNL Analytics]-ID:t till din funktion. Du vill till exempel att båda identifierarna ska skickas när besökar-ID:t skickas i ett dolt formulärelement till ett program på serversidan som använder API:t för datainfogning. I det här fallet bör du samla in och returnera besökar-ID:n för [!DNL Experience Cloud] och [!DNL Analytics]. Se [getMarketingCloudVisitorID](../../library/get-set/getmcvid.md).

**Parametern&quot;aid&quot; är ett äldre värde**

Parametern `aid` visas i en frågesträng under två olika villkorsuppsättningar.

**Fall 1**

Du ser parametern `aid` i en frågesträng när:

* ID-tjänsten [!DNL Experience Cloud] har distribuerats korrekt.
* Användaren som besöker en webbplats har ett befintligt [!DNL Analytics]-ID i sin [s_vi-cookie](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-analytics.html#section-5d50a078de444d12b7d927d68ff3b679).

**Fall 2**

Parametern `aid` visas i en frågesträng när din organisation använder en [respitperiod](../../reference/analytics-reference/grace-period.md) innan ID-tjänsten har implementerats fullständigt. Om användaren som besöker webbplatsen är ny och du inte använder någon respitperiod, får besökaren parametern `mid` ( [!DNL Experience Cloud] ID).

>[!MORELIKETHIS]
>
>* [Analytics-cookies](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-privacy.html)

