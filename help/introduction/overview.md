---
description: Experience Cloud Identity-tjänstens roll i Adobe Experience Cloud.
seo-description: Experience Cloud Identity Service (tidigare Visitor ID-tjänst eller Marketing Cloud ID-tjänst) aktiverar det gemensamma identifieringsramverket för Experience Cloud-tjänster som kundattribut och målgrupper.
seo-title: Översikt över tjänsten Experience Cloud ID
title: Översikt över tjänsten Experience Cloud ID
translation-type: tm+mt
source-git-commit: 98b72f87b188debd6a5f6b86822c3f714647de61
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# Översikt över tjänsten Experience Cloud ID

Det [!UICONTROL Experience Cloud Identity Service] möjliggör ett gemensamt identifieringsramverk för Experience Cloud Core Services (t.ex. kundattribut och målgrupper) i Experience Platform Identity Service.

>[!NOTE]
>
> Du kan se referenser till ID-tjänsten som akronymer eller tidigare namn, som ECID, Marketing Cloud ID-tjänst (MID) och Visitor ID-tjänst. De hänvisar till [!UICONTROL Experience Cloud Identity Service]. Du kanske också ser [!UICONTROL Experience Platform Identity Service]. Förtydliga:

* [!UICONTROL Experience Platform Identity Service]: Tjänsten som länkar identiteter. Det är en enhetslänkningstjänst för personbaserad upplevelsehantering.
* [!UICONTROL Experience Cloud ID Service] (ECID): Det unika, beständiga ID som tilldelats en besökare. Det är en specifik enhet som kan användas av plattformsidentitetstjänsten.

När din organisation implementerar ID-tjänsten kan du med detta ID identifiera samma besökare och deras data i olika Experience Cloud-lösningar.

![](assets/ecid-new.png)

Dessutom kan ID-tjänsten ersätta olika lösningsspecifika ID:n (t.ex. Analytics AID). Och med funktionerna [Kund-ID och Autentiseringstillstånd](/help/reference/authenticated-state.md) kan du med ID-tjänsten skicka dina egna kund-ID:n till Experience Cloud. Tänk dock på att ID-tjänsten bara fungerar med de lösningar du redan prenumererar på. Den ger inte åtkomst till andra produkter om du inte är registrerad för dem.

I framtiden är ID-tjänsten en integrerad komponent i många nuvarande och framtida funktioner, förbättringar och tjänster för Experience Cloud. För närvarande stöder ID-tjänsten [Analytics](http://www.adobe.com/marketing-cloud/web-analytics.html), [Audience Manager](http://www.adobe.com/marketing-cloud/data-management-platform.html)och [Target](http://www.adobe.com/marketing-cloud/testing-targeting.html). Och det krävs om du vill delta i Adobe Experience Cloud Device Co-op. Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu. Mer information om ID-tjänstens betydelse och roll finns i [Varför Experience Cloud Identity Service ska finnas på din radardator](http://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/).

## Sammanfattning av funktioner

Sammanfattningsvis kan ID-tjänsten:

* Skapar en gemensam nyckel eller ett ID som kan användas för att länka profiler och identiteter.
* Identifierar unikt en enhet över flera lösningar.
* Ställer in en cookie för första part i kundens domän för att säkerställa spårning på samma domän. Mer information finns i dokumentet om [cookies och Experience Cloud Identity Service](https://docs.adobe.com/content/help/sv-SE/id-service/using/intro/cookies.html) .
* Tar emot alias och ID-mappningar från Experience Cloud kunder och partners.
* Hanterar ID-synkronisering i Experience Cloud.
* Stöder synkronisering med olika tredjepartsleverantörer över hela reklamteknikens ekosystem.

## Krav för ID-tjänst

Din lösning och andra Adobe-kodbibliotek måste uppfylla [vissa krav](/help/reference/requirements.md) innan du kan använda ID-tjänsten.

* [Cookies och Experience Cloud Identity Service](cookies.md): ID-tjänsten använder ditt företags-ID, Experience Cloud AMCV-cookie och en demdex-cookie för att skapa och lagra unika, beständiga identifierare för webbplatsens besökare. Med dessa cookies kan ID-tjänsten spåra besökare i olika domäner och möjliggöra datadelning mellan olika Experience Cloud-lösningar.
* [Så här begär och anger Experience Cloud Identity Service ID](id-request.md): En översikt över ID-begäran och svarsprocessen. De här exemplen omfattar ID-tilldelning på enskilda webbplatser, på olika webbplatser och för webbplatser som hanteras av olika Experience Cloud-kunder med egna företags-ID:n.
* [Förstå ID-synkronisering och matchningsfrekvenser](match-rates.md): En översikt över ID-synkroniseringsprocesser och matchningsfrekvenser i Experience Cloud Identity Service, inklusive Adobe Media Optimizer och ID-tjänsten.
