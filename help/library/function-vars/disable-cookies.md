---
description: En valfri boolesk flagga som förhindrar att Experience Cloud Identity Service returnerar demdex.net cookie-filen.
keywords: ID-tjänst
title: disableThirdPartyCookies
exl-id: 19d12822-0e17-4a1c-8e9c-25a22e20a4a8
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# disableThirdPartyCookies{#disablethirdpartycookies}

En valfri boolesk flagga som förhindrar att Experience Cloud Identity Service returnerar demdex.net cookie-filen.

>[!NOTE]
>
>Den här konfigurationen var `idSyncDisable3rdPartySyncing` och döptes om till `disableThirdPartyCookies` i version 18 januari 2018 av v3.0.

**Syntax:** `disableThirdPartyCookies: true|false` (standard är `false`.) För `VisitorAPI.js` v3.0.0 eller senare.

När `disableThirdPartyCookies: true` returnerar ID-tjänsten inte tredjepartsprodukten demdex.net cookie (se [Cookies och Experience Cloud Identity Service ](../../introduction/cookies.md) ). Om en besökare redan har denna cookie i sin webbläsare kommer ID-tjänsten inte att använda den för att skapa ett nytt Experience Cloud-ID (MID) eller returnera ett befintligt ID. I stället skapar ID-tjänsten en ny slumpmässig MID i cookie-filen för första part. När du har aktiverat det kan du samla in data med ID-tjänsten och dela dem mellan olika Experience Cloud-lösningar.

**Kodexempel**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable 
   disableThirdPartyCookies: true 
});
```
