---
description: En valfri boolesk flagga som förhindrar att ID-tjänsten anropar andra domäner.
keywords: spårning av korsdomän;ID-tjänst
title: disableThirdPartyCall
exl-id: 1d5b4e80-1b2d-4401-9057-449a6abf5db5
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# disableThirdPartyCall{#disablethirdpartycalls}

En valfri boolesk flagga som förhindrar att ID-tjänsten anropar andra domäner.

**Syntax:** ` `disableThirdPartyCall: true|false (standard är `false`).

När `disableThirdPartyCalls: true` anropas inte andra domäner av ID-tjänsten.

**Syfte**

Variabeln är avsedd för kunder som behöver:

* För att förhindra att ID-tjänsten ringer upp sina säkra, autentiserade sidor.
* Besökare på webbplatsen ska ha ett Experience Cloud-ID (MID).
* Deras andra Experience Cloud-lösningar fungerar som de ska.

**Implementeringsstrategi**

Eftersom andra Experience Cloud-lösningar är beroende av MID, anropar ID-tjänsten Adobe för att returnera och ange detta ID. Om du behöver stoppa ID-tjänsten från att ringa anrop från autentiserade avsnitt på webbplatsen kan du låta den ringa dessa nödvändiga samtal från sidor som inte kräver autentisering först. När besökaren har ett MID kan du ange `disableThirdPartyCalls= true` i ID-tjänstkoden för de autentiserade avsnitten på platsen. Förutsättningen här är att de flesta, om inte alla, av era kunder kommer att navigera till en autentiseringssida innan de får tillgång till de säkra delarna av er webbplats.

**Kodexempel**

```js
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here",{ 
   trackingServer: "Insert tracking server here here",  //Same as s.trackingServer 
   trackingServerSecure: "Insert secure tracking server here",  //Same as s.trackingServerSecure 
 
   //For CNAME support only. Exclude these variables if you're not using CNAME 
   marketingCloudServer: "Insert tracking server here", 
   marketingCloudServerSecure: "Insert secure tracking server here", 
 
   //Function variable 
   disableThirdPartyCalls: true 
}); 
```
