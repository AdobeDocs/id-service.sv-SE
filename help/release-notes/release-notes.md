---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID Service
seo-description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
seo-title: Versionsinformation 2020
title: Versionsinformation 2020
translation-type: tm+mt
source-git-commit: d0057a8242dafca63101b1a2f569766bde11bea7
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 5%

---


# Experience Cloud release notes - 2020 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service (ECID).

## Version 4.6

* Flagga `loadSSL` aktiverad som standard. Alla anrop till identitetstjänsten är aktiverade `https` som standard.  Kunderna kan ställa in det på false om de vill anropa Identity Services på http från sina `non-ssl` sidor.
* Funktionen som används för att identifiera `Internet-Explorer (IE)` version har uppdaterats för att åtgärda ett problem som rapporterats av `ESLint`.
Åtgärda prestandaproblem när ECID ges optIn `Internet-Explorer (IE) 11` `pre-approval` och uppdateras senare.

## Version 4.5

* Från och med version 4.5 avvisar ECID alla tomma ID:n som skickas till `setCustomerIDs` metoden.
* Korrigerade ett problem som uppstod när anmälan konfigurerades som `doesOptInApply=false` och `isIabContext=true`.

Information om månadsversioner finns i [Experience Cloud versionsinformation](https://docs.adobe.com/content/help/sv-SE/release-notes/experience-cloud/current.html) för alla produkter.
