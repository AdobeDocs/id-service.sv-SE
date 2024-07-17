---
description: Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av Analytics med Experience Cloud Identity Service.
keywords: Experience Cloud Identity Service
title: Vanliga frågor om analys- och identitetstjänster
exl-id: 98aeca0d-41a2-4b18-b307-19a6de816e38
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Vanliga frågor om analys- och identitetstjänster{#analytics-and-id-service-faqs}

Vanliga frågor och svar om funktioner, funktioner och problem i samband med användning av Analytics med identitetstjänsten.

## Spårningsservrar {#section-9a2ad7842e364c869e1650480d17f8ef}

**Hur hittar jag min spårningsserverinformation?**

Alla korrekt konfigurerade koddelar innehåller din spårningsserverinformation.

Men ibland kan kunderna dela upp sina Analytics-AppMeasurement i separata filer. Vissa kunder kan till exempel placera konfigurationsvariabler i en fil, använda en andra fil för plugin-program och sedan placera AppMeasurementen i en tredje fil. Detta rekommenderas inte.

Om du inte kan hitta din spårningsserverinformation kanske inte Analytics-instansen är korrekt konfigurerad. Kontakta [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) om du inte hittar din spårningsserverinformation.

**Vad händer om jag använder identitetstjänsten och ändrar min spårningsserver?**

Ingenting ändras för användare som redan har identifierats av identitetstjänsten. Gamla besökare som inte har migrerats till identitetstjänsten och som fortfarande identifieras med en Analytics-cookie klickas. Hur många användare som påverkas beror på hur länge identitetstjänsten har varit aktiv. En implementering där identitetstjänsten har varit aktiv i en vecka kan till exempel ha fler äldre användare än en implementering där identitetstjänsten har varit aktiv i sex månader eftersom användare som återvänder till webbplatsen skulle ha flyttats.

## Implementering och konfiguration {#section-6028f55d5b514ae6a631c6a79f42fb89}

**Måste jag konfigurera en CNAME för att spåra besökare över domäner?**

Om du har en huvudwebbplats där kunder kan identifieras innan de besöker andra domäner kan en CNAME aktivera spårning av korsdomäner i webbläsare som inte accepterar cookies från tredje part (till exempel Safari).

I webbläsare som accepterar cookies från tredje part anges en cookie i domänen [demdex.net](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html) under begäran att hämta ett besökar-ID. Denna cookie gör det möjligt för identitetstjänsten att returnera samma besökar-ID för Experience Cloud på alla domäner som har konfigurerats med samma organisations-ID. I webbläsare som avvisar cookies från tredje part tilldelas varje domän ett nytt besökar-ID för Experience Cloud.

Även när en CNAME är konfigurerad identifieras besökare annorlunda på den sekundära webbplatsen och huvudwebbplatsen i webbläsare som inte accepterar cookies från tredje part om huvudstartwebbplatsen inte besöks först.

**Varför finns inte Experience Cloud ID-parametern (MID) i Analytics-begäran?**

Om identitetstjänsten returnerar information korrekt, men du inte ser parametern `MID`, kontrollerar du att du har uppgraderat till en version av AppMeasurementet som stöds.

**Kan min webbplats använda H-kod och AppMeasurement för JavaScript med identitetstjänsten?**

Ja. Så länge båda filerna refererar till samma VisitorAPI.js-fil kan du använda en blandning av H-kod och AppMeasurement för JavaScript på hela webbplatsen.

H-kod stöds dock inte med visitorAPI.js-koden version 1.6 eller senare. Om du vill uppgradera till visitorAPI.js v 1.6 (eller senare) kan du inte fortsätta använda H-kod.

**Vad är en respitperiod och hur konfigurerar jag den?**

Se [Identitetstjänstens respitperiod](../reference/analytics-reference/grace-period.md) och kontakta [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html).

**Varför måste jag migrera till datainsamling i realtid (RDC) för att kunna använda identitetstjänsten?**

RDC ger globala prestandafördelar och krävs för att säkerställa att implementeringen är klar för kommande funktioner som utnyttjar det globala nätverket av edge notes. Se [Analyskrav: Regional Data Collection (RDC)](../reference/requirements.md#section-7d04bb013bc84a25bae3b148bc0ca25f).

## Rapportering {#section-123cd55a32e54a45a23beb140becfa8f}

**Vilka möjliga orsaker till diskrepanser när Analytics används med identitetstjänsten?**

Vanliga orsaker till diskrepanser vid användning av identitetstjänsten är:

* Fortsatt användning av den gamla s_vi-cookien. Detta bidrar till avvikelser i datainsamlingen.
* Dubbelräkna besökare när de navigerar från en undersökning till ett popup-fönster.

## Cookies {#section-b7d5384fbedd47b09e1030211c39a3d1}

**Vad händer i Analytics när identitetstjänsten inte kan ange AMCV-cookien?**

Det finns tre möjliga scenarier där detta påverkar analysdata för nya besökare:

1. En slutanvändare lämnar en sida innan AMCV-cookies har angetts korrekt (inom det 30 sekunder långa timeoutfönstret).

   Om en besökare lämnar en sida innan inläsningen är klar skickas inte Analytics-träffen. Analyserna tar inte emot data från det här scenariot och anser att data som gått förlorade till ett tidigt avslutande av sidan. Baserat på våra tester, som inkluderade avlägset belägna områden, fann vi att detta scenario i genomsnitt utgjorde mindre än 1 % av trafiken. Det är viktigt att notera att detta scenario inträffar ibland även utan att identitetstjänsten finns - det är en artefakt av att koden för insamling av analysdata finns med längst ned på sidan.

1. En slutanvändare har inte tilldelats någon identitetstjänst eller ett analys-ID inom det 30 sekunder långa timeoutfönstret på grund av långsamma anslutningar eller webbläsarens &quot;snurrning&quot;.

   Både identitetstjänsten och analys-ID skulle inte anges och besökaren skulle tilldelas ett klient-side-ID. Detta gör det möjligt att samla in analysdata, men besökarens profil kommer att avbrytas när ett analys-ID anges på en efterföljande sida. Klientsidans ID matchar inte heller någon befintlig besökarprofil som lagras i Audience Manager eller Analytics. Detta ID för klientsidan visas också som två olika besökare i Analytics om två separata domäner skickas till samma rapportsvit.

1. En slutanvändare tilldelas inte något ID-tjänste-ID inom det 30 sekunder långa timeoutfönstret, men tilldelas ett standardID för Analytics-spårning och respitperioden är inte aktiverad.

   Scenario 3 har samma resultat som scenario 2 eftersom ett klientbaserat ID används.

>[!TIP]
>
>Om du använder de senaste uppdateringarna av VisitorAPI.js och AppMeasurement.js med standardinställningarna bör du undvika allvarliga eller märkbara konsekvenser av de tre osannolika scenarierna ovan.

>[!MORELIKETHIS]
>
>* [Kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html)
