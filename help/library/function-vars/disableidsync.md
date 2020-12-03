---
description: En valfri boolesk flagga som inaktiverar ID-synkronisering.
keywords: ID Service
seo-description: En valfri boolesk flagga som inaktiverar ID-synkronisering.
seo-title: disableIdSyncs
title: disableIdSyncs
uuid: 8bea1de8-53c8-4a15-bcf5-f0869763a32e
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c
workflow-type: tm+mt
source-wordcount: '44'
ht-degree: 4%

---


# disableIdSyncs{#disableidsyncs}

En valfri boolesk flagga som inaktiverar ID-synkronisering.

>[!NOTE]
>
>Den här konfigurationen har fått `idSyncDisableSyncs` ett nytt namn `disableIdSyncs` i version 3.0 från 18 januari 2018.

**Syntax:** `disableIdSyncs: true|false` (standard är `false`.)

**Exempel på kod**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable 
   disableIdSyncs: true 
});
```

