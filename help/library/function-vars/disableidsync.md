---
description: En valfri boolesk flagga som inaktiverar ID-synkronisering.
keywords: ID-tjänst
title: disableIdSyncs
exl-id: 96d42133-6040-4da3-9315-fd94318b33aa
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 5%

---

# disableIdSyncs{#disableidsyncs}

En valfri boolesk flagga som inaktiverar ID-synkronisering.

>[!NOTE]
>
>Den här konfigurationen `idSyncDisableSyncs` och ändrat namn till `disableIdSyncs` den 18 januari 2018-versionen av v3.0.

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
