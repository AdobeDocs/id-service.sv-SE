---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID Service
seo-description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
seo-title: Versionsinformation 2020
title: Versionsinformation 2020
translation-type: tm+mt
source-git-commit: c4da0f3da99a96d2be7421f49e0e88286d0505e0

---


# Versionsinformation om Experience Cloud - 2020 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service (ECID).

## Version 4.6

* Flagga `loadSSL` aktiverad som standard. Alla anrop till identitetstjänsten är aktiverade `https` som standard.  Kunderna kan ställa in det på false om de vill anropa Identity Services på http från sina `non-ssl` sidor.
* Funktionen som används för att identifiera `Internet-Explorer (IE)` version har uppdaterats för att åtgärda ett problem som rapporterats av `ESLint`.
Åtgärda prestandaproblem när ECID ges optIn `Internet-Explorer (IE) 11` `pre-approval` och uppdateras senare.

## Version 4.5

* Från och med version 4.5 avvisar ECID alla tomma ID:n som skickas till `setCustomerIDs` metoden.
* Korrigerade ett problem som uppstod när anmälan konfigurerades som `doesOptInApply=false` och `isIabContext=true`.
