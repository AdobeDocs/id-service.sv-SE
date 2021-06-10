---
description: Med den här variabeln kan du åsidosätta standardintervallet för livstid för AMCV-cookien.
keywords: ID-tjänst
title: cookieLifetime
exl-id: bdbabdcd-a87b-412c-8c2f-3f39820f939a
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 8%

---

# cookieLifetime{#cookielifetime}

Med den här variabeln kan du åsidosätta standardintervallet för livstid för AMCV-cookien.

Som standard upphör [!DNL Experience Cloud] ID-tjänstcookies att gälla efter 24 månader. Ange tidsintervallet i sekunder.

**Syntax:** ` cookieLifetime: *`livstid i sekunder`*`

**Exempel på kod**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable. Example changes expiration period to 12-months. 
   cookieLifetime:31536000 
});
```
