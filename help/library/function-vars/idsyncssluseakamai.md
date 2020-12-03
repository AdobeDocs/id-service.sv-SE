---
description: Anger om målpubliceringsmallen ska använda Akamai för HTTPS-anslutningar.
keywords: ID Service
seo-description: Anger om målpubliceringsmallen ska använda Akamai för HTTPS-anslutningar.
seo-title: idSyncSSLUseAkamai
title: idSyncSSLUseAkamai
uuid: 501ccc37-c3ab-4454-bfcf-3e3c3e8b5ca3
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 6%

---


# idSyncSSLUseAkamai{#idsyncssluseakamai}

Anger om målpubliceringsmallen ska använda Akamai för HTTPS-anslutningar.

Konfigurationen är aktiverad per partner `idSyncSSLUseAkamai` .

**Syntax:** `idSyncSSLUseAkamai: true`

**Exempel på kod**

```js
//Call the ID service 
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
 
    //Set Akamai URL for ID sync container 
    idSyncSSLUseAkamai:true 
 
    ... 
});
```

