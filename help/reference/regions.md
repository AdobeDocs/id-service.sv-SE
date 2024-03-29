---
description: AMCV-cookien innehåller Experience Cloud-ID (MID) och ett region-ID för webbplatsens besökare. Dessa ID:n lagras som nyckelvärdepar. Mittanvändar-ID:t innehåller besökarens Experience Cloud-ID. Regionens id innehåller region-id:t för webbplatsens besökare. Du kan återställa informationen genom att analysera AMCV-cookien.
keywords: ID-tjänst
title: Hämta region- och användar-ID från AMCV Cookie eller ID-tjänsten
exl-id: 986e761e-4bc7-4511-86b7-7d13a7761a2b
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Hämta region- och användar-ID från AMCV Cookie eller ID-tjänsten {#get-region-and-user-ids-from-the-amcv-cookie-or-the-id-service}

AMCV-cookien innehåller Experience Cloud-ID (MID) och ett region-ID för webbplatsens besökare. Dessa ID:n lagras som nyckelvärdepar. Mittanvändar-ID:t innehåller besökarens Experience Cloud-ID. Det aamlh:region-ID som innehåller region-ID för webbplatsens besökare. Du kan återställa informationen genom att analysera AMCV-cookien.

Mer information finns i [Hämta användar-ID:n och regioner via Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-mcid-ids.html).

Om du är en [!DNL Audience Manager] -kund kan du hämta region-ID:t från det svar som skickas av Data Collection Server (DCS). Se [Hämta användar-ID:n och regioner från ett DCS-svar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-aam-ids.html).

Du kan också hämta region-ID:t med en `GET` metod som tillhandahålls av ID-tjänsten. Se [Hämta region-ID (platstips)](../library/get-set/getlocationhint.md#reference-a761030ff06c4439946bb56febf42d4c).
