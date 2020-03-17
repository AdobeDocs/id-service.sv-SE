---
description: En valfri boolesk flagga som förhindrar att ID-tjänsten anropar andra domäner.
keywords: cross domain tracking;ID Service
seo-description: En valfri boolesk flagga som förhindrar att ID-tjänsten anropar andra domäner.
seo-title: disableThirdPartyCalls
title: disableThirdPartyCalls
uuid: e92ce1f5-67a4-476c-9d04-41d4e96b1592
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c

---


# disableThirdPartyCalls{#disablethirdpartycalls}

En valfri boolesk flagga som förhindrar att ID-tjänsten anropar andra domäner.

**Syntax:** ` `disableThirdPartyCall: true|false&quot;(standard är `false`.)

När `disableThirdPartyCalls: true`detta inträffar kommer ID-tjänsten inte att göra anrop till andra domäner.

**Syfte**

Variabeln är avsedd för kunder som behöver:

* För att förhindra att ID-tjänsten ringer upp sina säkra, autentiserade sidor.
* Besökare på webbplatsen ska ha ett Experience Cloud ID (MID).
* Deras övriga Experience Cloud-lösningar fungerar som de ska.

**Genomförandestrategi**

Eftersom andra Experience Cloud-lösningar är beroende av MID, anropar ID-tjänsten Adobe för att returnera och ange detta ID. Om du behöver stoppa ID-tjänsten från att ringa anrop från autentiserade avsnitt på webbplatsen kan du låta den ringa dessa nödvändiga samtal från sidor som inte kräver autentisering först. När besökaren har ett MID kan du ange ID-tjänstkoden `disableThirdPartyCalls= true` i de autentiserade avsnitten på platsen. Förutsättningen här är att de flesta, om inte alla, av dina kunder navigerar till en autentiseringssida innan de får tillgång till de säkra delarna av din webbplats.

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

