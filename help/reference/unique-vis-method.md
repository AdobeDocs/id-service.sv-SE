---
title: Identifiera unika besökare
description: Dokumentation för Adobe ECID (ID-tjänst)
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# Identifiera unika besökare

Metoden för att identifiera unika besökare i flera sammanhang innehåller en prioriterad sekvens för att säkerställa noggrannheten vid fastställandet. I följande tabell visas den prioriterade sekvensen:
 
| Beställning används | Frågeparameter (samlingsmetod) | post_visid_type, kolumnvärde | Finns när |
|— |— |— |— |
| 1 |[vid (s.visitorID)](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)| 0 |s.visitorID har angetts.|
| 2 |[hjälp (s_vi cookie)](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)| 3 |Visitor hade en befintlig s_vi-cookie innan du distribuerade Visitor ID-tjänsten, eller så har du konfigurerat en[respitperiod](https://docs.adobe.com/content/help/en/id-service/using/reference/analytics-reference/grace-period.html)för besöks-ID. |
| 3 |[mid (AMCV_ cookie inställd av identitetstjänsten)](https://docs.adobe.com/content/help/en/id-service/using/home.html)| 5 | Besökarens webbläsare accepterar cookies (förstapartsprogrammet) och identitetstjänsten distribueras. |
| 4 |[find (fallback cookie on H.25.3 eller senare, eller AppMeasurement for JavaScript)](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)| 4 | Besökarens webbläsare accepterar cookies (första part). |
| 5 |[HTTP Mobile Subscriber header](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)| 2 | Enheten känns igen som en mobil enhet. |
| 6 |[IP-adress, användaragent, gateway-IP-adress](https://docs.adobe.com/content/help/en/analytics/technotes/visitor-identification.html)| 1 | Besökarens webbläsare accepterar inte cookies. |

Information om hur unika besökare rapporteras finns i [Unika besökare i Analytics](https://docs.adobe.com/content/help/en/analytics/components/variables/dimensions-reports/reports-unique-visitors-v15-dsc.html).
