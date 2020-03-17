---
description: Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av andra Experience Cloud-lösningar med ID-tjänsten.
keywords: ID Service
seo-description: Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av andra Experience Cloud-lösningar med ID-tjänsten.
seo-title: Vanliga frågor om andra Experience Cloud-lösningar
title: Vanliga frågor om andra Experience Cloud-lösningar
uuid: 7d848663-6cbb-4d80-ab06-7b6d2dc20e2b
translation-type: tm+mt
source-git-commit: e6d65f1bfed187d7440512e8f3c2de0550506c95

---


# Vanliga frågor om andra Experience Cloud-lösningar{#faqs-for-other-experience-cloud-solutions}

Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av andra Experience Cloud-lösningar med ID-tjänsten.

## Dynamic Tag Management (DTM) {#section-7ac4b9c1f1fd45a5a03eac3fb5968af7}

**Kan jag använda dynamisk tagghantering för att distribuera besökar-ID-tjänsten?**

Ja, det här är det rekommenderade och rekommenderade distributionsalternativet.

Se [Standardimplementering med DTM](../implementation-guides/standard.md#concept-89cd0199a9634fc48644f2d61e3d2445).

## Analytics och Audience Manager {#section-b3dd206d497041acb04554c6fb1c912a}

**Kommer besökshistoriken för en användare att exporteras från[!DNL Adobe Analytics]till[!DNL Audience Manager]efter att jag har implementerat Experience Cloud Identity Service?**

Det finns två alternativ här:

* Om en användare har någon besöksaktivitet efter att ID-tjänsten har implementerats inkluderas besökaren och deras historik i dataexporten till [!DNL Audience Manager].
* Om en användare inte har någon besöksaktivitet efter att ID-tjänsten har implementerats inkluderas inte besökaren och historiken i dataexporten till Audience Manager. Eftersom det inte finns någon ny aktivitet kan vi inte koppla analys-ID:t till Experience Cloud-ID:t.

