---
description: En valfri boolesk flagga som förhindrar att Experience Cloud Identity Service returnerar cookie-filen demdex.net från tredje part.
keywords: ID Service
seo-description: En valfri boolesk flagga som förhindrar att Experience Cloud Identity Service returnerar cookie-filen demdex.net från tredje part.
seo-title: disableThirdPartyCookies
title: disableThirdPartyCookies
uuid: 7ed5aa16-44ca-4702-878a-1a208ca95270
translation-type: tm+mt
source-git-commit: 584b6240c3e0286111689499ca5df5d98aa9fab2

---


# disableThirdPartyCookies{#disablethirdpartycookies}

En valfri boolesk flagga som förhindrar att Experience Cloud Identity Service returnerar cookie-filen demdex.net från tredje part.

>[!NOTE]
>
>Den här konfigurationen har fått `idSyncDisable3rdPartySyncing` ett nytt namn `disableThirdPartyCookies` i version 3.0 från 18 januari 2018.

**Syntax:** `disableThirdPartyCookies: true|false` (standard är `false`.) För `VisitorAPI.js` v3.0.0 eller senare.

När `disableThirdPartyCookies: true`ID-tjänsten inte returnerar någon cookie för dedex.net (se [Cookies och Experience Cloud Identity Service](../../introduction/cookies.md) ). Om en besökare redan har denna cookie i sin webbläsare kommer ID-tjänsten inte att använda den för att skapa ett nytt Experience Cloud ID (MID) eller returnera ett befintligt ID. I stället skapar ID-tjänsten en ny slumpmässig MID i cookie-filen för första part. När den är aktiverad kan ni samla in data med ID-tjänsten och dela dem med olika Experience Cloud-lösningar.

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

