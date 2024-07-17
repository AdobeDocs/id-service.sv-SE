---
description: Krävs för flerdelsdomäner på den översta nivån där någon av de två sista delarna av URL:en är längre än 2 tecken.
keywords: ID-tjänst
title: cookieDomain
exl-id: 280416ad-372a-4a59-a938-0f49c0ce300f
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# cookieDomain{#cookiedomain}

Krävs för flerdelsdomäner på den översta nivån där någon av de två sista delarna av URL:en är längre än 2 tecken.

**Syntax:** ` cookieDomain: " *`URL`*"` (prefixet `www` krävs inte.)

**Använd skiftläge**

* Obligatoriskt: `www.example.com.uk`
* Krävs inte: `www.example.co.uk`

**Kodexempel**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable 
   cookieDomain:"example.com.uk" 
});
```
