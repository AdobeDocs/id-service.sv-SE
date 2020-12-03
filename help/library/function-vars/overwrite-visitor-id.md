---
description: Den här egenskapen skriver över en besökares Experience Cloud- och Analytics-ID:n när de navigerar från en domän till en annan. Om du vill skriva över ett ID måste du äga och ha implementerat ID-tjänsten på varje domän. Med den här koden kan du inte skriva över ID:n på domäner som du inte kontrollerar.
keywords: ID Service
seo-description: Den här egenskapen skriver över en besökares Experience Cloud- och Analytics-ID:n när de navigerar från en domän till en annan. Om du vill skriva över ett ID måste du äga och ha implementerat ID-tjänsten på varje domän. Med den här koden kan du inte skriva över ID:n på domäner som du inte kontrollerar.
seo-title: overwriteCrossDomainMCIDAndAID
title: overwriteCrossDomainMCIDAndAID
uuid: 8e48127a-ac62-4ea0-9756-2a27b20ecbcf
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---


# overwriteCrossDomainMCIDAndAID{#overwritecrossdomainmcidandaid}

Den här egenskapen skriver över en besökares Experience Cloud- och Analytics-ID:n när de navigerar från en domän till en annan. Om du vill skriva över ett ID måste du äga och ha implementerat ID-tjänsten på varje domän. Med den här koden kan du inte skriva över ID:n på domäner som du inte kontrollerar.

**Syntax:** `Visitor.overwriteCrossDomainMCIDAndAID: true|false` (standard är `false`)

**Exempel på kod**

JavaScript-koden kan se ut ungefär som i följande exempel.

```js
//Call the ID service 
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ID-HERE", { 
     ... 
 
     //Set overwrite property 
     overwriteCrossDomainMCIDAndAID: true 
}); 
```

**Användningsexempel**

Om du vill spåra besökare skriver ID-tjänsten ett [!DNL Experience Cloud] ID (eller MID) till en webbläsarcookie. I följande tabell visas och beskrivs de vanliga användningsfall där du kanske vill skriva över en befintlig MID som angetts av ID-tjänsten i en annan domän.

<table id="table_FC1AF6551D6646E0BF1C4FB7C1316EBB"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Användningsfall </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Identifiera besökare på olika domänlandningssidor</b> </p> </td> 
   <td colname="col2"> <p>Säg att ni äger Domains A och B. I det här fallet kan du ange <span class="codeph"> Visitor.overwriteCrossDomainMCIDAndAID: true </span> när: </p> <p> 
     <ul id="ul_FB4704BFE7134F1688E34BF1A36627B7"> 
      <li id="li_FF71FD1FB9DD4702B675A140FAD2B481">Varje domän har en egen landningssida. </li> 
      <li id="li_78F75469D32D473B93148B46D35E67F1">En besökare har redan en cookie (och ett MID) från ett tidigare besök i domän B. </li> 
      <li id="li_305CE5138EEB43D3BF9CE38D1E7FFA04">Du vill konsekvent identifiera en besökare om de kommer till domän B från domän A. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Identifiera besökare på landnings- och konverteringssidor</b> </p> </td> 
   <td colname="col2"> <p>Säg att ni äger Domains A och B. I det här fallet kan du ange <span class="codeph"> Visitor.overwriteCrossDomainMCIDAndAID: true </span> när: </p> 
    <ul id="ul_7BEBFD523A2F47AFB6963536E43692D0"> 
     <li id="li_71586080489340E2A6C0B263F231E3DE">Avsnitt A är en landningssida. </li> 
     <li id="li_4E3D3CB380EE4F1BAC4CD752194AE8DE">Avsnitt B är en separat sida för konvertering, bokning eller annat arbetsflöde. </li> 
     <li id="li_FB393B16CFAC4D2D9B2328EBA4573C1A">En besökare har redan en cookie (och ett MID) från ett tidigare besök i domän B och du vet att dessa är mindre önskade MID på klientsidan i stället för MID på serversidan. </li> 
     <li id="li_36FC138530A4476A995C0F9FD73C41DE">Du vill konsekvent identifiera en besökare om de kommer till domän B från domän A. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Identifiera besökare från mobilappar till webbläsare</b> </p> </td> 
   <td colname="col2"> <p>Det här användningsfallet är något annorlunda. Det handlar om att identifiera användare när de går från en mobilapp till din webbplats. I det här fallet har besökaren redan en MID lokalt angiven av en mobilapp och har en annan MID angiven i en cookie på webbplatsen. Du kan ange <span class="codeph"> Visitor.overwriteCrossDomainMCIDAndAID: true </span> för att skriva över MID som angetts i webbläsarens cookie med MID som angetts av mobilappen. </p> </td> 
  </tr> 
 </tbody> 
</table>

