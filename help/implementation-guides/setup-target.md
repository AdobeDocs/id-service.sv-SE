---
description: Dessa instruktioner är till för målkunder som vill använda Experience Cloud Identity Service och som inte använder datainsamlingstaggar. Vi rekommenderar dock att du använder taggar för att implementera ID-tjänsten. Taggar effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.
keywords: ID-tjänst
title: Implementera identitetstjänsten Experience Cloud för Target
exl-id: 7a387e98-c8fc-4904-942a-be5e527eada2
source-git-commit: 792fb5d5192843f345577a99b6179fb6d95fedc0
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Implementera identitetstjänsten Experience Cloud för Target{#implement-the-experience-cloud-id-service-for-target}

De här instruktionerna är till för målkunder som vill använda Experience Cloud Identity Service och som inte använder [datainsamlingstaggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv-SE). Vi rekommenderar dock att du använder taggar för att implementera ID-tjänsten. Taggar effektiviserar implementeringsarbetsflödet och säkerställer automatiskt korrekt kodplacering och sekvensering.

>[!IMPORTANT]
>
>* [Läs kraven](../reference/requirements.md) innan du börjar.
>* Konfigurera och testa koden i en utvecklingsmiljö innan den implementeras i produktionen.

## Steg 1: Hämta ID-tjänstkoden {#section-b32ba0548aa546a79dd38be59832a53e}

[!UICONTROL ID Service] kräver kodbiblioteket `VisitorAPI.js`. Kontakta [kundtjänst](https://helpx.adobe.com/se/marketing-cloud/contact-support.html) om du vill hämta den här koden.

## Steg 2: Lägg till funktionen Visitor.getInstance i ID-tjänstkoden {#section-287ef2958e9f43858fe9d630ae519e22}

**Del 1: Kopiera funktionen Visitor.getInstance nedan**

```js
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE"); 
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
 
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE");
```

## Steg 3: Lägg till ditt organisations-ID för Experience Cloud i Visitor.getInstance {#section-522b1877be9243c39b222859b821f0ce}

Ersätt `INSERT-MARKETING-CLOUD-ORGANIZATION ID-HERE` med ditt [!DNL Experience Cloud]-organisations-ID i funktionen `Visitor.getInstance`. Om du inte känner till ditt organisations-ID kan du hitta det på administrationssidan för [!DNL Experience Cloud]. Se även [Administration - bastjänster](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/admin-getting-started.html?lang=sv-SE). Den redigerade funktionen kan se ut ungefär som i exemplet nedan.

`var visitor = Visitor.getInstance("1234567ABC@AdobeOrg");`

>[!IMPORTANT]
>
>*Ändra inte skiftläget för tecknen i ditt organisations-ID.* ID:t är skiftlägeskänsligt och måste användas exakt som angivet.

## Steg 4: Lägg till API-kod för besökare på sidan {#section-02d8dd7678b64a85b5abc1c4ef0845dd}

Distribuera filen `VisitorAPI.js` till din plats i taggarna `<head>` före referensen till filen `mbox.js`. ID-tjänsten [!DNL Experience Cloud] måste köras innan det första [!DNL Target]-nätverksanropet genereras. Flytta koden till produktion efter testning och verifiering.

## Steg 5: Testa och distribuera ID-tjänstkoden {#section-e81ee439bb8a4c2abea43d76f3112e9c}

Du kan testa och distribuera enligt följande.

**Testa och verifiera**

Så här testar du implementeringen av din ID-tjänst:

* Kontrollera om det finns en AMCV-cookie i domänen där sidan finns.
* Kontrollera att `mboxMCGVID` visas i din [!DNL Target]-begäran och att den innehåller [!DNL Experience Cloud]-ID:t (MID).

Mer information om AMCV-cookien och MID finns i [Cookies och Experience Cloud Identity Service](../introduction/cookies.md).

**Distribuera**

Distribuera koden när den har testats.
