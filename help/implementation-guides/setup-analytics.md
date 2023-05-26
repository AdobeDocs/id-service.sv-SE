---
description: Dessa instruktioner är till för Analytics-kunder som vill använda Experience Cloud Identity Service och inte använder Dynamic Tag Management (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
keywords: ID-tjänst
title: Implementera Experience Cloud Identity Service för analys
exl-id: c0271e49-32e5-49ee-bb11-548751ccafad
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Implementera Experience Cloud Identity Service för analys {#implement-the-experience-cloud-id-service-for-analytics}

Dessa instruktioner är till för Analytics-kunder som vill använda Experience Cloud Identity Service och inte använder Dynamic Tag Management (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.

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

The [!UICONTROL ID Service] kräver `VisitorAPI.js` kodbibliotek. Så här hämtar du det här kodbiblioteket:

1. Gå till **[!UICONTROL Admin]** > **[!UICONTROL Code Manager]**.
1. I [!UICONTROL Code Manager]klickar du på antingen **[!UICONTROL JavaScript (New)]** eller **[!UICONTROL JavaScript (Legacy)]**.

   Detta hämtar komprimerade kodbibliotek.

1. Dekomprimera kodfilen och öppna `VisitorAPI.js` -fil.

## Steg 2. Lägg till funktionen Visitor.getInstance i ID-tjänstkoden {#section-6053a6b7c16c466a9f9fdbf9cb9db3df}

>[!IMPORTANT]
>
>* I tidigare versioner av ID-tjänstens API placerades den här funktionen på en annan plats och en annan syntax krävdes. Om du migrerar från en version som är tidigare [version 1.4](../release-notes/notes-2015.md#section-f5c596f355b14da28f45c798df513572), notera den nya placeringen och syntaxen som beskrivs här.
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

**Del 2: Lägga till funktionskod i filen VisitorAPI.js**

Placera `Visitor.getInstance` i slutet av filen efter kodblocket. Den redigerade filen ska se ut så här:

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

I `Visitor.getInstance` funktion, ersätt `INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE` med [!DNL Experience Cloud] organisations-ID. Om du inte känner till ditt organisations-ID kan du hitta det på [!DNL Experience Cloud] administrationssida. Se även [Administration - bastjänster](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/admin-getting-started.html). Den redigerade funktionen kan se ut ungefär som i exemplet nedan.

`var visitor = Visitor.getInstance("1234567ABC@AdobeOrg", { ...`

>[!IMPORTANT]
>
>*Gör inte* ändra skiftläget för tecknen i ditt organisations-ID. ID:t är skiftlägeskänsligt och måste användas exakt som angivet.

## Steg 4: Lägg till dina spårningsservrar i Visitor.getInstance {#section-70ec9ebff47940d8ab520be5ec4728c5}

Spårningsservrar används för [!DNL Analytics] datainsamling.

**Del 1: Hitta URL:er till spårningsservern**

Kontrollera `s_code.js` eller `AppMeasurement.js` filer för att hitta spårningsserverns URL:er. Du vill att URL:erna som anges av dessa variabler ska vara:

* `s.trackingServer`
* `s.trackingServerSecure`

**Del 2: Ange spårningsservervariabler**

Så här tar du reda på vilka spårningsservervariabler som ska användas:

1. Besvara frågorna i beslutsmatrisen nedan. Använd de variabler som motsvarar dina svar.
1. Ersätt platshållarna för spårningsservern med URL:erna för spårningsservern.
1. Ta bort oanvänd spårningsserver och [!DNL Experience Cloud] servervariabler från koden.

![](assets/tracking-server-matrix.png)

>[!NOTE]
>
>Om det används matchar du [!DNL Experience Cloud] server-URL:er till deras motsvarande spårningsserver-URL:er enligt följande:
>
>* [!DNL Experience Cloud] server-URL = URL för spårningsserver
>* [!DNL Experience Cloud] säker URL för server = spårningsserverns säkra URL


Om du är osäker på hur du hittar spårningsservern kan du läsa [Vanliga frågor](../faq-intro/faq.md) och [Fylla i variablerna trackingServer och trackingServerSecure korrekt](https://helpx.adobe.com/analytics/kb/determining-data-center.html#).

## Steg 5: Uppdatera filen AppMeasurement.js eller s_code.js {#section-b53113aea1bd4de896e0e4e9a7edee19}

Lägg till den här funktionen i `AppMeasurement.js` eller `s_code.js` fil:

`s.visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE");`

Placera koden i samma avsnitt som innehåller konfigurationer som `linkInternalFilters`, `charSet`, `trackDownloads`, osv.

***(Valfritt men rekommenderas)* Skapa en anpassad egenskap **

Ange en anpassad svällning i `AppMeasurement.js` eller `s_code.js` för att mäta täckningen. Lägg till den här anpassade sviten i `doPlugins` din `AppMeasurement.js` eller `s_code.js` filer:

```js
// prop1 is used as an example only. Choose any available prop. 
s.prop1 = (typeof(Visitor) != "undefined" ? "VisitorAPI Present" : "VisitorAPI Missing");
```

## Steg 6: Lägg till API-kod för besökare på sidan {#section-d46d6aa324c842f2931d901e38d6db1d}

Placera `VisitorAPI.js` i `<head>` -taggar på varje sida. När du `VisitorAPI.js` till din sida:

* Placera den i början av `<head>` -avsnittet visas före andra lösningstaggar.
* Den måste köras före AppMeasurement och koden för andra [!DNL Experience Cloud] lösningar.

Flytta koden till produktion efter testning och verifiering.

## Steg 7: (Valfritt) Konfigurera en respitperiod {#section-7bbb2f72c26e4abeb8881e18366797a3}

Om något av dessa fall gäller din situation, fråga [Kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) för att konfigurera en temporär [respitperiod](../reference/analytics-reference/grace-period.md). Gränsperioder kan vara upp till 180 dagar. Du kan förnya en respitperiod om det behövs.

**Partiell implementering**

Du behöver en respitperiod om du har sidor som använder ID-tjänsten och vissa sidor som inte gör det, och de alla rapporterar till samma [!DNL Analytics] rapportsvit. Det här är vanligt om du har en global rapportserie som rapporterar över domäner.

Avbryt respitperioden när ID-tjänsten har distribuerats på alla dina webbsidor som rapporterar till samma rapportsvit.

**s_vi Cookie-krav**

Du behöver en respitperiod om du kräver att nya besökare ska ha en s_vi-cookie efter migrering till ID-tjänsten. Detta är vanligt om implementeringen läser s_vi-cookien och lagrar den i en variabel.

Avbryt respitperioden när implementeringen kan hämta MID i stället för att läsa s_vi-cookien.

Se, [Cookies och Experience Cloud Identity Service](../introduction/cookies.md).

Du behöver en frist om du skickar data till ett internt system från en datafeed i Clickstream och som bearbetar använder `visid_high` och `visid_low` kolumner.

Avbryt respitperioden efter att dataöverföringsprocessen kan använda `post_visid_high` och `post_visid_low` kolumner.

Se, [Referens för Clickstream-datakolumn](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-overview.html).

**Inmatning av data i Clickstream**

## Steg 8: Testa och distribuera ID-tjänstkod {#section-e9c1764ac21a4ec5be1ff338c0e2e01b}

Du kan testa och distribuera enligt följande.

**Testa och verifiera**

Om du vill testa implementeringen av din ID-tjänst ska du kontrollera följande:

* [AMCV cookie](../introduction/cookies.md) i domänen där sidan finns.
* MID-värde i [!DNL Analytics] bildförfrågan med [Felsökningsverktyget för Adobe](https://experienceleague.adobe.com/docs/analytics/implementation/validate/debugger.html).

Se, [Testa och verifiera Experience Cloud Identity Service](../implementation-guides/test-verify.md).

**Distribuera kod**

Distribuera koden när den har testats.

Om du aktiverat en respitperiod i [Steg 7](../implementation-guides/setup-analytics.md#section-7bbb2f72c26e4abeb8881e18366797a3):

* Se till att [!DNL Analytics] ID (AID) och MID finns i bildbegäran.
* Kom ihåg att inaktivera fristen när du uppfyller villkoren för att avbryta prenumerationen.
