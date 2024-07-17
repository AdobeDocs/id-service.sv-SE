---
description: Den här funktionen är främst avsedd för A4T-kunder för att hjälpa till att lösa problem som rör arbete med ID:n på enstaka sidor/skärmar eller appar.
keywords: ID-tjänst
title: resetState
exl-id: 8e8cb299-bb89-4bc1-8841-3091ce0cbd81
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# resetState{#resetstate}

Den här funktionen är främst avsedd för A4T-kunder för att hjälpa till att lösa problem som rör arbete med ID:n på enstaka sidor/skärmar eller appar.

## Användningsfall {#section-840b88a5cdb042488b340cad5d7b22a5}

Som A4T-kund som använder ID-tjänsten kan du använda funktionen `visitor.resetState()` när du behöver:

* Om du vill skicka ett SDID (Additional Data ID), eller något annat ID, från en sida eller skärm till en annan via en omdirigering. I vanliga fall skickas inte ID-tjänsten detta ID utan den här funktionen.
* Använd kod som bara uppdaterar specifika avsnitt på en sida eller i en app via Ajax-anrop och du vill spåra dessa åtgärder. Anta att du har en sida där klickning på ett objekt bara laddar eller ändrar ett speciellt avsnitt. I det här fallet kan ID-tjänsten inte begära ett annat ID om inte sidan läses in igen. Med `visitor.resetState()` kan du dock begära ett nytt ID under dessa villkor.

Se kodexemplen nedan.

## Syntax {#section-9e63503e178f4be28ac850abf44d6d91}

**Syntax:** ` visitor.resetState( *`state`*);`

## Kodexempel {#section-d75b211bb4ea473887eb284de2ad838b}

Implementeringen av din ID-tjänst påverkar hur du använder funktionen. Se tabellen nedan för exempel.

**Implementering på serversidan**

En implementering på serversidan är för A4T-kunder med blandade implementeringar på server- och klientsidan av [!DNL Target], [!DNL Analytics] och ID-tjänsten. Om du har konfigurerat ID-tjänsten med den här metoden behöver du bara lägga till `visitor.resetState()` på sidan. Anrop till ID-tjänsten returnerar automatiskt ett nytt ID och servertillstånd.

**Icke-standardimplementering** (med ID)

Om du har konfigurerat ID-tjänsten med en [icke-standardimplementering](../../implementation-guides/implementation-guides.md#section-2c4f2db1f9704315a7cccab6d2e07113) måste du konfigurera ett variabelobjekt så att det innehåller det SDID (eller andra ID) som du vill skicka med `visitor.resetState()`. Som framgår nedan inkluderar detta ditt [organisations-ID](../../reference/requirements.md#section-a02f537129a64ffbb690d5738d360c26) och det ID som du vill skicka. Koden kan se ut ungefär som i följande exempel.

```js
//Instantiate server state variable 
var serverState = { 
     "Insert Experience Cloud organization ID here": { 
          //Specify the SDID or other ID 
          supplementalDataIDCurrent: "1234", 
          supplementalDataIDCurrentConsumed: { 
               "payload:top-center": false 
          } 
     } 
}; 
 
//Instantiate ID service 
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here", { 
     ... 
}); 
 
//Reset server state to pass the SDID 
visitor.resetState(serverState);
```

**Icke-standardimplementering** (utan att skicka ett ID)

I det här fallet kan `visitor.resetState()` användas för att generera ett nytt ID. Detta kan vara användbart i ett enkelsidigt program när en användare navigerar till en ny skärm utan att uppdatera sidan och du behöver ett nytt ID.

```js
 
//Instantiate ID service 
var visitor = Visitor.getInstance ("Insert Experience Cloud organization ID here", { 
     ... 
}); 
 
//Request a supplemental Data ID for consumer1 and consumer2: 
var sdid1 = visitor.getSupplementalDataID("consumer1"); // sdid1: 1234 
var sdid2 = visitor.getSupplementalDataID("consumer2"); // sdid2: 1234 
 
//User navigates to a new screen in a single-page app, without refreshing the page. 
//To reset the Supplemental Data ID internal, call resetState without passing any parameters. 
//This way we will not be recycling the `1234` ID anymore. Instead Visitor will generate a new supplemental Data ID going forward. 
visitor.resetState(); 
 
//Request a supplemental Data ID for consumer3 and consumer4: 
var sdid1 = visitor.getSupplementalDataID("consumer3"); // sdid1: 5678 
 
var sdid2 = visitor.getSupplementalDataID("consumer4"); // sdid2: 5678
```

**Dynamic Tag Manager (DTM)**

Det finns för närvarande ingen DTM-konfigurationssökväg för `visitor.resetState()`.
