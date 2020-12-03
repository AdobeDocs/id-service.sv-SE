---
description: Den här egenskapen anger det ID för datakällans behållare som du vill använda för ID-synkroniseringar.
keywords: ID Service
seo-description: Den här egenskapen anger det ID för datakällans behållare som du vill använda för ID-synkroniseringar.
seo-title: idSyncContainerID
title: idSyncContainerID
uuid: e35dc48b-1aa1-41e3-91c1-ef1e9d2d8b90
translation-type: tm+mt
source-git-commit: f7f23d89649a888f5e9d8c94526b550fbda7045b
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---


# idSyncContainerID{#idsynccontainerid}

Den här egenskapen anger det ID för datakällans behållare som du vill använda för ID-synkroniseringar.

Innehåll:

<ul class="simplelist"> 
 <li> <a href="../../library/function-vars/idsyncontainerid.md#section-b0c50732b1c84bed8616e82e8e83d58c" format="dita" scope="local"> Exempel på syntax och kod </a> </li> 
 <li> <a href="../../library/function-vars/idsyncontainerid.md#section-6aed44fbe9d6401a8f912cb0d98339a7" format="dita" scope="local"> Vad är behållare och när skulle jag använda detta? </a> </li> 
 <li> <a href="../../library/function-vars/idsyncontainerid.md#section-f283cb69c8de4348b5316cc4e02a3e9e" format="dita" scope="local"> Ange behållar-ID när du använder DIL och VisitorAPI.js </a> </li> 
</ul>

## Exempel på syntax och kod {#section-b0c50732b1c84bed8616e82e8e83d58c}

**Syntax:** ` idSyncContainerID: *`behållar-ID-värde`*`

**Exempel på kod:**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   ... 
   //Set container ID 
   idSyncContainerID:80 
});
```

## Vad är behållare och när skulle jag använda detta? {#section-6aed44fbe9d6401a8f912cb0d98339a7}

**Behållare**

Behållare är objekt som skapas av [!DNL Audience Manager]. Även om de inte är externt tillgängliga listas alla datakällor som:

* Är tillgängliga för dig, men används inte, för ID-synkronisering.
* Används för ID-synkronisering.

Även om du inte är en [!DNL Audience Manager] kund har ditt konto dessa behållare om du utbyter ID:n med olika datakällor på olika sidor i domänen. Detta beror på att [!DNL Audience Manager] tillhandahåller den teknik och de serverfunktioner som möjliggör synkronisering av ID:n.

**Användningsexempel**

Beroende på din situation kan du behöva lägga till den här konfigurationen i din ID-tjänstkod eller inte.

<table id="table_48621F343C7F4760A75F6BCC2DB2DA20"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Villkor </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Behövs inte</b> </p> </td> 
   <td colname="col2"> <p>Du behöver inte använda den här konfigurationen om: </p> <p> 
     <ul id="ul_4D6F794CD65C43D0BEFBA6F5DE420C2E"> 
      <li id="li_0F048A6AC7BE4450AFA1B20B1AC25808">Du använder ID-tjänsten med någon <span class="keyword"> Experience Cloud- </span> lösning och utför inte ID-synkronisering med andra datakällor. I det här fallet har ditt konto en standardbehållare med ID 0 och ingen åtgärd krävs. </li> 
      <li id="li_5657D64D9406407D9B4DB7D8BE4F8EE4">Alla datakällor finns i en enda behållare. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Behövs</b> </p> </td> 
   <td colname="col2"> <p>Du måste använda den här konfigurationen när alla dessa villkor gäller: </p> <p> 
     <ul id="ul_9AFD14FC5A2745F7BD7BE7B64545DA62"> 
      <li id="li_04F0EFBBD71B43608CAAA7E7409D33FE">Du använder inte <span class="keyword"> Audience Manager </span>. </li> 
      <li id="li_4BFA6DC76CE9455EBBC337FD2FE820BF">Du måste synkronisera ID:n med andra datakällor som är ordnade efter behållare. </li> 
      <li id="li_731DA5D1CBF244F8BEBE57C0E2EBA713">Du måste synkronisera ID:n med datakällor i olika behållare på olika sidor i domänen. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

## Ange behållar-ID när du använder DIL och VisitorAPI.js {#section-f283cb69c8de4348b5316cc4e02a3e9e}

Om du har distribuerat [!UICONTROL DIL]*och* VisitorAPI.js på samma sida:

* Tjänstkoden för besökar-ID har företräde framför DIL för ID-synkroniseringar.
* Ange endast konfigurationen i ID-tjänstkoden `idSyncContainerID` .

