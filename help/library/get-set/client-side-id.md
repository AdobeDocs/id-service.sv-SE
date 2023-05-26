---
description: Anropa den här ID-tjänstfunktionen för att avgöra om ID-tjänsten genererade ett MID (klientside, Experience Cloud visitor ID). Finns i VisitorAPI.js version 1.7.0 eller senare.
keywords: ID-tjänst
title: isClientSideMarketingCloudVisitorID
exl-id: ed2672e7-da1a-4c02-9f4e-c14419ec9ec7
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# isClientSideMarketingCloudVisitorID{#isclientsidemarketingcloudvisitorid}

Anropa den här ID-tjänstfunktionen för att avgöra om ID-tjänsten genererade ett MID (klientside, Experience Cloud visitor ID). Finns i VisitorAPI.js version 1.7.0 eller senare.

**Syntax**

`var *`variableName`* = visitor.isClientSideMarketingCloudVisitorID()`

I följande tabell visas och beskrivs de svar som returneras av den här funktionen.

<table id="table_5D08A5DD6FD04F94818B0E8B790D3136"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Svar </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> sant</span> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten kunde inte eller fick inte ett MID från <span class="keyword"> Experience Cloud</span> server. Ett MID skapades lokalt i webbläsaren (klientsidan). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> falskt</span> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten tog emot ett MID från <span class="keyword"> Experience Cloud</span> server. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> null</span> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten gjorde inget anrop till <span class="keyword"> Experience Cloud</span> server. </p> </td> 
  </tr> 
 </tbody> 
</table>
