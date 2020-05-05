---
description: getInstance returnerar ett besökar-ID-objekt för angivet Experience Cloud-organisations-ID. Detta krävs för att initiera det besökar-ID-objekt som tillhandahålls AppMeasurement via s.visitor.
keywords: ID Service
seo-description: getInstance returnerar ett besökar-ID-objekt för angivet Experience Cloud-organisations-ID. Detta krävs för att initiera det besökar-ID-objekt som tillhandahålls AppMeasurement via s.visitor.
seo-title: getInstance
title: getInstance
uuid: 259b88a6-e3d0-4aab-b935-566099bdab98
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# getInstance{#getinstance}

getInstance returnerar ett besökar-ID-objekt för angivet Experience Cloud-organisations-ID. Detta krävs för att initiera det besökar-ID-objekt som tillhandahålls AppMeasurement via s.visitor.

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
>*Instansiera inte* Visitor-funktionen med `var visitor = new Visitor`. Du måste använda rätt funktionsanrop som beskrivs här. Gäller för [!UICONTROL VisitorAPI.js] -kodbiblioteket v3.0 eller senare.

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

Om `getInstance` inte hittar någon befintlig instans skapas en ny instans och returneras. Detta liknar den [ i `s_gi()` . ](https://docs.adobe.com/content/help/en/analytics/implementation/vars/functions/s-gi.html) Funktionen [!DNL AppMeasurement]i.

**Vanlig användning**

ID-tjänstens [!DNL Experience Cloud] API innehåller en lista över alla instanser som skapats för varje [!DNL Adobe Experience Cloud] organisations-ID. Om programmet som använder ID-tjänstens API inte skickar runt en referens till instansen kan instansen hittas genom att anropa den `getInstance` i stället för att skapa en ny. Detta ger även stöd för flera instanser för olika organisationer på samma webbsida eller i samma program.

Detta är användbart för program som inte har en klar `init` fas, men som måste anropa ID-tjänstens API på flera ställen. Du kan anropa `getInstance` på alla dessa platser och instansen skapas av den första som körs. Den befintliga instansen returneras av efterföljande anrop.
