---
description: Med den här konfigurationen kan du åsidosätta standardintervallet för SDID (Supplemental Data ID) när du skickar det ID:t från en sida till en annan med hjälp av hjälpfunktionen appendSupplementalDataIDTo. Som standard har ID-tjänstkoden på den mottagande sidan 30 sekunder på sig att hämta SDID från den URL som skickas av den refererande sidan. Om ID-tjänstkoden på den mottagande sidan inte kan hämta SDID på mindre än 30 sekunder begär den ett nytt SDID. Den här funktionen är främst avsedd för A4T-kunder som behöver skicka SDID från en sida till en annan och vill ha kontroll över tidsgränsen.
keywords: ID Service
seo-description: Med den här konfigurationen kan du åsidosätta standardintervallet för SDID (Supplemental Data ID) när du skickar det ID:t från en sida till en annan med hjälp av hjälpfunktionen appendSupplementalDataIDTo. Som standard har ID-tjänstkoden på den mottagande sidan 30 sekunder på sig att hämta SDID från den URL som skickas av den refererande sidan. Om ID-tjänstkoden på den mottagande sidan inte kan hämta SDID på mindre än 30 sekunder begär den ett nytt SDID. Den här funktionen är främst avsedd för A4T-kunder som behöver skicka SDID från en sida till en annan och vill ha kontroll över tidsgränsen.
seo-title: sdidParamExpiry
title: sdidParamExpiry
uuid: cdaf7e2d-b196-4c70-936d-8a98191cbb85
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# sdidParamExpiry{#sdidparamexpiry}

Med den här konfigurationen kan du åsidosätta standardintervallet för SDID (Supplemental Data ID) när du skickar det ID:t från en sida till en annan med hjälp av hjälpfunktionen appendSupplementalDataIDTo. Som standard har ID-tjänstkoden på den mottagande sidan 30 sekunder på sig att hämta SDID från den URL som skickas av den refererande sidan. Om ID-tjänstkoden på den mottagande sidan inte kan hämta SDID på mindre än 30 sekunder begär den ett nytt SDID. Den här funktionen är främst avsedd för A4T-kunder som behöver skicka SDID från en sida till en annan och vill ha kontroll över tidsgränsen.

**Åsidosätt SDID-timeout**

Om du behöver ändra SDID-standardtidsgränsen lägger du till `sdidParamExpiry` i `Visitor.getInstance` funktionen med följande syntax:

**Syntax:** ` sdidParamExpiry: *`tid i sekunder`*`

**Exempel på kod**

När den är konfigurerad kan ID-tjänstkoden se ut ungefär som i det här exemplet. I det här exemplet anges SDID-tidsgränsen till 15 sekunder. Den här konfigurationen fungerar med hjälpmetoden [appendSupplementalDataIDTo](../../library/get-set/appendsupplementaldataidto.md#reference-65d09de6fde0418f8c62fa79304a755d) .

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

