---
description: En valfri boolesk flagga som styr hur webbläsaren begär resurser från Experience Cloud Identity Service.
keywords: ID Service
seo-description: En valfri boolesk flagga som styr hur webbläsaren begär resurser från Experience Cloud Identity Service.
seo-title: useCORSOnly
title: useCORSOnly
uuid: 607dc035-dffc-4f4d-be51-08ef6c0a8fad
translation-type: tm+mt
source-git-commit: e6d65f1bfed187d7440512e8f3c2de0550506c95
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---


# useCORSOnly{#usecorsonly}

En valfri boolesk flagga som styr hur webbläsaren begär resurser från Experience Cloud Identity Service.

**Syntax:** `useCORSOnly: true|false` (standard är `false`.)

**Översikt**

När inställningen är `false`aktiverad utför webbläsaren resurskontroller med CORS eller JSONP. Men ID-tjänsten försöker alltid begära resurser med CORS först. Den återgår till JSONP i äldre webbläsare som inte stöder CORS. Om du behöver tvinga webbläsaren att endast använda CORS anger du `useCORSOnly:true` i `Visitor.getInstance` funktionsanropet.

>[!IMPORTANT]
>
>`Set useCORSOnly: true` om du har strikta säkerhetskrav. Du bör bara aktivera det här läget om du är säker på att alla besökare använder webbläsare som stöder CORS. Användarupplevelsen påverkas inte av webbläsare som inte stöder CORS. Webbläsare utan CORS-stöd kan dock inte begära resurser eller utbyta data med [!DNL Adobe Experience Cloud].

**Exempel på kod**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable 
   useCORSOnly: true 
});
```

