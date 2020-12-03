---
description: API för avanmälningsbiblioteket och konfigurationsinställningsreferensen.
seo-description: API för avanmälningsbiblioteket och konfigurationsinställningsreferensen.
seo-title: Anmälningsreferens
title: Anmälningsreferens
uuid: d5023a34-2f3e-464d-b21f-579b2f416ce6
translation-type: tm+mt
source-git-commit: 4fbfefddcf36855f32f2a4047e19ef0b22fc508c
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---


# Anmälningsreferens{#opt-in-reference}

API för avanmälningsbiblioteket och konfigurationsinställningsreferensen.

Medgivandeinställningar anges för avanmälningsfunktionerna som kategorier:

```
adobe.OptInCategories = { 
    "AAM": "aam", 
    "ANALYTICS": "aa", 
    "ECID": "ecid", 
    "TARGET": "target" 
}
```

## Parametrar för Opt-in-konfiguration {#section-d66018342baf401389f248bb381becbf}

I det här avsnittet beskrivs hur du använder API för att konfigurera anmälan. En stor del av konfigurationen och implementeringen kan göras med tillägget Experience Platform Launch.

Opt-in-konfigurationer finns i JavaScript- `getInstance()` funktionen för Visitor som instansierar det globala `adobe` objektet. Nedan visas JS-konfigurationer för besökare som är relaterade till Opt-in-tjänsten.

**`doesOptInApply (boolean or function that evaluates to a boolean)`**:

Om värdet är false behöver besökarna inte välja. Gör att du kan skapa cookies i Experience Cloud oavsett vilken kategori du har valt in eller ut. Den här konfigurationen aktiverar eller inaktiverar deltagande på ett övergripande sätt.

**`preOptInApprovals (Object <adobe.OptInCategories enum: boolean>)`**

Definiera vilka kategorier som godkänns eller nekas när ingen inställning har angetts av besökaren, vilket kallas standardinställningar för organisationen.

**`previousPermissions (Object<adobe.OptInCategories enum: boolean>)`**

Besökarens inställningar anges uttryckligen. Behörigheterna i den här konfigurationen skriver över organisationsstandardvärden ( `previousPermissions` skriver över `preOptInApprovals`).

**`isOptInStorageEnabled (boolean)`**

Aktivera deltagande för att lagra behörigheter i en cookie från en annan leverantör (inom den aktuella kundens domän)

(Valfritt) **`optInCookiesDomain (string)`**

Första parts domän eller underdomän som ska användas för cookie-filen för anmälan (om `isOptInStorageEnabled` värdet är true)

(Valfritt) **`optInStorageExpiry (integer)`**

Antal sekunder som standardförfallotiden på 13 månader ska åsidosättas

## Ändringar av parametrar för samtycke {#section-c3d85403ff0d4394bd775c39f3d001fc}

När som helst när besökaren befinner sig på webbplatsen kan han/hon göra inställningar för den första gången eller ändra sina inställningar med din CMP. När JS-besökaren har initierats med initiala inställningar kan besökarens behörigheter ändras med följande funktioner:

**`adobe.optIn.approve(categories, shouldWaitForComplete)`**

