---
description: Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av andra Experience Cloud-lösningar med ID-tjänsten.
keywords: ID-tjänst
title: Frågor och svar för andra Experience Cloud-lösningar
exl-id: d1164951-01c9-4375-981a-f87d8a280e4b
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 2%

---

# Vanliga frågor om andra Experience Cloud-lösningar{#faqs-for-other-experience-cloud-solutions}

Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av andra Experience Cloud-lösningar med ID-tjänsten.

## Dynamic Tag Management (DTM) {#section-7ac4b9c1f1fd45a5a03eac3fb5968af7}

**Kan jag använda dynamisk tagghantering för att distribuera besökar-ID-tjänsten?**

Ja, det här är det rekommenderade och rekommenderade distributionsalternativet.

Se [Standardimplementering med DTM](../implementation-guides/standard.md#concept-89cd0199a9634fc48644f2d61e3d2445).

## Analyser och Audience Manager {#section-b3dd206d497041acb04554c6fb1c912a}

**Kommer besökshistoriken för en användare att exporteras från  [!DNL Adobe Analytics] till  [!DNL Audience Manager] efter att jag har implementerat Experience Cloud Identity Service?**

Det finns två alternativ här:

* Om en användare har någon besöksaktivitet efter att ID-tjänsten har implementerats inkluderas besökaren och deras historik i dataexporten till [!DNL Audience Manager].
* Om en användare inte har någon besöksaktivitet efter att ID-tjänsten har implementerats inkluderas inte besökaren och historiken i dataexporten till Audience Manager. Eftersom det inte finns någon ny aktivitet kan vi inte koppla analys-ID:t till Experience Cloud-ID:t.
