---
description: getInstance returnerar ett besökar-ID-objekt för det angivna Experience Cloud-organisations-ID:t. Detta krävs för att initiera det besökar-ID-objekt som tillhandahålls AppMeasurement via s.visitor.
keywords: ID-tjänst
title: getInstance
exl-id: 4941cf51-a8d0-4796-a102-4cd13cd5574d
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# getInstance{#getinstance}

getInstance returnerar ett besökar-ID-objekt för det angivna Experience Cloud-organisations-ID:t. Detta krävs för att initiera det besökar-ID-objekt som tillhandahålls AppMeasurement via s.visitor.

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
>*Gör inte* instansiera besökarfunktionen med `var visitor = new Visitor`. Du måste använda rätt funktionsanrop som beskrivs här. Gäller för [!UICONTROL VisitorAPI.js] kodbibliotek v3.0 eller senare.

**ActionScript / Flash**

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

If `getInstance` hittar inte en befintlig instans. En ny instans skapas och returneras. Detta liknar [ `s_gi()` function ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/s-gi.html) in [!DNL AppMeasurement].

**Vanlig användning**

The [!DNL Experience Cloud] ID-tjänste-API:t underhåller en lista över alla instanser som skapats för varje [!DNL Adobe Experience Cloud] organisations-ID. Om programmet som använder ID-tjänstens API inte skickar en referens till instansen kan instansen hittas genom att anropa `getInstance` i stället för att skapa en ny. Detta ger även stöd för flera instanser för olika organisationer på samma webbsida eller i samma program.

Detta är användbart för program som inte har en tydlig `init` men måste anropa ID-tjänstens API på flera platser. Du kan ringa `getInstance` på alla dessa platser och den första som körs skapar instansen. Den befintliga instansen returneras av efterföljande anrop.
