---
description: De här instruktionerna är till för Analytics- och Audience Manager-kunder som vill använda Experience Cloud Identity Service och som inte använder datainsamlingstaggar. Vi rekommenderar dock att du använder taggar för att implementera ID-tjänsten. Taggar effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
keywords: ID-tjänst
title: Implementera Experience Cloud Identity Service för Analytics och Audience Manager
exl-id: e31720a1-5c89-4084-88f6-443994dbb2f4
source-git-commit: 7ef084bc1add5a4ea8c7be738055b0c21e247eea
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Implementera Experience Cloud Identity Service för Analytics och Audience Manager{#implement-the-experience-cloud-id-service-for-analytics-and-audience-manager}

De här instruktionerna gäller för Analytics- och Audience Manager-kunder som vill använda Experience Cloud identitetstjänst och som inte använder [datainsamlingstaggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en). Vi rekommenderar dock att du använder taggar för att implementera ID-tjänsten. Taggar effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.

>[!IMPORTANT]
>
>* [Läs kraven](../reference/requirements.md) innan du börjar.
>* För den här proceduren krävs AppMeasurement. Kunder som använder s_code kan inte slutföra den här proceduren.
>* Konfigurera och testa koden i en utvecklingsmiljö innan den implementeras i produktionen.

## Steg 1: Planera för vidarebefordran på serversidan {#section-880797cc992d4755b29cada7b831f1fc}

Utöver de steg som beskrivs här bör kunder som använder [!DNL Analytics] och [!DNL Audience Manager] migrera till vidarebefordran på serversidan. Med vidarebefordran på serversidan kan du ta bort DIL (Audience Manager datainsamlingskod) och ersätta den med [Audience Management Module](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/audience-management-module.html). Mer information finns i [vidarebefordringsdokumentationen på serversidan](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/server-side-forwarding/ssf.html).

Migrering till vidarebefordran på serversidan kräver planering och samordning. Den här processen innebär externa ändringar av webbplatskoden och interna åtgärder som Adobe måste vidta för att etablera ditt konto. Många av dessa migreringsprocedurer måste faktiskt ske parallellt och släppas ut tillsammans. Din implementeringsväg ska följa den här händelsesekvensen:

1. Arbeta med dina [!DNL Analytics]- och [!DNL Audience Manager]-kontakter för att planera migreringen av din ID-tjänst och vidarebefordran på serversidan. Gör det viktigt att välja en spårningsserver i den här planen.

1. Fyll i formuläret på [integrerings- och provisioneringswebbplatsen](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=X8SVES) för att komma igång.

1. Implementera ID-tjänsten och [!DNL Audience Management Module] samtidigt. [!DNL Audience Management Module] (vidarebefordran på serversidan) och ID-tjänsten måste släppas för samma uppsättning sidor och samtidigt för att fungera korrekt.

## Steg 2: Hämta ID-tjänstkoden {#section-0780126cf43e4ad9b6fc5fe17bb3ef86}

ID-tjänsten kräver kodbiblioteket `VisitorAPI.js`. Så här hämtar du det här kodbiblioteket:

1. Gå till **[!UICONTROL Admin]** > **[!UICONTROL Code Manager]**.

1. Klicka på **[!UICONTROL JavaScrpt (New)]** eller **[!UICONTROL JavaScript (Legacy)]** i Kodhanteraren. Detta hämtar komprimerade kodbibliotek.

1. Dekomprimera kodfilen och öppna filen `VisitorAPI.js`.

## Steg 3: Lägg till funktionen Visitor.getInstance i ID-tjänstkoden {#section-9e30838b4d0741658a7a492153c49f27}

>[!IMPORTANT]
>
>* I tidigare versioner av ID-tjänstens API placerades den här funktionen på en annan plats och en annan syntax krävdes. Om du migrerar från en version som är äldre än [version 1.4](../release-notes/notes-2015.md#section-f5c596f355b14da28f45c798df513572) bör du notera den nya placeringen och syntaxen som beskrivs här.
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

**Del 2: Lägg till funktionskod i Visitor API.js-filen**

Placera funktionen `Visitor.getInstance` i slutet av filen efter kodblocket. Den redigerade filen ska se ut så här:

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

## Steg 4: Lägg till ditt Experience Cloud Organization ID i Visitor.getInstance {#section-e2947313492546789b0c3b2fc3e897d8}

Ersätt `Visitor.getInstance` med ditt Experience Cloud-organisations-ID i funktionen `INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE`. Om du inte känner till ditt företags-ID kan du hitta det på Experience Cloud administrationssida. Den redigerade funktionen kan se ut ungefär som i exemplet nedan.

`var visitor = Visitor.getInstance("1234567ABC@AdobeOrg", { ...`

>[!IMPORTANT]
>
>*Ändra inte skiftläget för tecknen i ditt organisations-ID.* ID:t är skiftlägeskänsligt och måste användas exakt som angivet.

## Steg 5: Lägg till dina spårningsservrar i Visitor.getInstance {#section-0dfc52096ac2427f86045aab9a0e0dfc}

Analytics använder spårningsservrar för datainsamling.

**Del 1: Hitta URL:er till spårningsservern**

Kontrollera dina `s_code.js`- eller `AppMeasurement.js`-filer för att hitta URL:er för spårningsservern. Du vill att URL:erna som anges av dessa variabler ska vara:

* `s.trackingServer`
* `s.trackingServerSecure`

**Del 2: Ange spårningsservervariabler**

Så här tar du reda på vilka spårningsservervariabler som ska användas:

1. Besvara frågorna i beslutsmatrisen nedan. Använd de variabler som motsvarar dina svar.
1. Ersätt platshållarna för spårningsservern med URL:erna för spårningsservern.
1. Ta bort oanvända spårningsservrar och Experience Cloud-servervariabler från koden.

![](assets/tracking-server-matrix.png)

>[!NOTE]
>
>Om det används matchar du URL:erna för Experience Cloud-servern med deras motsvarande URL:er för spårningsservern så här:

* URL för Experience Cloud-server = URL för spårningsserver
* Säker URL för Experience Cloud-server = spårningsserverns säkra URL

Om du är osäker på hur du hittar spårningsservern kan du läsa [Vanliga frågor](../faq-intro/faq.md) och [Fylla i variablerna trackingServer och trackingServerSecure](https://helpx.adobe.com/analytics/kb/determining-data-center.html#) korrekt.

## Steg 6: Uppdatera filen AppMeasurement.js {#section-5517e94a09bc44dfb492ebca14b43048}

Det här steget kräver [!UICONTROL AppMeasurement]. Du kan inte fortsätta om du fortfarande använder s_code.

Lägg till funktionen `Visitor.getInstance` som visas nedan i din `AppMeasurement.js`-fil. Placera den i avsnittet som innehåller konfigurationer som `linkInternalFilters`, `charSet`, `trackDownloads` osv.:

`s.visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE");`

>[!IMPORTANT]
>
>Nu bör du ta bort DIL-koden [!DNL Audience Manager] och ersätta den med Audience Management Module. Mer information finns i [Implementera vidarebefordran på serversidan](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html).

***(Valfritt, men rekommenderas)* Skapa en anpassad prop &#x200B;**

Ange en anpassad prop i `AppMeasurement.js` för att mäta täckning. Lägg till den här anpassade proppen i funktionen `doPlugins` i din `AppMeasurement.js`-fil:

```js
// prop1 is used as an example only. Choose any available prop. 
s.prop1 = (typeof(Visitor) != "undefined" ? "VisitorAPI Present" : "VisitorAPI Missing");
```

## Steg 7: Lägg till API-kod för besökare på sidan {#section-c2bd096a3e484872a72967b6468d3673}

Placera `[!UICONTROL VisitorAPI.js]`-filen i `<head>` -taggarna på varje sida. När du skickar filen `VisitorAPI.js` till sidan:

* Placera det i början av avsnittet `<head>` så att det visas före andra lösningstaggar.
* Den måste köras före AppMeasurement och koden för andra [!DNL Experience Cloud]-lösningar.

## Steg 8: (Valfritt) Konfigurera en respitperiod {#section-aceacdb7d5794f25ac6ff46f82e148e1}

Om något av dessa användningsfall gäller din situation ber du [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) att ställa in en tillfällig [respitperiod](../reference/analytics-reference/grace-period.md). Gränsperioder kan vara upp till 180 dagar. Du kan förnya en respitperiod om det behövs.

**Partiell implementering**

Du behöver en respitperiod om du har sidor som använder ID-tjänsten och vissa sidor som inte gör det, och de alla rapporterar till samma Analytics-rapportserie. Det här är vanligt om du har en global rapportserie som rapporterar över domäner.

Avbryt respitperioden när ID-tjänsten har distribuerats på alla dina webbsidor som rapporterar till samma rapportsvit.

**s_vi Cookie-krav**

Du behöver en respitperiod om du kräver att nya besökare ska ha en s_vi-cookie efter migrering till ID-tjänsten. Detta är vanligt om implementeringen läser s_vi-cookien och lagrar den i en variabel.

Avbryt respitperioden när implementeringen kan hämta MID i stället för att läsa s_vi-cookien.

Se även [Cookies och Experience Cloud Identity Service](../introduction/cookies.md).

**Integrering av Clickstream-data**

Du behöver en respitperiod om du skickar data till ett internt system från en Clickstream-datafeed och som bearbetar använder kolumnerna `visid_high` och `visid_low`.

Avbryt respitperioden efter att dataöverföringsprocessen kan använda kolumnerna `post_visid_high` och `post_visid_low`.

Se även [Referens för Clickstream-datakolumn](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-overview.html).

## Steg 9: Testa och distribuera ID-tjänstkoden {#section-f857542bfc70496dbb9f318d6b3ae110}

Du kan testa och distribuera enligt följande.

**Testa och verifiera**

Om du vill testa implementeringen av din ID-tjänst ska du kontrollera följande:

* [AMCV-cookie](../introduction/cookies.md) i domänen där du har sidor.
* MID-värde i Analytics-bildbegäran med [Adobe-felsökaren](https://experienceleague.adobe.com/docs/analytics/implementation/validate/debugger.html).
* Se även [Testa och verifiera Experience Cloud identitetstjänst](../implementation-guides/test-verify.md).

Information om hur du verifierar vidarebefordran på serversidan finns i [Så här verifierar du implementeringen av vidarebefordran på serversidan](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf-verify.html).

**Distribuera**

Distribuera koden när den har testats.

Om du aktiverade en respitperiod:

* Kontrollera att Analytics ID (AID) och MID finns i bildbegäran.
* Kom ihåg att inaktivera fristen när du uppfyller villkoren för att avbryta prenumerationen.
