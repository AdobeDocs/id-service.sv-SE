---
description: Dessa instruktioner är till för Analytics- och Audience Manager-kunder som vill använda Experience Cloud identitetstjänst och inte använder dynamisk tagghantering (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
keywords: ID Service
seo-description: Dessa instruktioner är till för Analytics- och Audience Manager-kunder som vill använda Experience Cloud identitetstjänst och inte använder dynamisk tagghantering (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
seo-title: Implementera identitetstjänsten Experience Cloud för Analytics och Audience Manager
title: Implementera identitetstjänsten Experience Cloud för Analytics och Audience Manager
uuid: d46050ae-87de-46cc-911b-d6346c7fd511
translation-type: tm+mt
source-git-commit: ddff95876722b981f22c7e3196ff2ce9b696010e
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---


# Implementera identitetstjänsten Experience Cloud för Analytics och Audience Manager{#implement-the-experience-cloud-id-service-for-analytics-and-audience-manager}

Dessa instruktioner är till för Analytics- och Audience Manager-kunder som vill använda Experience Cloud identitetstjänst och inte använder dynamisk tagghantering (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.

>[!IMPORTANT]
>
>* [Läs kraven](../reference/requirements.md) innan du börjar.
>* Den här proceduren kräver AppMeasurement. Kunder som använder s_code kan inte slutföra den här proceduren.
>* Konfigurera och testa koden i en utvecklingsmiljö innan den implementeras i produktionen.


## Steg 1: Planera för vidarebefordran på serversidan {#section-880797cc992d4755b29cada7b831f1fc}

Utöver de steg som beskrivs här, bör kunder som använder [!DNL Analytics] och [!DNL Audience Manager] bör migrera till vidarebefordran på serversidan. Med vidarebefordran på serversidan kan du ta bort DIL (Audience Manager data collection code) och ersätta den med [Audience Management Module](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/audience-management-module.html). Mer information finns i dokumentationen [för vidarebefordran på](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/server-side-forwarding/ssf.html) serversidan.

Migrering till vidarebefordran på serversidan kräver planering och samordning. Detta innebär externa ändringar av webbplatskoden och interna åtgärder som Adobe måste vidta för att etablera ditt konto. Många av dessa migreringsprocedurer måste faktiskt ske parallellt och släppas ut tillsammans. Din implementeringsväg ska följa den här händelsesekvensen:

1. Arbeta med dina [!DNL Analytics] och [!DNL Audience Manager] kontakters kontaktpersoner för att planera migreringen av din ID-tjänst och vidarebefordran på serversidan. Gör det viktigt att välja en spårningsserver i den här planen.

1. Fyll i formuläret på webbplatsen [för](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=X8SVES) integreringar och etableringar för att komma igång.

1. Implementera ID-tjänsten och [!DNL Audience Management Module] samtidigt. För att [!DNL Audience Management Module] (vidarebefordran på serversidan) och ID-tjänsten ska fungera på rätt sätt måste de släppas för samma uppsättning sidor och samtidigt.

## Steg 2: Hämta ID-tjänstkoden {#section-0780126cf43e4ad9b6fc5fe17bb3ef86}

ID-tjänsten kräver `VisitorAPI.js` kodbiblioteket. Så här hämtar du det här kodbiblioteket:

1. Gå till **[!UICONTROL Admin]** > **[!UICONTROL Code Manager]**.

1. I Kodhanteraren klickar du antingen **[!UICONTROL JavaScrpt (New)]** eller **[!UICONTROL JavaScript (Legacy)]**. Detta hämtar komprimerade kodbibliotek.

1. Dekomprimera kodfilen och öppna `VisitorAPI.js` filen.

## Steg 3: Lägg till funktionen Visitor.getInstance i ID-tjänstkoden {#section-9e30838b4d0741658a7a492153c49f27}

>[!IMPORTANT]
>
>* I tidigare versioner av ID-tjänstens API placerades den här funktionen på en annan plats och en annan syntax krävdes. Om du migrerar från en version som är tidigare än [version 1.4](../release-notes/notes-2015.md#section-f5c596f355b14da28f45c798df513572)bör du notera den nya placeringen och syntaxen som beskrivs här.
>* Kod i ALL CAPS är en platshållare för faktiska värden. Ersätt den här texten med ditt företags-ID, URL för spårningsserver eller annat namngivet värde.


**Del 1: Kopiera funktionen Visitor.getInstance nedan**

```js
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE", { 
     trackingServer: "INSERT-TRACKING-SERVER-HERE", // same as s.trackingServer 
     trackingServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE", // same as s.trackingServerSecure 
 
     // To enable CNAME support, add the following configuration variables 
     // If you are not using CNAME, DO NOT include these variables 
     marketingCloudServer: "INSERT-TRACKING-SERVER-HERE", 
     marketingCloudServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE" // same as s.trackingServerSecure 
}); 
```

**Del 2: Lägga till funktionskod i Visitor API.js-filen**

Placera `Visitor.getInstance` funktionen i slutet av filen efter kodblocket. Den redigerade filen ska se ut så här:

```js
/* 
========== DO NOT ALTER ANYTHING BELOW THIS LINE ========== 
Version and copyright section 
*/ 
 
// Visitor API code library section 
 
// Put Visitor.getInstance at the end of the file, after the code library 
 
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE", { 
     trackingServer: "INSERT-TRACKING-SERVER-HERE", // same as s.trackingServer 
     trackingServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE", // same as s.trackingServerSecure 
 
     // To enable CNAME support, add the following configuration variables 
     // If you are not using CNAME, DO NOT include these variables 
     marketingCloudServer: "INSERT-TRACKING-SERVER-HERE", 
     marketingCloudServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE" // same as s.trackingServerSecure 
}); 
```

## Steg 4: Lägg till ditt organisations-ID för Experience Cloud i Visitor.getInstance {#section-e2947313492546789b0c3b2fc3e897d8}

Ersätt `Visitor.getInstance` med ditt företags-ID i `INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE` funktionen. Om du inte känner till ditt organisations-ID kan du hitta det på administrationssidan för Experience Cloud. Den redigerade funktionen kan se ut ungefär som i exemplet nedan.

`var visitor = Visitor.getInstance("1234567ABC@AdobeOrg", { ...`

>[!IMPORTANT]
>
>*Ändra inte* skiftläget för tecknen i ditt företags-ID. ID:t är skiftlägeskänsligt och måste användas exakt som angivet.

## Steg 5: Lägg till dina spårningsservrar i Visitor.getInstance {#section-0dfc52096ac2427f86045aab9a0e0dfc}

Analytics använder spårningsservrar för datainsamling.

**Del 1: Hitta URL:er till spårningsservern**

Kontrollera dina `s_code.js` eller `AppMeasurement.js` filerna för att hitta spårningsserverns URL:er. Du vill att URL:erna som anges av dessa variabler ska vara:

* `s.trackingServer`
* `s.trackingServerSecure`

**Del 2: Ange spårningsservervariabler**

Så här tar du reda på vilka spårningsservervariabler som ska användas:

1. Besvara frågorna i beslutsmatrisen nedan. Använd de variabler som motsvarar dina svar.
1. Ersätt platshållarna för spårningsservern med URL:erna för spårningsservern.
1. Ta bort oanvända spårningsserver- och Experience Cloud-servervariabler från koden.

![](assets/tracking-server-matrix.png)

>[!NOTE]
>
>Om det används matchar du URL:erna för Experience Cloud-servern med deras motsvarande URL:er för spårningsservern så här:

* URL för Experience Cloud-server = URL för spårningsserver
* Säker URL för Experience Cloud-server = spårningsserverns säkra URL

Om du är osäker på hur du hittar spårningsservern kan du läsa [Vanliga frågor](../faq-intro/faq.md) och [Korrekt fylla i variablerna](https://helpx.adobe.com/analytics/kb/determining-data-center.html#)trackingServer och trackingServerSecure.

## Steg 6: Uppdatera filen AppMeasurement.js {#section-5517e94a09bc44dfb492ebca14b43048}

Det här steget kräver [!UICONTROL AppMeasurement]. Du kan inte fortsätta om du fortfarande använder s_code.

Lägg till den `Visitor.getInstance` funktion som visas nedan i `AppMeasurement.js` filen. Placera den i det avsnitt som innehåller konfigurationer som `linkInternalFilters`, `charSet`, `trackDownloads`osv. :

`s.visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE");`

>[!IMPORTANT]
>
>Nu bör du ta bort [!DNL Audience Manager] DIL-koden och ersätta den med Audience Management Module. Mer information finns i [Implementera vidarebefordran](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/server-side-forwarding/ssf.html) på serversidan.

***(Valfritt, men rekommenderas)*Skapa en anpassad förinställning **

Ange en anpassad propp i `AppMeasurement.js` för att mäta täckning. Lägg till den här anpassade proppen till `doPlugins` funktionen för din `AppMeasurement.js` fil:

```js
// prop1 is used as an example only. Choose any available prop. 
s.prop1 = (typeof(Visitor) != "undefined" ? "VisitorAPI Present" : "VisitorAPI Missing");
```

## Steg 7: Lägg till besökar-API-kod på sidan {#section-c2bd096a3e484872a72967b6468d3673}

Placera ` [!UICONTROL VisitorAPI.js]` filen i `<head>` taggarna på varje sida. När du skickar `VisitorAPI.js` filen till sidan:

* Placera det i början av avsnittet så att det visas före andra lösningstaggar. `<head>`
* Det måste köras före AppMeasurement och koden för andra [!DNL Experience Cloud] lösningar.

## Steg 8: (Valfritt) Konfigurera en respitperiod {#section-aceacdb7d5794f25ac6ff46f82e148e1}

Om något av dessa fall gäller din situation ber du [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) att skapa en tillfällig [respitperiod](../reference/analytics-reference/grace-period.md). Gränsperioder kan vara upp till 180 dagar. Du kan förnya en respitperiod om det behövs.

**Partiell implementering**

Du behöver en respitperiod om du har sidor som använder ID-tjänsten och vissa sidor som inte gör det, och de alla rapporterar till samma Analytics-rapportserie. Det här är vanligt om du har en global rapportserie som rapporterar över domäner.

Avbryt respitperioden när ID-tjänsten har distribuerats på alla dina webbsidor som rapporterar till samma rapportsvit.

**s_vi Cookie-krav**

Du behöver en respitperiod om du kräver att nya besökare ska ha en s_vi-cookie efter migrering till ID-tjänsten. Detta är vanligt om implementeringen läser s_vi-cookien och lagrar den i en variabel.

Avbryt respitperioden när implementeringen kan hämta MID i stället för att läsa s_vi-cookien.

Se även [Cookies och Experience Cloud Identity Service](../introduction/cookies.md).

**Integrering av Clickstream-data**

Du behöver en respitperiod om du skickar data till ett internt system från en Clickstream-datafeed och som bearbetar använder kolumnerna `visid_high` och `visid_low` .

Avbryt respitperioden efter att dataöverföringsprocessen kan använda kolumnerna `post_visid_high` och `post_visid_low` .

Se även [Referens](https://docs.adobe.com/content/help/en/analytics/export/analytics-data-feed/data-feed-overview.html)för Clickstream-datakolumnen.

## Steg 9: Testa och distribuera ID-tjänstkod {#section-f857542bfc70496dbb9f318d6b3ae110}

Du kan testa och distribuera enligt följande.

**Testa och verifiera**

Om du vill testa implementeringen av din ID-tjänst ska du kontrollera följande:

* [AMCV-cookie](../introduction/cookies.md) i den domän där sidorna finns.
* MID-värde i Analytics-bildbegäran med [Adobe-felsökaren](https://docs.adobe.com/content/help/en/analytics/implementation/validate/debugger.html).
* Se även [Testa och verifiera Experience Cloud Identity Service](../implementation-guides/test-verify.md).

Information om hur du verifierar vidarebefordran på serversidan finns i [Så här verifierar du implementeringen](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/server-side-forwarding/ssf-verify.html)av vidarebefordran på serversidan.

**Distribuera**

Distribuera koden när den har testats.

Om du aktiverade en respitperiod:

* Kontrollera att Analytics-id (AID) och MID finns i bildbegäran.
* Kom ihåg att inaktivera fristen när du uppfyller villkoren för att avbryta prenumerationen.

