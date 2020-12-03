---
title: Identifiera unika besökare
description: Dokumentation för Adobe ECID (ID-tjänst)
translation-type: tm+mt
source-git-commit: 8ad5ae179540596913fccc59070aecc57b09f586
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 13%

---


# Identifiera unika besökare

Metoden för att identifiera unika besökare i flera sammanhang innehåller en prioriterad sekvens för att säkerställa noggrannheten vid fastställandet. I följande tabell visas den prioriterade sekvensen:

| Order som används | Frågeparameter (samlingsmetod) | post_visid_type, kolumnvärde | Visas när |
|---|---|---|---|
|  1  | vid[s.visitorID](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)  | 0  | `s.visitorID` är inställt. |
|  2  | aid[s_vi cookie](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)  | 3  | Besökaren hade en befintlig s_vi-cookie innan du distribuerade Visitor ID-tjänsten, eller så har du konfigurerat en[respitperiod](https://docs.adobe.com/content/help/en/id-service/using/reference/analytics-reference/grace-period.html)för Visitor ID.  |
|  3  | mid[AMCV_ cookie inställd av identitetstjänsten](https://docs.adobe.com/content/help/sv-SE/id-service/using/home.html)  |  5  |  Besökarens webbläsare accepterar cookies (första part) och[!UICONTROL Identity Service]distribueras.  |
|  4  | fet[reservcookie på H.25.3 eller senare, eller AppMeasurement för JavaScript](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)  |  4  |  Besökarens webbläsare accepterar cookies (förstapartsprogram).  |
|  5  |  [HTTP Mobile Subscriber header](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)  |  2  |  Enheten känns igen som en mobil enhet.  |
|  6  |  [IP-adress, användaragent, gateway-IP-adress](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)  |  1  |  Besökarens webbläsare accepterar inte cookies. |

Information om hur unika besökare rapporteras finns i [Unika besökare i Analytics](https://docs.adobe.com/content/help/en/analytics/components/variables/dimensions-reports/reports-unique-visitors-v15-dsc.html).
