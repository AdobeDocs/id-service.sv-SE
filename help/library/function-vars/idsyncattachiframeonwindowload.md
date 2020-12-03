---
description: En valfri boolesk flagga som styr hur Experience Cloud Identity Service läser in iFrame för ID-synkronisering.
keywords: ID Service
seo-description: En valfri boolesk flagga som styr hur Experience Cloud Identity Service läser in iFrame för ID-synkronisering.
seo-title: idSyncAttachIframeOnWindowLoad
title: idSyncAttachIframeOnWindowLoad
uuid: aa2c2fa4-2cab-4e08-8d35-729a6c3e459a
translation-type: tm+mt
source-git-commit: e6d65f1bfed187d7440512e8f3c2de0550506c95
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 2%

---


# idSyncAttachIframeOnWindowLoad{#idsyncattachiframeonwindowload}

En valfri boolesk flagga som styr hur Experience Cloud Identity Service läser in iFrame för ID-synkronisering.

**Syntax:** ` `idSyncAttachIframeOnWindowLoad= true|false&quot;(standard är `false`.)

När `idSyncAttachIframeOnWindowLoad: true` ID-tjänsten läser in iFrame för synkronisering av ID vid inläsning av fönster. Som standard läser ID-tjänsten in iFrame för ID-synkronisering så snabbt som möjligt i stället för vid inläsning av fönster.

**Exempel på kod**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable. Example loads ID sync iFrame on window load instad of ASAP. 
   idSyncAttachIframeOnWindowLoad: true 
});
```

