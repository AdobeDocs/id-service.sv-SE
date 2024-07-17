---
description: Dessa instruktioner är till för Analytics-kunder som vill använda Experience Cloud Identity Service och som inte använder datainsamlingstaggar. Vi rekommenderar dock att du använder taggar för att implementera ID-tjänsten. Taggar effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
keywords: ID-tjänst
title: Implementera Experience Cloud Identity Service för analys
exl-id: c0271e49-32e5-49ee-bb11-548751ccafad
source-git-commit: 792fb5d5192843f345577a99b6179fb6d95fedc0
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Implementera Experience Cloud Identity Service för analys {#implement-the-experience-cloud-id-service-for-analytics}

De här instruktionerna är till för Analytics-kunder som vill använda Experience Cloud Identity Service och som inte använder [datainsamlingstaggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en). Vi rekommenderar dock att du använder taggar för att implementera ID-tjänsten. Taggar effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.

>[!IMPORTANT]
>
>* [Läs kraven](../reference/requirements.md) innan du börjar.
>* Konfigurera och testa koden i en utvecklingsmiljö innan den implementeras i produktionen.

Så här implementerar du ID-tjänsten för Adobe Analytics:

1. [Hämta ID-tjänstkoden](../implementation-guides/setup-analytics.md#section-ead9403a6b7e45b887f9ac959ef89f7f)
1. [Lägg till funktionen Visitor.getInstance i ID-tjänstkoden](../implementation-guides/setup-analytics.md#section-6053a6b7c16c466a9f9fdbf9cb9db3df)
1. [Lägg till ditt organisations-ID för Experience Cloud i Visitor.getInstance](../implementation-guides/setup-analytics.md#section-7b8a6e76dc124d0e9ab1ce96ab2ffb0e)
1. [Lägg till dina spårningsservrar i Visitor.getInstance](../implementation-guides/setup-analytics.md#section-70ec9ebff47940d8ab520be5ec4728c5)
1. [Uppdatera filen AppMeasurement.js eller s_code.js](../implementation-guides/setup-analytics.md#section-b53113aea1bd4de896e0e4e9a7edee19)
1. [Lägg till API-kod för besökare på sidan](../implementation-guides/setup-analytics.md#section-d46d6aa324c842f2931d901e38d6db1d)
1. [(Valfritt) Konfigurera en respitperiod](../implementation-guides/setup-analytics.md#section-7bbb2f72c26e4abeb8881e18366797a3)
1. [Testa och distribuera ID-tjänstkod](../implementation-guides/setup-analytics.md#section-e9c1764ac21a4ec5be1ff338c0e2e01b)

## Steg 1: Hämta ID-tjänstkoden {#section-ead9403a6b7e45b887f9ac959ef89f7f}

[!UICONTROL ID Service] kräver kodbiblioteket `VisitorAPI.js`. Så här hämtar du det här kodbiblioteket:

1. Gå till **[!UICONTROL Admin]** > **[!UICONTROL Code Manager]**.
1. I [!UICONTROL Code Manager] klickar du antingen på **[!UICONTROL JavaScript (New)]** eller **[!UICONTROL JavaScript (Legacy)]**.

   Detta hämtar komprimerade kodbibliotek.

1. Dekomprimera kodfilen och öppna filen `VisitorAPI.js`.

## Steg 2. Lägg till funktionen Visitor.getInstance i ID-tjänstkoden {#section-6053a6b7c16c466a9f9fdbf9cb9db3df}

>[!IMPORTANT]
>
>* I tidigare versioner av ID-tjänstens API placerades den här funktionen på en annan plats och en annan syntax krävdes. Om du migrerar från en version som är äldre än [version 1.4](../release-notes/notes-2015.md#section-f5c596f355b14da28f45c798df513572) bör du notera den nya placeringen och syntaxen som beskrivs här.
>* Kod i ALL CAPS är en platshållare för faktiska värden. Ersätt den här texten med ditt företags-ID, URL för spårningsserver eller annat namngivet värde.

**Del 1: Kopiera funktionen Visitor.getInstance nedan**

```js
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION-ID-HERE", { 
     trackingServer: "INSERT-TRACKING-SERVER-HERE", // same as s.trackingServer 
     trackingServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE", // same as s.trackingServerSecure 
 
     // To enable CNAME support, add the following configuration variables 
     // If you are not using CNAME, DO NOT include these variables 
     marketingCloudServer: "INSERT-TRACKING-SERVER-HERE", 
     marketingCloudServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE" // same as s.trackingServerSecure 
}); 
```

**Del 2: Lägg till funktionskod i filen VisitorAPI.js**

Placera funktionen `Visitor.getInstance` i slutet av filen efter kodblocket. Den redigerade filen ska se ut så här:

```js
/* 
========== DO NOT ALTER ANYTHING BELOW THIS LINE ========== 
Version and copyright section 
*/ 
 
// Visitor API code library section 
 
// Put Visitor.getInstance at the end of the file, after the code library

var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION-ID-HERE", { 
     trackingServer: "INSERT-TRACKING-SERVER-HERE", // same as s.trackingServer 
     trackingServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE", // same as s.trackingServerSecure 
 
     // To enable CNAME support, add the following configuration variables 
     // If you are not using CNAME, DO NOT include these variables 
     marketingCloudServer: "INSERT-TRACKING-SERVER-HERE", 
     marketingCloudServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE" // same as s.trackingServerSecure 
}); 
```

## Steg 3: Lägg till ditt organisations-ID för Experience Cloud i Visitor.getInstance {#section-7b8a6e76dc124d0e9ab1ce96ab2ffb0e}

Ersätt `INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE` med ditt [!DNL Experience Cloud]-organisations-ID i funktionen `Visitor.getInstance`. Om du inte känner till ditt organisations-ID kan du hitta det på administrationssidan för [!DNL Experience Cloud]. Se även [Administration - bastjänster](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/admin-getting-started.html). Den redigerade funktionen kan se ut ungefär som i exemplet nedan.

`var visitor = Visitor.getInstance("1234567ABC@AdobeOrg", { ...`

>[!IMPORTANT]
>
>*Ändra inte skiftläget för tecknen i ditt organisations-ID.* ID:t är skiftlägeskänsligt och måste användas exakt som angivet.

## Steg 4: Lägg till dina spårningsservrar i Visitor.getInstance {#section-70ec9ebff47940d8ab520be5ec4728c5}

Spårningsservrar används för datainsamling [!DNL Analytics].

**Del 1: Hitta URL:er till spårningsservern**

Kontrollera dina `s_code.js`- eller `AppMeasurement.js`-filer för att hitta URL:er för spårningsservern. Du vill att URL:erna som anges av dessa variabler ska vara:

* `s.trackingServer`
* `s.trackingServerSecure`

**Del 2: Ange spårningsservervariabler**

Så här tar du reda på vilka spårningsservervariabler som ska användas:

1. Besvara frågorna i beslutsmatrisen nedan. Använd de variabler som motsvarar dina svar.
1. Ersätt platshållarna för spårningsservern med URL:erna för spårningsservern.
1. Ta bort oanvända spårningsservrar och [!DNL Experience Cloud] servervariabler från koden.

![](assets/tracking-server-matrix.png)

>[!NOTE]
>
>Om det används matchar du URL:erna för servern [!DNL Experience Cloud] med deras motsvarande URL:er för spårningsservern så här:
>
>* [!DNL Experience Cloud] server-URL = URL för spårningsserver
>* Skyddad URL för [!DNL Experience Cloud]-server = spårningsserverns säkra URL

Om du är osäker på hur du hittar spårningsservern kan du läsa [Vanliga frågor](../faq-intro/faq.md) och [Fylla i variablerna trackingServer och trackingServerSecure](https://helpx.adobe.com/analytics/kb/determining-data-center.html#) korrekt.

## Steg 5: Uppdatera filen AppMeasurement.js eller s_code.js {#section-b53113aea1bd4de896e0e4e9a7edee19}

Lägg till den här funktionen i din `AppMeasurement.js`- eller `s_code.js`-fil:

`s.visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE");`

Placera koden i samma avsnitt som innehåller konfigurationer som `linkInternalFilters`, `charSet`, `trackDownloads` osv.

***(Valfritt men rekommenderas)* Skapa en anpassad egenskap **

Ange en anpassad prop i `AppMeasurement.js` eller `s_code.js` för att mäta täckning. Lägg till den här anpassade proppen i funktionen `doPlugins` för dina `AppMeasurement.js`- eller `s_code.js`-filer:

```js
// prop1 is used as an example only. Choose any available prop. 
s.prop1 = (typeof(Visitor) != "undefined" ? "VisitorAPI Present" : "VisitorAPI Missing");
```

## Steg 6: Lägg till API-kod för besökare på sidan {#section-d46d6aa324c842f2931d901e38d6db1d}

Placera `VisitorAPI.js`-filen i `<head>` -taggarna på varje sida. När du skickar filen `VisitorAPI.js` till sidan:

* Placera det i början av avsnittet `<head>` så att det visas före andra lösningstaggar.
* Den måste köras före AppMeasurementet och koden för andra [!DNL Experience Cloud]-lösningar.

Flytta koden till produktion efter testning och verifiering.

## Steg 7: (Valfritt) Konfigurera en respitperiod {#section-7bbb2f72c26e4abeb8881e18366797a3}

Om något av dessa användningsfall gäller din situation ber du [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) att ställa in en tillfällig [respitperiod](../reference/analytics-reference/grace-period.md). Gränsperioder kan vara upp till 180 dagar. Du kan förnya en respitperiod om det behövs.

**Partiell implementering**

Du behöver en respitperiod om du har sidor som använder ID-tjänsten och vissa sidor som inte gör det, och de alla rapporterar till samma [!DNL Analytics]-rapportserie. Det här är vanligt om du har en global rapportserie som rapporterar över domäner.

Avbryt respitperioden när ID-tjänsten har distribuerats på alla dina webbsidor som rapporterar till samma rapportsvit.

**s_vi Cookie-krav**

Du behöver en respitperiod om du kräver att nya besökare ska ha en s_vi-cookie efter migrering till ID-tjänsten. Detta är vanligt om implementeringen läser s_vi-cookien och lagrar den i en variabel.

Avbryt respitperioden när implementeringen kan hämta MID i stället för att läsa s_vi-cookien.

Se [Cookies och Experience Cloud Identity Service](../introduction/cookies.md).

Du behöver en respitperiod om du skickar data till ett internt system från en Clickstream-datafeed och som bearbetar använder kolumnerna `visid_high` och `visid_low`.

Avbryt respitperioden efter att dataöverföringsprocessen kan använda kolumnerna `post_visid_high` och `post_visid_low`.

Mer information finns i [Referens för Clickstream-datakolumn](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-overview.html).

**Inmatning av data i Clickstream**

## Steg 8: Testa och distribuera ID-tjänstkoden {#section-e9c1764ac21a4ec5be1ff338c0e2e01b}

Du kan testa och distribuera enligt följande.

**Testa och verifiera**

Om du vill testa implementeringen av din ID-tjänst ska du kontrollera följande:

* [AMCV-cookie](../introduction/cookies.md) i domänen där sidan finns.
* MID-värde i bildbegäran [!DNL Analytics] med felsökningsverktyget [Adobe](https://experienceleague.adobe.com/docs/analytics/implementation/validate/debugger.html).

Se [Testa och verifiera identitetstjänsten Experience Cloud](../implementation-guides/test-verify.md).

**Distribuera kod**

Distribuera koden när den har testats.

Om du aktiverade en respitperiod i [steg 7](../implementation-guides/setup-analytics.md#section-7bbb2f72c26e4abeb8881e18366797a3):

* Kontrollera att [!DNL Analytics] ID (AID) och MID finns i bildbegäran.
* Kom ihåg att inaktivera fristen när du uppfyller villkoren för att avbryta prenumerationen.
