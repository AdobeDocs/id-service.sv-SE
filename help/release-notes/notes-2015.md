---
description: Versionsinformation och uppdateringar för 2015.
keywords: ID-tjänst
title: Versionsinformation 2015
exl-id: 57c45726-f856-4af5-a30a-9a1bdcaa6411
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# Versionsinformation 2015 {#release-notes}

Versionsinformation och uppdateringar för 2015.

## Version 1.5.3 {#section-7c09ba2832bd4644a1ccc3aa83abe66a}

November 2015

The Children&#39;s Online Privacy Protection Act (COPPA) förbjuder insamling av personuppgifter online från barn som är yngre än 13 år utan verifierbart föräldrars samtycke. Kunder som är intresserade av COPPA kan lägga till en valfri variabel till sina [!DNL Experience Cloud] ID-tjänstkod som hindrar den från att ange cookies i en webbläsares tredjepartsdomän. Se [Stöd för COPPA i Experience Cloud Identity Service](../reference/coppa.md#concept-d7ddf81bebd74f129661fcec1ca19413). För version 1.5.3 eller senare.

## Version 1.5.2 {#section-e3c73e47539942a89b02d33061128148}

September 2015

* Korrigerade ett fel i webbläsaren Safari som gjorde att synkroniseringstjänsterna inte fungerade när användare blockerade cookies från tredje part. (AAM-20764)
* Anrop till ID-tjänsten inkluderar nu versions-ID i `d_visid_ver=` parameter. Det returnerade ID:t hjälper interna team att felsöka och ge support. (AAM-20824)

## Version 1.5.1 {#section-f4309d7917964a748fee4bdb45bffa44}

Augusti 2015

* Korrigerade ett fel som hindrade ID-tjänsten från att begära en iframe om det inte finns några data att synkronisera eller utlösa. (AAM-20164)
* Ett fel som gjorde att ID-tjänsten inte kunde ställa in en domäncookie på flera delar har korrigerats. Om du till exempel har en domän som `my_company.co.uk`under vissa omständigheter skulle ID-tjänsten ställa in en cookie i `co.uk` endast. (AN-104683)

   Detta påverkade bara ett fåtal klienter som träffade *alla* av följande kriterier:

   * Använda ID-tjänsten.
   * Aktiverad som [respitperiod ](../reference/analytics-reference/grace-period.md)*eller* använder cookies från första part och användarna blockerar cookies från tredje part.

   * Har sidor med flerdelade toppnivådomäner.

Dokumentationsrevideringar i den här versionen är:

* [API-metoder och kodbibliotek](../library/library.md#concept-ff27497375644a898d47984aefb21c97): Omorganiserat innehåll och omorganiserad text. I de flesta fall får varje metod en egen sida.
* [Krav för Experience Cloud Identity Service](../reference/requirements.md): Reviderat innehåll och omorganiserad text.

## Version 1.5 {#section-db5edfa11ae143ada07a96e0ab06dc57}

Juli 2015

The [!DNL Experience Cloud] ID-tjänsten stöder flera ID:n och autentiseringstillstånd. Den här ändringen tar också bort inaktuellt stöd för [!DNL Audience Manager] DPID-mappningar till användar-ID som används av `setCustomerIDs` funktion. Se [Kund-ID och autentiseringstillstånd](../reference/authenticated-state.md)

## Version 1.4 {#section-f5c596f355b14da28f45c798df513572}

Maj 2015

Från och med version 1.4 skickar den inställda konfigurationsmetoden ett config-objekt i som den andra parametern till `Visitor.getInstance` funktion.

```js
var visitor = Visitor.getInstance("016D5C175213CCA80A490D05@AdobeOrg",{ 
    "loadTimeout":1000, 
    "trackingServer":"myco.sc.omtrdc.net", 
    "idSyncContainerID":80 
});
```

Se [Experience Cloud](../implementation-guides/setup-analytics.md#concept-9ebbea85cb844a15b557be572cd142fd).

## Version 1.3.5 {#section-eed4567f058f446d9a819e4682621aed}

Februari 2015

Korrigerade hanteringen av timeout för begäranden om AAM och platstips. Efter en timeout lämnas fälten tomma för den aktuella sidan och alla återanrop görs. Timeout-värdet behandlas som ett feltillstånd, så det kommer att försöka igen på nästa sida. (AN-94473, AN-94474)

## Version 1.3.4 {#section-bca4a3e7c05546b7af1c9ec47fdb3331}

Januari 2015

Realiserad `<head>/<body>` taggsökning för JSONP-begäran `<script>` -taggbehållare samt skapande av `<script>` tagg för att ta hänsyn till olika DOM-implementeringar (HTML eller XHTML) med möjligen olika skiftlägeskänslighetsinställningar. (AN-9355)
