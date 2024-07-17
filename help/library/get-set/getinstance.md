---
description: getInstance returnerar ett besökar-ID-objekt för angivet Experience Cloud-organisations-ID. Detta krävs för att initiera det besökar-ID-objekt som tillhandahålls AppMeasurementet via s.visitor.
keywords: ID-tjänst
title: getInstance
exl-id: 4941cf51-a8d0-4796-a102-4cd13cd5574d
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# getInstance{#getinstance}

getInstance returnerar ett besökar-ID-objekt för angivet Experience Cloud-organisations-ID. Detta krävs för att initiera det besökar-ID-objekt som tillhandahålls AppMeasurementet via s.visitor.

**Syntax**

**JavaScript**

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

>[!CAUTION]
>
>*Instansiera inte* besökarfunktionen med `var visitor = new Visitor`. Du måste använda rätt funktionsanrop som beskrivs här. Gäller för [!UICONTROL VisitorAPI.js]-kodbiblioteket v3.0 eller senare.

**ActionScript/Flash**

```js
import com.adobe.mc.Visitor; 
... 
var visitor = Visitor.getInstance("INSERT-MARKETING-CLOUD-ORGANIZATION-ID-HERE", { 
     trackingServer: "INSERT-TRACKING-SERVER-HERE", // same as s.trackingServer 
     trackingServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE", // same as s.trackingServerSecure 
 
     // To enable CNAME support, add the following configuration variables 
     // If you are not using CNAME, DO NOT include these variables 
     marketingCloudServer: "INSERT-TRACKING-SERVER-HERE", 
     marketingCloudServerSecure: "INSERT-SECURE-TRACKING-SERVER-HERE" // same as s.trackingServerSecure 
});
```

Om `getInstance` inte hittar någon befintlig instans skapas en ny instans och returneras. Detta liknar funktionen [`s_gi()` ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/s-gi.html) i [!DNL AppMeasurement].

**Vanlig användning**

ID-tjänste-API:t för [!DNL Experience Cloud] upprätthåller en lista över alla instanser som skapats för varje [!DNL Adobe Experience Cloud] organisation-ID. Om programmet som använder ID-tjänstens API inte skickar runt en referens till instansen kan instansen hittas genom att anropa `getInstance` i stället för att skapa en ny. Detta ger även stöd för flera instanser för olika organisationer på samma webbsida eller i samma program.

Detta är användbart för program som inte har en klar `init`-fas, men som måste anropa ID-tjänstens API på flera platser. Du kan anropa `getInstance` på alla dessa platser, och den första som körs skapar instansen. Den befintliga instansen returneras av efterföljande anrop.
