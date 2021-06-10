---
description: Anger ett tidsgränsintervall i millisekunder. Används för att berätta om andra lösningar (t.ex. Analytics, Audience Manager, Target osv.) hur länge du ska vänta på ett svar från ID-tjänsten.
keywords: ID-tjänst
title: loadTimeout
exl-id: 485264f4-ee24-4042-8be3-259e70462110
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 1%

---

# loadTimeout{#loadtimeout}

Anger ett tidsgränsintervall i millisekunder. Används för att berätta om andra lösningar (t.ex. Analytics, Audience Manager, Target osv.) hur länge du ska vänta på ett svar från ID-tjänsten.

**Syntax:** ` loadTimeout: *`intervall i millisekunder`*`

Standardvärdet är 30 000 millisekunder (30 sekunder). Vi rekommenderar att du *inte* ändrar standardvärdet.

>[!NOTE]
>
>Anrop till ID-tjänsten är asynkrona i förhållande till annan kod som inte är Adobe på sidan. Om du ökar eller minskar tidsgränsen ändras alltså inte den hastighet med vilken sidan återger innehåll. Långa timeoutintervall kan dock påverka sidinläsningstider som mäts med vanliga nätverksövervakningsverktyg, men återgivningstiden påverkas inte.

**Exempel på kod**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable. Example sets the timeout to 10,000 milliseconds (10 seconds). 
   loadTimeout:10000 
});
```
