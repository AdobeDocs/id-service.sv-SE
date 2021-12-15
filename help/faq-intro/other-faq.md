---
description: Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av andra Experience Cloud-lösningar med ID-tjänsten.
keywords: ID-tjänst
title: Frågor och svar för andra Experience Cloud-lösningar
exl-id: d1164951-01c9-4375-981a-f87d8a280e4b
source-git-commit: e171c94ccfa1f4fe9b8d909d0204adb94f20cbb6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Frågor och svar för andra Experience Cloud-lösningar{#faqs-for-other-experience-cloud-solutions}

Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av andra Experience Cloud-lösningar med ID-tjänsten.

## Analyser och Audience Manager {#section-b3dd206d497041acb04554c6fb1c912a}

**Exporteras användarens besökshistorik från [!DNL Adobe Analytics] till [!DNL Audience Manager] efter att jag har implementerat Experience Cloud Identity Service?**

Det finns två alternativ här:

* Om en användare har någon besöksaktivitet efter att ID-tjänsten har implementerats inkluderas besökaren och deras historik i dataexporten till [!DNL Audience Manager].
* Om en användare inte har någon besöksaktivitet efter att ID-tjänsten har implementerats inkluderas inte besökaren och historiken i dataexporten till Audience Manager. Eftersom det inte finns någon ny aktivitet kan vi inte koppla analys-ID:t till Experience Cloud-ID:t.
