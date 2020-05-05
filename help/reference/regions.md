---
description: AMCV-cookien innehåller Experience Cloud ID (MID) och ett region-ID för webbplatsens besökare. Dessa ID:n lagras som nyckelvärdepar. Mittanvändar-ID:t innehåller besökarens Experience Cloud-ID. Regionens id innehåller region-id:t för webbplatsens besökare. Du kan återställa informationen genom att analysera AMCV-cookien.
keywords: ID Service
seo-description: AMCV-cookien innehåller Experience Cloud ID (MID) och ett region-ID för webbplatsens besökare. Dessa ID:n lagras som nyckelvärdepar. Mittanvändar-ID:t innehåller besökarens Experience Cloud-ID. Regionens id innehåller region-id:t för webbplatsens besökare. Du kan återställa informationen genom att analysera AMCV-cookien.
seo-title: Hämta region- och användar-ID från AMCV Cookie eller ID-tjänsten
title: Hämta region- och användar-ID från AMCV Cookie eller ID-tjänsten
uuid: bdd9d001-f29f-4ff0-800b-8182243da218
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# Hämta region- och användar-ID från AMCV Cookie eller ID-tjänsten {#get-region-and-user-ids-from-the-amcv-cookie-or-the-id-service}

AMCV-cookien innehåller Experience Cloud ID (MID) och ett region-ID för webbplatsens besökare. Dessa ID:n lagras som nyckelvärdepar. Mittanvändar-ID:t innehåller besökarens Experience Cloud-ID. Det aamlh:region-ID som innehåller region-ID för webbplatsens besökare. Du kan återställa informationen genom att analysera AMCV-cookien.

Mer information finns i [Hämta användar-ID:n och regioner via Experience Cloud Identity Service](https://docs.adobe.com/content/help/en/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-mcid-ids.html).

Om du är [!DNL Audience Manager] kund kan du hämta region-ID:t från svaret som skickas av DCS-servern (Data Collection Server). Se [Hämta användar-ID och regioner från ett DCS-svar](https://docs.adobe.com/content/help/en/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-aam-ids.html).

Du kan också hämta region-ID:t med en `GET` metod som tillhandahålls av ID-tjänsten. Se [Hämta region-ID:n (platstips)](../library/get-set/getlocationhint.md#reference-a761030ff06c4439946bb56febf42d4c).
