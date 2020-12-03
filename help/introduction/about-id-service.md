---
description: Experience Cloud Identity Service i Adobe Experience Cloud.
keywords: ID Service
seo-description: Experience Cloud Identity Service i Adobe Experience Cloud.
seo-title: Om ID-tjänsten
title: Översikt
uuid: c52d6155-00a0-4fc5-9d8e-5ce00b8d01e6
translation-type: tm+mt
source-git-commit: ec67177fc6491e4c8cea835d198574c9fdb4b01f
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Om ID-tjänsten{#aboutidservice}

Experience Cloud Identity Service i Adobe Experience Cloud.

<!--
mcvid-functionality.xml
-->

## Experience Cloud Identity Service: En grundläggande del av bastjänsterna {#section-2de0eb1d65664e92a4d8bbb167b84bde}

Experience Cloud Identity Service möjliggör ett gemensamt identifieringsramverk för Experience Cloud Core Services, lösningar, kundattribut och målgrupper. Det fungerar genom att tilldela ett unikt, beständigt ID till en besökare. När din organisation implementerar ID-tjänsten kan du med detta ID identifiera samma besökare och deras data i olika Experience Cloud-lösningar.

![](assets/ecid-new.png)

Dessutom kan ID-tjänsten ersätta olika lösningsspecifika ID:n (t.ex. Analytics AID). Och med funktionerna [Kund-ID:n och Autentiseringstillstånd](../reference/authenticated-state.md) kan du med ID-tjänsten skicka dina egna kund-ID:n till [!DNL Experience Cloud]. Tänk dock på att ID-tjänsten bara fungerar med de lösningar du redan prenumererar på. Den ger inte åtkomst till andra produkter om du inte är registrerad för dem.

Framöver är ID-tjänsten en integrerad komponent i många aktuella och framtida [!DNL Experience Cloud] funktioner, förbättringar och tjänster. För närvarande stöder ID-tjänsten [Analytics](http://www.adobe.com/marketing-cloud/web-analytics.html), [Audience Manager](http://www.adobe.com/marketing-cloud/data-management-platform.html)och [Target](http://www.adobe.com/marketing-cloud/testing-targeting.html). Och det krävs om du vill delta i Device Co-op [!DNL Adobe Experience Cloud] . Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu. Mer information om ID-tjänstens betydelse och roll finns i [Varför Experience Cloud Identity Service ska finnas på din radardator](http://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/).

## Sammanfattning av funktioner {#section-96555473455c4bf8924c2d56ff4f3255}

Sammanfattningsvis kan ID-tjänsten:

* Skapar en gemensam nyckel eller ett ID som kan användas för att länka profiler och identiteter.
* Identifierar unikt en enhet över flera lösningar.
* Ställer in en cookie för första part i kundens domän för att säkerställa spårning på samma domän. Se [Experience Cloud](../introduction/cookies.md).
* Tar emot alias och ID-mappningar från [!DNL Experience Cloud] kunder och partners.
* Hanterar ID-synkronisering i [!DNL Experience Cloud].
* Stöder synkronisering med olika tredjepartsleverantörer över hela reklamteknikens ekosystem.
