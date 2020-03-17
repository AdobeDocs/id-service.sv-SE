---
description: Med den här variabeln kan du åsidosätta standardintervallet för livstid för AMCV-cookien.
keywords: ID Service
seo-description: Med den här variabeln kan du åsidosätta standardintervallet för livstid för AMCV-cookien.
seo-title: cookieLifetime
title: cookieLifetime
uuid: cd945db3-429a-4625-ac3f-69ac259377a3
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c

---


# cookieLifetime{#cookielifetime}

Med den här variabeln kan du åsidosätta standardintervallet för livstid för AMCV-cookien.

Som standard upphör cookies i ID-tjänster att gälla efter 24 månader. [!DNL Experience Cloud] Ange tidsintervallet i sekunder.

**Syntax:** livstid i ` cookieLifetime: *`sekunder`*`

**Kodexempel**

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

