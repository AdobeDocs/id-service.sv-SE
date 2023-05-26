---
description: Detta är ett asynkront API som returnerar identifierare för Analytics, ID-tjänsten, avanmälan av datainsamling, geografisk plats och metadatablockinnehåll som standard. Du kan också styra vilka ID:n du vill returnera med den valfria uppräkningen visitor.FIELDS.
keywords: ID-tjänst
title: getVisitorValues
exl-id: bd023e8d-a804-4205-989f-e1e58080b63c
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# getVisitorValues{#getvisitorvalues}

Detta är ett asynkront API som returnerar identifierare för Analytics, ID-tjänsten, avanmälan av datainsamling, geografisk plats och metadatablockinnehåll som standard. Du kan också styra vilka ID:n du vill returnera med den valfria uppräkningen visitor.FIELDS.

Innehåll:

<ul class="simplelist"> 
 <li> <a href="../../library/get-set/getvisitorvalues.md#section-5aebe3907b2b46e997f45a1d1ed35c09" format="dita" scope="local"> Syntax </a> </li> 
 <li> <a href="../../library/get-set/getvisitorvalues.md#section-36a31683558742a5915db3a391e09f7b" format="dita" scope="local"> Användningsfall 1: Begär standarddatauppsättning </a> </li> 
 <li> <a href="../../library/get-set/getvisitorvalues.md#section-467b2f4e513344c89b7332b05f6f59f3" format="dita" scope="local"> Användningsfall 2: Begär en anpassad datauppsättning </a> </li> 
 <li> <a href="../../library/get-set/getvisitorvalues.md#section-4c4c300167694c6fbff1d6c612f372b5" format="dita" scope="local"> Svarsparametrar definierade </a> </li> 
</ul>

## Syntax {#section-5aebe3907b2b46e997f45a1d1ed35c09}

Den här funktionen använder följande syntax (kursiv stil representerar en platshållare för en variabel): ` var *`values`* = visitor.getVisitorValues (callback, [visitor.FIELDS. *`ID-typ`*, visitor.FIELDS. *`ID-typ`*]);`

I funktionsparametrarna:

* ` *`callback`*` representerar din egen callback-kod som tar emot returnerade ID:n.
* *(Valfritt)* ` visitor.FIELDS. *`ID-typ`*` är en uppräkning där du kan ange vilken [ID-värden](../../library/get-set/getvisitorvalues.md#section-4c4c300167694c6fbff1d6c612f372b5) du vill att den här funktionen ska returneras.

Mer information finns i följande användningsexempel och definitioner.

## Användningsfall 1: Begär standarddatauppsättning {#section-36a31683558742a5915db3a391e09f7b}

Den här koden returnerar standarddatauppsättningen. Din förfrågan och ditt svar kan se ut som i följande exempel.

```js
//Call the ID service 
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{...}); 
   
//Add your callback to the GET method to return IDs and data. 
visitor.getVisitorValues(visitorIdsCallback);
```

I standardsvaret på samplingen har vissa värden förkortats i demonstrationssyfte.

```js
//Formatted IDs in JSON response 
{ 
    MCMID: 'mid-1234', 
    MCOPTOUT: 'isoptedout-true', 
    MCAID: 'aid-1234', 
    MCAAMLH: 7, 
    MCAAMB: 'hgfe54236786oygj' 
}
```

## Användningsfall 2: Begär en anpassad datauppsättning {#section-467b2f4e513344c89b7332b05f6f59f3}

Den här koden använder en valfri array för att returnera en specifik uppsättning ID:n med `visitor.FIELDS` enum. I det här fallet vill vi bara ha besökarens Experience Cloud ID (MCID) och Analytics ID (MCAID). Din förfrågan och ditt svar kan se ut som i följande exempel.

```js
//Call the ID service 
var visitor = Visitor.getInstance("Insert Experience Cloud organization ID here", { ... });

// Add an optional array to specify which IDs you want to return. 
visitor.getVisitorValues(visitorIdsCallback, [visitor.FIELDS.MCMID, visitor.FIELDS.MCAID]);
```

Det anpassade exempelsvaret returnerar endast de ID:n som anges i begäran.

```js
//Formatted IDs in JSON response 
{ 
    MCMID: 'mid-1234', 
    MCAID: 'aid-4321' 
}
```

## Svarsparametrar definierade {#section-4c4c300167694c6fbff1d6c612f372b5}

I följande tabell visas och definieras svarsparametrarna. Detta är också alla värden i `visitor.FIELDS` enum. Observera att den här metoden returnerar en tom sträng om det inte finns några värden för en viss variabel.

<table id="table_32D0FEEA76CE4F298EED4B8F5C644232"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Värde </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> MCAAMB </span> </p> </td> 
   <td colname="col2"> <p>Krypterad <span class="keyword"> Audience Manager </span> metadata som kallas"blob". </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> MCAAMLH </span> </p> </td> 
   <td colname="col2"> <p>Datainsamlingens region-ID. Detta är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. </p> <p>Se <a href="https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html" format="https" scope="external"> DCS-region-ID, -platser och -värdnamn </a> och <a href="../../library/get-set/getlocationhint.md#reference-a761030ff06c4439946bb56febf42d4c" format="dita" scope="local"> getLocationHint </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> MCAID </span> </p> </td> 
   <td colname="col2"> <p>Besökarens <span class="keyword"> Analyser </span> ID. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> MCMID </span> </p> </td> 
   <td colname="col2"> <p>Besökarens Experience Cloud-ID. </p> <p>Se <a href="../../introduction/cookies.md" format="dita" scope="local"> Cookies och Experience Cloud Identity Service </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> MCOPTOUT </span> </p> </td> 
   <td colname="col2"> <p>En flagga som anger om en besökare har valt att inte samla in data. </p> <p>Värdena är: </p> <p> 
     <ul id="ul_E82431DE12B449F8822499364B363798"> 
      <li id="li_2BAB7C15A38A408E8FC4B85E70B66E46"> <span class="codeph"> 'isoptedout-true' </span>: En besökare har valt bort datainsamling. </li> 
      <li id="li_BB80AE4CEBC44166BC04428B212FEF51"> <span class="codeph"> 'isoptedout-false' </span>: En besökare har inte avanmält sig från datainsamlingen. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
