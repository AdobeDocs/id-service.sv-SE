---
description: En valfri boolesk flagga som lägger till ett Secure-attribut i AMCV-cookien.
keywords: ID-tjänst
title: secureCookie
exl-id: ba281b1c-1112-4ed6-b4fd-b8f87cabc575
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---

# secureCookie{#securecookie}

En valfri boolesk flagga som lägger till ett Secure-attribut i AMCV-cookien.

Det här konfigurationsattributet är tillgängligt i `visitorAPI`, version 3.3.0.

>[!NOTE]
>
>Konfigurationen `SecureCookie` fungerar inte på oskyddade domäner och kan leda till att du inte får MID-värden för besök som använder ett oskyddat protokoll. Konfigurationen `secureCookie` ska bara anges till `true` när du är säker på att alla sidor och underdomäner alltid använder ett säkert protokoll.

**Syntax:** `secureCookie: true | false` (standard)

**Exempel på kod**

```js
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ID-HERE",{ 
 
        //Set secure cookie property 
        secureCookie: true 
 });
```
