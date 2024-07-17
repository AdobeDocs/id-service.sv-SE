---
description: En valfri boolesk flagga som styr hur Experience Cloud Identity Service läser in iFrame för ID-synkronisering.
keywords: ID-tjänst
title: idSyncAttachIframeOnWindowLoad
exl-id: 44c45378-f007-4d87-913a-d6bb9961948c
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# idSyncAttachIframeOnWindowLoad{#idsyncattachiframeonwindowload}

En valfri boolesk flagga som styr hur Experience Cloud Identity Service läser in iFrame för ID-synkronisering.

**Syntax:** ` `idSyncAttachIframeOnWindowLoad= true|false (standard är `false`).

När `idSyncAttachIframeOnWindowLoad: true` ID-tjänsten läser in iFrame för synkronisering av ID vid inläsning av fönster. Som standard läser ID-tjänsten in iFrame för ID-synkronisering så snabbt som möjligt i stället för vid inläsning av fönster.

**Kodexempel**

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
