---
description: Anropa den här ID-tjänstfunktionen för att avgöra om ID-tjänsten genererade ett MID (Experience Cloud visitor ID) på klientsidan. Finns i VisitorAPI.js version 1.7.0 eller senare.
keywords: ID Service
seo-description: Anropa den här ID-tjänstfunktionen för att avgöra om ID-tjänsten genererade ett MID (Experience Cloud visitor ID) på klientsidan. Finns i VisitorAPI.js version 1.7.0 eller senare.
seo-title: isClientSideMarketingCloudVisitorID
title: isClientSideMarketingCloudVisitorID
uuid: 1c39ac60-1d2b-4ed4-a2ea-30d680e61e10
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c

---


# isClientSideMarketingCloudVisitorID{#isclientsidemarketingcloudvisitorid}

Anropa den här ID-tjänstfunktionen för att avgöra om ID-tjänsten genererade ett MID (Experience Cloud visitor ID) på klientsidan. Finns i VisitorAPI.js version 1.7.0 eller senare.

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
   <td colname="col1"> <p> <span class="codeph"> true</span> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten kunde inte eller fick inte ett MID från <span class="keyword"> Experience Cloud</span> -servern. Ett MID skapades lokalt i webbläsaren (klientsidan). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> false</span> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten tog emot ett MID från <span class="keyword"> Experience Cloud</span> -servern. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> null</span> </p> </td> 
   <td colname="col2"> <p>ID-tjänsten ringde inte till <span class="keyword"> Experience Cloud</span> -servern. </p> </td> 
  </tr> 
 </tbody> 
</table>

