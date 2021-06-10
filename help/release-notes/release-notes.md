---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID-tjänst
title: Versionsinformation 2020
exl-id: c9d7876e-debc-4c8e-8ebc-91646610c876
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 5%

---

# Versionsinformation för Experience Cloud - 2020 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service (ECID).

## Version 4.6

* Skapade `loadSSL`-flagga som standard. Alla anrop till identitetstjänsten är som standard på `https`.  Kunderna kan ställa in det på false om de vill anropa Identity Services på http från sina `non-ssl`-sidor.
* Funktionen som används för att identifiera versionen `Internet-Explorer (IE)` har uppdaterats för att åtgärda ett problem som rapporterats av `ESLint`.
Åtgärda prestandaproblem den `Internet-Explorer (IE) 11` när ECID ges optIn `pre-approval` och uppdateras senare.

## Version 4.5

* Från och med version 4.5 avvisar ECID alla tomma ID:n som skickas till metoden `setCustomerIDs`.
* Ett problem som uppstod när anmälan konfigurerades som `doesOptInApply=false` och `isIabContext=true` har korrigerats.

Information om månadsversioner för alla produkter finns i [Versionsinformation för Experience Cloud](https://docs.adobe.com/content/help/sv-SE/release-notes/experience-cloud/current.html).
