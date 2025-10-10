---
description: Med den här konfigurationen kan du åsidosätta standardintervallet för SDID (Supplemental Data ID) när du skickar det ID:t från en sida till en annan med hjälp av hjälpfunktionen appendSupplementalDataIDTo. Som standard har ID-tjänstkoden på den mottagande sidan 30 sekunder på sig att hämta SDID från den URL som skickas av den refererande sidan. Om ID-tjänstkoden på den mottagande sidan inte kan hämta SDID på mindre än 30 sekunder begär den ett nytt SDID. Den här funktionen är främst avsedd för A4T-kunder som behöver skicka SDID från en sida till en annan och vill ha kontroll över tidsgränsen.
keywords: ID-tjänst
title: sdidParamExpiry
exl-id: 5458ffa5-03d1-4c52-907d-c50fe00ce35d
source-git-commit: 7ef084bc1add5a4ea8c7be738055b0c21e247eea
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# sdidParamExpiry{#sdidparamexpiry}

Med den här konfigurationen kan du åsidosätta standardintervallet för SDID (Supplemental Data ID) när du skickar det ID:t från en sida till en annan med hjälp av hjälpfunktionen appendSupplementalDataIDTo. Som standard har ID-tjänstkoden på den mottagande sidan 30 sekunder på sig att hämta SDID från den URL som skickas av den refererande sidan. Om ID-tjänstkoden på den mottagande sidan inte kan hämta SDID på mindre än 30 sekunder begär den ett nytt SDID. Den här funktionen är främst avsedd för A4T-kunder som behöver skicka SDID från en sida till en annan och vill ha kontroll över tidsgränsen.

**Åsidosätt SDID-timeout**

Om du behöver ändra SDID-standardtidsgränsen lägger du till `sdidParamExpiry` i funktionen `Visitor.getInstance` med följande syntax:

**Syntax:** `sdidParamExpiry: *`tid i sekunder`*`

**Kodexempel**

När den är konfigurerad kan ID-tjänstkoden se ut ungefär som i det här exemplet. I det här exemplet anges SDID-tidsgränsen till 15 sekunder. Den här konfigurationen fungerar med hjälpmetoden [appendSupplementalDataIDTo](../../library/get-set/appendsupplementaldataidto.md#reference-65d09de6fde0418f8c62fa79304a755d).

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   ... 
   //Change the default SDID timeout to 15 seconds 
   sdidParamExpiry: 15 
}); 
 
//Call helper method to append SDID to the Page B URL from Page A 
var pageB = "www.domain.com/pageB"; 
var pageBWithSdid = visitor.appendSupplementalDataIDTo(pageB, "67987653465787219"); 
```
