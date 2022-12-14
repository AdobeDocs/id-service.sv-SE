---
description: Experience Cloud Identity-tjänstens roll i Adobe Experience Cloud.
title: Experience Cloud Identity Service - översikt
exl-id: dc7d6220-d42b-4a3e-bf37-1e4e87280ae1
source-git-commit: f7c25f5ebd0690c56c081422949eb34f1f277ae1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Experience Cloud Identity Service - översikt

Experience Cloud Identity Service aktiverar det gemensamma identifieringsramverket för Experience Cloud Application Services. Du kan använda Experience Cloud Identity Service för att ange [Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html).

ECID är ett delat ID-namnområde som används i Adobe Experience Platform- och Experience Cloud-program för att spåra besökares beteende och se till att varje enhet har en unik identifierare som kan finnas kvar i flera sessioner.

>[!TIP]
>
>Experience Cloud Identity Service, Experience Platform Identity Service och ECID är tre **olika** enheter.

Experience Cloud Identity Service kan ersätta olika programspecifika ID:n och använda [Kund-ID och autentiseringstillstånd](/help/reference/authenticated-state.md) så att du kan skicka in dina egna kund-ID:n till Experience Cloud.

>[!NOTE]
>
>Experience Cloud Identity Service fungerar bara med Experience Cloud Application Services som du prenumererar på och ger inte tillgång till andra programtjänster om du inte prenumererar på dem.

Experience Cloud Identity Service stöder följande program:

* [Adobe Analytics](https://business.adobe.com/products/analytics/web-analytics.html)
* [Audience Manager](https://business.adobe.com/products/audience-manager/adobe-audience-manager.html)
* [Adobe Target](https://business.adobe.com/products/target/adobe-target.html)

I framtiden är ID-tjänsten en integrerad komponent i många nuvarande och framtida funktioner, förbättringar och tjänster för Experience Cloud. För närvarande stöder ID-tjänsten [Analyser](http://www.adobe.com/marketing-cloud/web-analytics.html), [Audience Manager](http://www.adobe.com/marketing-cloud/data-management-platform.html)och [Mål](http://www.adobe.com/marketing-cloud/testing-targeting.html). Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu.

## Sammanfattning av funktioner

Sammanfattningsvis hjälper Experience Cloud Identity Service till att

* Identifierar en besökare på en enhet i flera program.
* Ställer in en cookie för första part i kundens domän för att säkerställa spårning på samma domän. Visa dokumentet på [cookies och Experience Cloud Identity Service](./cookies.md) för mer information.
* Tar emot alias och ID-mappningar från Experience Cloud kunder och partners.
* Hanterar ID-synkronisering i Experience Cloud.
* Stöder synkronisering med olika tredjepartsleverantörer över hela reklamteknikens ekosystem.

## Krav för identitetstjänsten i Experience Cloud

Din lösning och andra Adobe-kodbibliotek måste uppfylla [vissa krav](/help/reference/requirements.md) innan du kan använda identitetstjänsten.

* [Cookies och Experience Cloud Identity Service](cookies.md): Identitetstjänsten för Experience Cloud använder ditt företags-ID, Experience Cloud AMCV-cookien och en demdexcookie för att skapa och lagra unika, beständiga identifierare för webbplatsens besökare. Med dessa cookies kan identitetstjänsten spåra besökare i olika domäner och möjliggöra datadelning mellan olika Experience Cloud-lösningar.
* [Så här begär och anger Experience Cloud Identity Service ID:n](id-request.md): En översikt över ID-begäran och svarsprocessen. De här exemplen omfattar ID-tilldelning på enskilda webbplatser, på olika webbplatser och för webbplatser som hanteras av olika Experience Cloud-kunder med egna företags-ID:n.
* [Förstå ID-synkronisering och matchningsfrekvenser](match-rates.md): En översikt över ID-synkroniseringsprocesser och matchningsfrekvenser i Experience Cloud Identity Service, inklusive Adobe Media Optimizer och Identity Service.
