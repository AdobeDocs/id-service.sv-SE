---
description: Med den här hjälpmetoden kan du lägga till ett SDID (Supplemental Data ID) som en frågesträngsparameter i en omdirigerings-URL. Detta är användbart när du använder A4T och du måste behålla SDID från en sida till en annan och sammanfoga de olika besöken. Om du vill använda den här funktionen måste du ha implementerat ID-tjänsten med samma organisations-ID på käll- och måldomänerna.
keywords: ID-tjänst
title: appendSupplementalDataIDTo
exl-id: 7f0e7fca-4551-4165-a12b-c7e5514d6818
source-git-commit: 5710539b45a81394061cd4af2ef3edc27b49092e
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# appendSupplementalDataIDTo{#appendsupplementaldataidto}

Med den här hjälpmetoden kan du lägga till ett SDID (Supplemental Data ID) som en frågesträngsparameter i en omdirigerings-URL. Detta är användbart när du använder A4T och du måste behålla SDID från en sida till en annan och sammanfoga de olika besöken. Om du vill använda den här funktionen måste du ha implementerat ID-tjänsten med samma organisations-ID på käll- och måldomänerna.

Innehåll:

<ul class="simplelist"> 
 <li> <a href="../../library/get-set/appendsupplementaldataidto.md#section-cbb0b2f73bcc418386796c24c01b2365" format="dita" scope="local"> Exempel på syntax och kod </a> </li> 
 <li> <a href="../../library/get-set/appendsupplementaldataidto.md#section-dbe02d7ff6bd4ad1a2a26bf9cff54fa4" format="dita" scope="local"> provutdata </a> </li> 
 <li> <a href="../../library/get-set/appendsupplementaldataidto.md#section-cbb0b2f73bcc418386796c24c01b2365" format="dita" scope="local"> Exempel på syntax och kod </a> </li> 
 <li> <a href="../../library/get-set/appendsupplementaldataidto.md#section-99946715cefa4acc95200b093db5297e" format="dita" scope="local"> Ändrar SDID-timeout med sdidParamExpiry </a> </li> 
</ul>

## Exempel på syntax och kod {#section-cbb0b2f73bcc418386796c24c01b2365}

**Syntax:** ` appendSupplementalDataIDTo( *`URL`*, *`SDID`*)`

**Kodexempel**

```js
var visitor = Visitor.getInstance("Insert Experience Cloud organization ID here"); 

//Get current supplemental data id
var theCurrentSDID = visitor._supplementalDataIDCurrent ? visitor._supplementalDataIDCurrent : "";

//Call helper method to append SDID to the Page B URL from Page A 
var pageB = "www.domain.com/pageB"; 
var pageBWithSdid = visitor.appendSupplementalDataIDTo(pageB, theCurrentSDID));
```

## Exempelutdata {#section-dbe02d7ff6bd4ad1a2a26bf9cff54fa4}

Som framgår nedan innehåller URL-omdirigeringen besökarens SDID, ditt organisations-ID och en UNIX-tidsstämpel i anropet till den mottagande sidan.

<ul class="simplelist"> 
 <li> <span class="codeph"> www.domain.com/pageB?adobe_mc_sdid=SDID=7996F0B028999505-13DA591039D6226|MCORGID=123456789@AdobeOrg|TS=1498569322 </span> </li> 
</ul>

## Ändra SDID-timeout med sdidParamExpiry {#section-99946715cefa4acc95200b093db5297e}

Med konfigurationen [sdidParamExpiry](../../library/function-vars/sdidparamexpiry.md#reference-cef3fd03c43b4772b2422e220b40a458) kan du ändra standardintervallet för SDID-förfallodatum när du skickar ID:t från en sida till en annan med hjälp av hjälpfunktionen `appendSupplementalDataIDTo`. Som standard har ID-tjänstkoden på den mottagande sidan 30 sekunder på sig att hämta SDID från den URL som skickas av den refererande sidan. Om ID-tjänstkoden på den mottagande sidan inte kan hämta SDID på mindre än 30 sekunder begär den ett nytt SDID. Den här funktionen är främst avsedd för A4T-kunder som behöver skicka SDID från en sida till en annan och vill ha kontroll över tidsgränsen.

Om du behöver ändra SDID-standardtidsgränsen lägger du till `sdidParamExpiry` i funktionen `Visitor.getInstance` med följande syntax:

**Syntax:** ` sdidParamExpiry: *`tid i sekunder`*`

**Kodexempel**

När din ID-tjänstkod är konfigurerad kan den se ut ungefär som detta exempel. I det här exemplet anges SDID-tidsgränsen till 15 sekunder.

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   ... 
   //Change the default SDID timeout to 15 seconds 
   sdidParamExpiry: 15 
}); 
 
//Get current supplemental data id
var theCurrentSDID = visitor._supplementalDataIDCurrent ? visitor._supplementalDataIDCurrent : "";

//Call helper method to append SDID to the Page B URL from Page A 
var pageB = "www.domain.com/pageB"; 
var pageBWithSdid = visitor.appendSupplementalDataIDTo(pageB, theCurrentSDID)); 
```
