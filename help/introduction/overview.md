---
description: Experience Cloud Identity-tjänstens roll i Adobe Experience Cloud.
title: Översikt över tjänsten Experience Cloud ID
exl-id: dc7d6220-d42b-4a3e-bf37-1e4e87280ae1
source-git-commit: 2c87022baeb09a8767d0d9627bf2b607c51b2503
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Översikt över tjänsten Experience Cloud ID

[!UICONTROL Experience Cloud Identity Service] aktiverar det gemensamma identifieringsramverket för Experience Cloud Core Services-lösningar (som kundattribut och målgrupper) i Experience Platform Identity Service.

>[!NOTE]
>
> Du kan se referenser till ID-tjänsten som akronymer eller tidigare namn, som ECID, Marketing Cloud ID-tjänst (MID) och Visitor ID-tjänst. Dessa hänvisar till [!UICONTROL Experience Cloud Identity Service]. Du kan också se [!UICONTROL Experience Platform Identity Service]. Förtydliga:

* [!UICONTROL Experience Platform Identity Service]: Tjänsten som länkar identiteter. Det är en enhetslänkningstjänst för personbaserad upplevelsehantering.
* [!UICONTROL Experience Cloud ID Service] (ECID): Det unika, beständiga ID som tilldelats en besökare. Det är en specifik enhet som kan användas av plattformsidentitetstjänsten.

När din organisation implementerar ID-tjänsten kan du med detta ID identifiera samma besökare och deras data i olika Experience Cloud-lösningar.

![](assets/ecid-new.png)

Dessutom kan ID-tjänsten ersätta olika lösningsspecifika ID:n (t.ex. Analytics AID). Och med funktionen [Kund-ID:n och autentiseringstillstånd](/help/reference/authenticated-state.md) kan ID-tjänsten skicka dina egna kund-ID:n till Experience Cloud. Tänk dock på att ID-tjänsten bara fungerar med de lösningar du redan prenumererar på. Den ger inte åtkomst till andra produkter om du inte är registrerad för dem.

I framtiden är ID-tjänsten en integrerad komponent i många nuvarande och framtida funktioner, förbättringar och tjänster för Experience Cloud. För närvarande stöder ID-tjänsten [Analytics](http://www.adobe.com/marketing-cloud/web-analytics.html), [Audience Manager](http://www.adobe.com/marketing-cloud/data-management-platform.html) och [Target](http://www.adobe.com/marketing-cloud/testing-targeting.html). Och det krävs om du vill delta i Adobe Experience Cloud Device Co-op. Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu.

## Sammanfattning av funktioner

Sammanfattningsvis kan ID-tjänsten:

* Skapar en gemensam nyckel eller ett ID som kan användas för att länka profiler och identiteter.
* Identifierar unikt en enhet över flera lösningar.
* Ställer in en cookie för första part i kundens domän för att säkerställa spårning på samma domän. Mer information finns i dokumentet om [cookies och Experience Cloud Identity Service](./cookies.md).
* Tar emot alias och ID-mappningar från Experience Cloud kunder och partners.
* Hanterar ID-synkronisering i Experience Cloud.
* Stöder synkronisering med olika tredjepartsleverantörer över hela reklamteknikens ekosystem.

## Krav för ID-tjänst

Lösningen och andra kodbibliotek i Adobe måste uppfylla [vissa krav](/help/reference/requirements.md) innan du kan använda ID-tjänsten.

* [Cookies och Experience Cloud Identity Service](cookies.md): ID-tjänsten använder ditt företags-ID, Experience Cloud AMCV-cookie och en demdex-cookie för att skapa och lagra unika, beständiga identifierare för webbplatsens besökare. Med dessa cookies kan ID-tjänsten spåra besökare i olika domäner och möjliggöra datadelning mellan olika Experience Cloud-lösningar.
* [Så här begär och anger Experience Cloud Identity Service ID](id-request.md): En översikt över ID-begäran och svarsprocessen. De här exemplen omfattar ID-tilldelning på enskilda webbplatser, på olika webbplatser och för webbplatser som hanteras av olika Experience Cloud-kunder med egna företags-ID:n.
* [Förstå ID-synkronisering och matchningsfrekvenser](match-rates.md): En översikt över ID-synkroniseringsprocesser och matchningsfrekvenser i Experience Cloud Identity Service, inklusive Adobe Media Optimizer och ID-tjänsten.
