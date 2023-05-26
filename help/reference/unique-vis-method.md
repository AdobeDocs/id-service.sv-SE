---
title: Identifiera unika besökare
description: Dokumentation för Adobe ECID (ID-tjänst)
exl-id: 379dbf0a-814d-4348-9ac4-d0e8fc13b9dc
source-git-commit: c65816530ae2269b216f60b9b0450077e5aaac2f
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 4%

---

# Identifiera unika besökare

Metoden för att identifiera unika besökare i flera sammanhang innehåller en prioriterad sekvens för att säkerställa noggrannheten vid fastställandet. I följande tabell visas den prioriterade sekvensen:

| Order som används | Frågeparameter (samlingsmetod) | post_visid_type, kolumnvärde | Visas när |
|---|---|---|---|
|  1  | intensiv [s.visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=en)  | 0  | `s.visitorID` är inställt. |
|  2  | stöd  [s_vi cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-analytics.html?lang=en#section-5d50a078de444d12b7d927d68ff3b679)  | 3  | Besökaren hade en befintlig s_vi-cookie innan du distribuerade Visitor ID-tjänsten, eller så har du ett besökar-ID [respitperiod](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html?lang=en) konfigurerad.  |
|  3  | mitten [AMCV_ cookie inställd av identitetstjänsten](../introduction/cookies.md)  |  5  |  Besökarens webbläsare accepterar cookies (första part) och [!DNL Identity Service] distribueras.  |
|  4  | fet [grundcookie på H.25.3 eller senare, eller AppMeasurement for JavaScript](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-analytics.html?lang=en#section-65e33f9bfc264959ac1513e2f4b10ac7)  |  4  |  Besökarens webbläsare accepterar cookies (förstapartsprogram).  |
|  5  |  [HTTP Mobile Subscriber header](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=en)  |  2  |  Enheten känns igen som en mobil enhet.  |
|  6  |  [IP-adress, användaragent, gateway-IP-adress](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en)  |  1  |  Besökarens webbläsare accepterar inte cookies. |

{style="table-layout:auto"}

Information om hur unika besökare rapporteras finns på [Unika besökare i analyser](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=en).