Funktion som godkänner eller placerar besökaren i alla kategorier i en lista. Mer information om parametern shouldWaitForComplete finns i Arbetsflöde för [anmälan](../../implementation-guides/opt-in-service/getting-started.md#section-70cd243dec834c8ea096488640ae20a5).

**`adobe.optIn.deny(categories, shouldWaitForComplete)`**

Funktion som nekar eller flyttar besökaren från alla angivna kategorier.

**`adobe.optIn.approveAll()`**:

Om din begäran om tillstånd för webbplatsen att skapa är formulerad så att en besökarfilt beviljar eller nekar tillstånd för webbplatsen att skapa cookies, använder `approveAll()` eller `denyAll()`, i förhållande till deras svar.

**`adobe.optIn.denyAll()`**:

Om din begäran om tillstånd för webbplatsen att skapa är formulerad så att en besökarfilt beviljar eller nekar tillstånd för webbplatsen att skapa cookies, använder `approveAll()` eller `denyAll()`, i förhållande till svaret.

## Parametrar för Opt-in-arbetsflöden {#section-2c5adfa5459c4e72b96d2693123a53c2}

Opt-in har stöd för ett arbetsflöde där behörigheter kan samlas in över mer än en begärandecykel, till exempel var inställningarna ges en åt gången. Med hjälp av följande funktioner och med *true* för `shouldWaitForComplete` inställningen, kan din lösning samla in samtycke för en lösning eller en delmängd av de totala kategorierna och sedan samla in samtycke för nästa eller en delmängd av kategorierna. Från och med det första anropet väntar egenskapen tills den `adobe.optIn.status` `adobe.optIn.complete()` anropas i slutet av flödet. När du har anropat statusen är den *fullständig*.

**`adobe.optIn.approve(categories, shouldWaitForComplete)`**

Funktion som godkänner eller placerar besökaren i alla kategorier i en lista.

`adobe.optIn.deny(categories, shouldWaitForComplete)`

Funktion som nekar eller flyttar besökaren från alla angivna kategorier.

`adobe.optIn.complete()`

Funktion som utlöser sammanställningen av proceduren anropar till accept() och deny() i en begäran för att ange en besökares inställningar. När du prenumererar på ändringar av anmälan (se `adobe.optIn.fetchPermissions(callback, shouldAutoSubscribe`) nedan aktiveras återanropet endast när den här funktionen anropas.

## Parametrar för behörigheter för besökaranmälan {#section-7fe57279b5b44b4f8fe47e336df60155}

Samla in alternativbehörigheter för en besökare när som helst med någon av behörighetsfunktionerna:

`adobe.optIn.permissions`

Ett objekt som listar alla Experience Cloud-lösningar, som kategorier, som har beviljats eller nekats av besökaren.

`adobe.optIn.isApproved(categories)`

Om alla kategorier har godkänts returneras true.

`adobe.optIn.fetchPermissions(callback, shouldAutoSubscribe)`

Hämta listan över behörigheter asynkront. Återanropet anropas med listan över behörigheter när processen för att bevilja/neka behörigheter är slutförd. Om du anger värdet *true* för `shouldAutoSubscribe` registreras callback-funktionen för ändringar av Opt-in-alternativen som fortsätter framåt. Följande är egenskaper för `adobe.OptIn`:

**`permissions`**

Ett objekt som listar alla Experience Cloud-lösningar, som kategorier, som har beviljats eller nekats av besökarexemplet: `{ aa: true, ecid: false, aam: true... }`

**`status`**

* väntar
* ändrad
* complete

**`doesOptInApply`**

Sant eller falskt, som representerar konfigurationen som du angav i initieringen

**`isPending`**

Sant eller falskt, beroende på statusvärdet. Anmälningsrapporter är true för den här egenskapen för en besökare som ännu inte uttryckligen har accepterat eller nekat behörighet

**`isComplete`**

Sant eller falskt beroende på statusvärdet. Opt-in kan rapportera false för den här egenskapen när ett arbetsflödesliknande medgivande har påbörjats men inte slutförts.

## Metoder för Opt-in-objekt {#section-e0417801a82548d199d833010033e433}

**`approve(categories, shouldWaitForComplete)`**

**`categories`**: En eller flera kategorier att godkänna. Till exempel: `adobe.optIn.approve([adobe.OptInCategories.AAM, adobe.OptInCategories.ECID])`
**`shouldWaitForComplete`**: (valfritt) boolesk parameter, false som standard. Om du skickar true slutförs inte godkännandeprocessen förrän du ringer `adobe.optIn.complete()`. Den här processen liknar ett arbetsflöde.

```
<codeblock>
  adobe.optIn.approve(adobe.OptInCategories.ANALYTICS, 
         true); adobe.optIn.approve(adobe.OptInCategories.ECID, true); 
         adobe.optIn.complete() 
</codeblock>
```

**`deny(categories, shouldWaitForComplete)`**

* Skicka en eller flera kategorier för att kontrollera om de har godkänts.
* Om inga kategorier skickas kontrolleras ALLA tillgängliga kategorier.

**`isApproved(categories)`**

Kontrollera om en eller flera kategorier har godkänts av kunden.

**`isPreApproved(categories)`**

Kontrollera om en eller flera kategorier har godkänts i förväg av kunden. (Om de skickades i `preOptInApprovals` konfigurationen).

**`fetchPermissions(callback, shouldAutoSubscribe)`**

Async API för att hämta listan över behörigheter. Återanropet anropas med listan över behörigheter när processen för att bevilja/neka behörigheter är slutförd. **`shouldAutoSubscribe`:** Ett hjälpverktyg som automatiskt prenumererar på återanropet för alla framtida händelser. Betydelse som återanropet anropas varje gång en godkännanderutlösare eller en avvisare i Opt In anropas. På så sätt uppdateras du alltid utan att du själv behöver prenumerera på händelserna.

**Exempel**

`fetchPermissions`

```
optIn.fetchPermissions(function (permissions) { 
    // Here you can check if your category has been approved or not. 
    // We recommend using `optIn.isApproved()` to check for permissions because it abstracts  
       out the details of knowing exactly how the `permissions` list looks like. 
 
    if (adobe.optIn.isApproved(MY_CATEGORY) { 
        sendBeacon(); // Or something 
    } 
});

// OR: You can pass in `shouldAutoSubscribe` as true, your callback will be used to subscribe  
to all OptIn events going forward:

function callback() { 
    if (adobe.optIn.isApproved(MY_CATEGORY) { 
        sendBeacon(); // Or something 
    } 
} 
 
optIn.fetchPermissions(callback, true);
```

**`complete()`:**

>[!NOTE]
>
>Använd bara om du har skickat `shouldWaitForComplete` parametern som ska godkännas eller nekas. Detta API slutför godkännandeprocessen. Exempel: `adobe.optIn.complete()`.

**`approveAll()`:**

Godkänner alla befintliga kategorier.

**`denyAll()`**

Neka alla befintliga kategorier.

## Händelser för Opt-in-objekt {#section-06f25b33cab54bafb053183e937fb710}

**`complete`:**

Slutför händelse utlöses när godkännandeprocessen har slutförts. Om du anropar Godkänn/Neka utan att skicka `shouldWaitForComplete`, eller `approveAll`/ `denyAll`, utlöser den här händelsen. Eller om du skickar `shouldWaitForComplete`den här händelsen utlöses när `complete` anropas.

**Exempel**

```
<codeph>
  adobe.optIn.on("complete", callback); 
</codeph>
```
