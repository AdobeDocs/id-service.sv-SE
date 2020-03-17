---
description: Dessa instruktioner är till för målkunder som vill använda Experience Cloud Identity Service och inte använder dynamisk tagghantering (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
keywords: ID Service
seo-description: Dessa instruktioner är till för målkunder som vill använda Experience Cloud Identity Service och inte använder dynamisk tagghantering (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
seo-title: Implementera Experience Cloud Identity Service för Target
title: Implementera Experience Cloud Identity Service för Target
uuid: cb3581fa-4c4b-43aa-bb8e-8db85a6a1ef2
translation-type: tm+mt
source-git-commit: f7f23d89649a888f5e9d8c94526b550fbda7045b

---


# Implementera Experience Cloud Identity Service för Target{#implement-the-experience-cloud-id-service-for-target}

Dessa instruktioner är till för målkunder som vill använda Experience Cloud Identity Service och inte använder dynamisk tagghantering (DTM). Vi rekommenderar dock starkt att du använder DTM för att implementera ID-tjänsten. DTM effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.

>[!IMPORTANT]
>
>* [Läs kraven](../reference/requirements.md) innan du börjar.
>* Konfigurera och testa koden i en utvecklingsmiljö innan den implementeras i produktionen.
>



## Steg 1: Hämta ID-tjänstkoden {#section-b32ba0548aa546a79dd38be59832a53e}

Kodbiblioteket [!UICONTROL ID Service] kräver `VisitorAPI.js` kodbiblioteket. Kontakta [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) för att få den här koden.

## Steg 2: Lägg till funktionen Visitor.getInstance i ID-tjänstkoden {#section-287ef2958e9f43858fe9d630ae519e22}

**Del 1: Kopiera funktionen Visitor.getInstance nedan**

```js
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE"); 
```

**Del 2: Lägga till funktionskod i filen VisitorAPI.js**

Placera `Visitor.getInstance` funktionen i slutet av filen efter kodblocket. Den redigerade filen ska se ut så här:

```js
/* 
========== DO NOT ALTER ANYTHING BELOW THIS LINE ========== 
Version and copyright section 
*/ 
 
// Visitor API code library section 
 
// Put Visitor.getInstance at the end of the file, after the code library 
 
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE");
```

## Steg 3: Lägg till ditt Experience Cloud-organisations-ID i Visitor.getInstance {#section-522b1877be9243c39b222859b821f0ce}

Ersätt `Visitor.getInstance` med ditt `INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE` organisations-ID i [!DNL Experience Cloud] funktionen. Om du inte känner till ditt organisations-ID kan du hitta det på [!DNL Experience Cloud] administrationssidan. Se även [Administration - bastjänster](https://marketing.adobe.com/resources/help/en_US/mcloud/admin_getting_started.html). Den redigerade funktionen kan se ut ungefär som i exemplet nedan.

`var visitor = Visitor.getInstance("1234567ABC@AdobeOrg");`

>[!IMPORTANT]
>
>*Ändra inte* skiftläget för tecknen i ditt företags-ID. ID:t är skiftlägeskänsligt och måste användas exakt som angivet.

## Steg 4: Lägg till API-kod för besökare på sidan {#section-02d8dd7678b64a85b5abc1c4ef0845dd}

Distribuera `VisitorAPI.js` filen till platsen i `<head>` -taggarna före referensen till `mbox.js` filen. ID- [!DNL Experience Cloud] tjänsten måste köras innan det första [!DNL Target] nätverksanropet genereras. Flytta koden till produktion efter testning och verifiering.

## Steg 5: Testa och distribuera ID-tjänstkod {#section-e81ee439bb8a4c2abea43d76f3112e9c}

Du kan testa och distribuera enligt följande.

**Testa och verifiera**

Så här testar du implementeringen av din ID-tjänst:

* Kontrollera om det finns en AMCV-cookie i domänen där sidan finns.
* Kontrollera `mboxMCGVID` att det finns ett ID ( [!DNL Target] MID) i din [!DNL Experience Cloud] begäran.

Se [Cookies och Experience Cloud Identity Service](../introduction/cookies.md) för information om AMCV-cookien och MID.

**Distribuera**

Distribuera koden när den har testats.
