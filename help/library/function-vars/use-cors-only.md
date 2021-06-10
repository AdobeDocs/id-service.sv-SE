---
description: En valfri boolesk flagga som styr hur webbläsaren begär resurser från Experience Cloud Identity Service.
keywords: ID-tjänst
title: useCORSOnly
exl-id: 049a082a-8e6b-44cc-bd05-c12aaf3cbe4d
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 2%

---

# useCORSOnly{#usecorsonly}

En valfri boolesk flagga som styr hur webbläsaren begär resurser från Experience Cloud Identity Service.

**Syntax:** `useCORSOnly: true|false` (default is  `false`.)

**Översikt**

När inställningen är `false` utför webbläsaren resurskontroller med CORS eller JSONP. Men ID-tjänsten försöker alltid begära resurser med CORS först. Den återgår till JSONP i äldre webbläsare som inte stöder CORS. Om du behöver tvinga webbläsaren att endast använda CORS anger du `useCORSOnly:true` i funktionsanropet `Visitor.getInstance`.

>[!IMPORTANT]
>
>`Set useCORSOnly: true` om du har strikta säkerhetskrav. Du bör bara aktivera det här läget om du är säker på att alla besökare använder webbläsare som stöder CORS. Användarupplevelsen påverkas inte av webbläsare som inte stöder CORS. Webbläsare utan stöd för CORS kan dock inte begära resurser eller utbyta data med [!DNL Adobe Experience Cloud].

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
