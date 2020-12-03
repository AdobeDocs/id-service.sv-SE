---
description: En valfri boolesk flagga som lägger till ett Secure-attribut i AMCV-cookien.
keywords: ID Service
seo-description: En valfri boolesk flagga som lägger till ett Secure-attribut i AMCV-cookien.
seo-title: secureCookie
title: secureCookie
uuid: 995d19f6-9c9d-4493-9c9c-545b0b5696b0
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# secureCookie{#securecookie}

En valfri boolesk flagga som lägger till ett Secure-attribut i AMCV-cookien.

Det här konfigurationsattributet är tillgängligt i `visitorAPI`, version 3.3.0.

>[!NOTE]
>
>Konfigurationen fungerar inte på oskyddade domäner och kan leda till att du inte får MID-värden för besök som använder ett oskyddat protokoll. `SecureCookie` Konfigurationen ska `secureCookie` bara anges till `true` när du är säker på att alla sidor och underdomäner alltid använder ett säkert protokoll.

**Syntax:** `secureCookie: true | false` (standard)

**Exempel på kod**

```js
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ID-HERE",{ 
 
        //Set secure cookie property 
        secureCookie: true 
 });
```

