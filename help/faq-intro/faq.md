---
description: Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av ID-tjänsten.
keywords: ID-tjänst
title: Vanliga frågor om ID-tjänster
exl-id: 4dd2220c-8a9d-4e27-838b-be5ad357cb3e
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 1%

---

# Vanliga frågor om ID-tjänsten{#id-service-faqs}

Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av ID-tjänsten.

## Funktionalitet {#section-659e89f8b9a74cb8afff35587dc96836}

**Vilken typ av funktioner tillhandahåller ID-tjänsten?**

Se [Översikt](../introduction/overview.md).

**Varför gör ID-tjänsten inget anrop för att hämta Experience Cloud-ID?**

Detta kan vara svårt att diagnostisera. En sak som du kan kontrollera är rubrikerna för skyddsprofiler på din webbplats. Om du har en strikt säkerhetsprincip kan dessa inställningar blockera tredjepartssamtal som görs av ID-tjänsten. Se [Principer för innehållssäkerhet och Experience Cloud-identitetstjänsten](../reference/csp.md#concept-968c423a7392479db0a0d821ae9783e3).

**Lagring av VisitorAPI.js-filer**

Du kan få problem om du har VisitorAPI.js som värd för en lokal fil i mobilappar. Vi rekommenderar att du har filen på en webbserver.

## Inläsningstider för sidan och fördröjning {#section-c78e148d8dbe4c77a436ef0f2af5434b}

**Hur påverkar placeringen av ID-tjänstens VisitorAPI.js-bibliotek sidinläsningstiderna?**

Placera VisitorAPI.js-biblioteket överst på sidan i `<head>`-avsnittet i koden. Detta bidrar till att säkerställa att anropet för ett ID skickas innan sidans brödtext börjar läsas in och maximerar chanserna för att ett ID returneras korrekt.

Anropet till ID-tjänsten är asynkront och är det enda anropet till domänen [demdex.net](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html). Anropet till ID-tjänsten blockerar inte andra element från att läsas in på sidan.

För [!DNL Target]-kunder kan det öka chanserna att ett [!DNL Target]-anrop blockeras om ID-tjänstkoden placeras i `<body>` på sidan. Om du måste placera ID-tjänstkoden i sidans brödtext ska den placeras efter den öppna `<body>`-taggen.

**Gör ID-tjänsten ett serversamtal med varje sidinläsning?**

Nej, det här samtalet sker endast första gången sidan återges och därefter var sjunde dag. Under tiden krävs inga serversamtal. ID-tjänsten körs i klientläge och behöver inte göra något serveranrop för att returnera ett ID.

Se [Översikt](../introduction/overview.md).

**När du använder ID-tjänsten, vad kan orsaka långsam sidinläsning eller påverka användarupplevelsen?**

Det är svårt att katalogisera alla möjliga villkor. Miljoner kunder ansluter till våra tjänster och den enorma variationen i var och hur de kopplar samman påverkar prestandan. Exempel:

* Hastigheten varierar kraftigt i mobilnätverk. Dessa nätverk lider också av signal- och data- eller röstpaketsförlust.
* Anslutningen påverkas av enheter som ansluter via WiFi under olika förhållanden. Exempel: paketförluster och hastighetsproblem är vanliga på offentliga platser som kaféer eller i andra miljöer som flygplan där paketen måste studsa genom en satellit innan de når markbundna nätverk.
* Dåligt konfigurerade lokala nätverk kan påverka anslutningsmöjligheterna och hastigheten negativt.
* Klientenheter kan ha egna problem, t.ex. för lite minne, för mycket diskbyte eller begränsad processorkraft jämfört med den aktuella arbetsbelastningen.
* Webbläsarna köar och kör fjärrserveranrop och bearbetar till och med svaren med olika regler, beroende på webbläsartillverkare och version. Det här beteendet påverkar hastighet och prestanda.

**Kan du ange några förbättringar som du har gjort för att korta sidinläsningstiderna?**

Till exempel, trådgenerering. Vi har introducerat trådgenerering om flera ID-synkroniseringsbegäranden skulle göras. Vi har observerat från labbrapporter att användargränssnittet skulle blockeras för kunder som utför flera ID-synkroniseringar på grund av att en mängd kontinuerliga CPU-beräkningar sker. Därför introducerade vi trådar som separerar begäranden om ID-synkronisering med 100 msek vardera.

Den här förändringen förbättrar prestanda för kunder som använder Visitor 2.3.0+ och DIL 6.10+. Förbättringarna av sidinläsningstiderna visas i bilden nedan:

![](assets/id_sync_improvements_copy.png)

**Påverkar webbläsarbegäranden med CORS jämfört med JSON-P sidprestanda?**

Resursbegäranden med CORS är vanligtvis mer att föredra än med JSONP. Med JSONP kan vissa webbläsare köa och avprioritera begäranden i förhållande till andra synkrona och asynkrona anrop på sidan. CORS ser till att dessa begäranden behandlas med högre prioritet i webbläsarens anropsstack.

Se [CORS-stöd i Experience Cloud Identity Service](../reference/cors.md#concept-6c280446990d46d88ba9da15d2dcc758).

## Säkerhet {#section-b176b8492fbe4acfb79ebb30ec902f98}

**Stöder ID-tjänsten CORS?**

Ja. Se [CORS-stöd i Experience Cloud Identity Service](../reference/cors.md#concept-6c280446990d46d88ba9da15d2dcc758).

**Vad är CORS?**

*`Cross-Origin Resource Sharing`* eller CORS är en metod som används i webbläsare för att begära resurser. ID-tjänsten begär alltid resurser med CORS i webbläsare som stöder det. ID-tjänsten begär resurser med JSON-P i äldre webbläsare som inte stöder CORS. Se [Experience Cloud](../reference/cors.md#concept-6c280446990d46d88ba9da15d2dcc758).

**Vad händer om mina säkerhetskrav är så strikta att jag aldrig vill använda JSONP?**

Om du har strikta säkerhetskrav anger du API-konfigurationen för ID-tjänsten `useCORSOnly: true`. Du bör bara aktivera det här läget om du är säker på att webbplatsens besökare använder webbläsare som stöder CORS.

Se [Experience Cloud](../reference/cors.md#concept-6c280446990d46d88ba9da15d2dcc758) och [useCORSOnly](../library/function-vars/use-cors-only.md#reference-8a9a143d838b48d6b23329b84b13e1fa).

>[!MORELIKETHIS]
>
>* [Kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html)

