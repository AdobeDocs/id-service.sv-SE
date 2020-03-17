---
description: Krävs för flerdelsdomäner på den översta nivån där någon av de två sista delarna av URL:en är längre än 2 tecken.
keywords: ID Service
seo-description: Krävs för flerdelsdomäner på den översta nivån där någon av de två sista delarna av URL:en är längre än 2 tecken.
seo-title: cookieDomain
title: cookieDomain
uuid: a57e5477-c07b-4d54-8aea-8e8b152f1423
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c

---


# cookieDomain{#cookiedomain}

Krävs för flerdelsdomäner på den översta nivån där någon av de två sista delarna av URL:en är längre än 2 tecken.

**Syntax:** ` cookieDomain: " *`URL`*"` ( `www` prefixet är inte obligatoriskt.)

**Användningsfall**

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

