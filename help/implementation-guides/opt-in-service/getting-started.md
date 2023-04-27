---
description: Implementera anmälningstjänsten som den enda referenspunkt som används av Experience Cloud-lösningar (kallas kategorier i anmälan) för att avgöra om cookies ska skapas på en besökares enhet eller inte.
title: Konfigurera anmälningstjänst
exl-id: 6e8a6531-9924-4523-a842-cb4614a7a7a0
source-git-commit: 070390ec0534c9066d717fe52ff572f34c110137
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 1%

---

# Konfigurera anmälningstjänst{#setting-up-opt-in-service}

Implementera anmälningstjänsten som den enda referenspunkt som används av Experience Cloud-lösningar (kallas kategorier i anmälan) för att avgöra om cookies ska skapas på en besökares enhet eller inte.

Opt-in-tjänsten är ett JavaScript-bibliotek som paketerats med Experience Cloud ID (ECID) och finns i Visitor JS i den globala `adobe` objektet som `adobe.optIn` -objekt. Med den installerade Opt-in-tjänsten kan du ange om en besökare kan välja att gå med i Adobe-lösningar samtidigt eller att presentera lösningar i följd för respektive behörighet. Med funktionen för hantering av tjänstgodkännande kan du implementera med olika konfigurationer för dina specifika sekretesskrav.

Med anmälningstjänsten kan du ange om en besökare kan välja att använda Adobe-lösningar samtidigt eller att presentera lösningar i ordning för respektive behörighet. När godkännandeprocessen är slutförd och inspelad av kunden kan CMP-besökarnas godkännanden hämtas av alla Adobe-lösningar för att svara på sambandsanrop.

## Förutsättningar {#section-c39246f45e514c8ea9fdbe6f7ffa3ad0}

1. ECID version 4.0.

   [Hämta](https://github.com/Adobe-Marketing-Cloud/id-service/releases) den senaste ECID-versionen.

1. Stödbibliotek:

   * ECID 4.0 eller senare
   * AppMeasurement 2.11 eller senare
   * DIL 9.0
   * AT.js version 1.7.0
   * AT.js Starta tillägg 9.0
   * För Analytics, App Measurement 2.11 with extension 1.6
   * För Mål, utökning 0.9.1

1. Bli en god vana i det system för samtyckeshantering som ni kommer att använda med anmälan och förstå eventuella ytterligare krav.

   <!--
   For IAB, see here for additional pre-reqs.
   -->

1. Ditt företags sekretesskrav är specifika för hur du väljer att följa GDPR. Observera vilka bibliotek ditt företags sekretessteam kan använda i ett förhandstillstånd.

Om du använder [Taggar i Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv), dra nytta av [Anmäl tillägg](../../implementation-guides/opt-in-service/launch.md) för att konfigurera anmälningstjänsten.

## Anmälningskategorier {#section-9ab0492ab4414f0ca16dc08d3a905f47}

Inställningarna för besökarens deltagande är relativa till en Adobe Experience Cloud-lösning, där varje lösning representeras som en kategori. Kategorierna tillhandahålls av `adobe.OptInCategories` objekt där t.ex. ECID-komponenten kallas `adobe.OptInCategories`. `ECID`. Här följer en definition av `adobe.OptInCategories`:

Inställningarna för deltagande upprätthålls per kategori, där varje Experience Cloud-lösning representeras av en kategori:

```
adobe.OptInCategories = { 
    AAM: "aam", 
    TARGET: "target",  
    ANALYTICS: "aa", 
    ECID: "ecid", 
     
};
```

Med anmälningstjänsten kan du ange besökarnas behörigheter för varje Adobe-lösning som används på webbplatsen. Det innehåller ett bibliotek där besökarens inställningar sparas per godkänd kategori och ett sekventiellt flöde där godkännandeprocessen får inställningarna&quot;bekräfta&quot; eller&quot;avvisa&quot; för varje kategori ett i taget. Du kan ange att lösningar/kategorier ska ingå som en helhet eller som enskilda lösningar.
Alla Adobe-lösningars klientbibliotek är beroende av anmälningstjänsten och kommer inte att generera cookies om inte lösningen har beviljats tillstånd. Opt-in stöder olika metoder för att tillhandahålla och uppdatera medgivandeinställningarna för den aktuella besökaren. I det här avsnittet finns exempel på hur du anger inställningar för Opt-in-tjänster. Se [API-referens för deltagande](../../implementation-guides/opt-in-service/api.md#reference-4f30152333dd4990ab10c1b8b82fc867) för en fullständig lista över funktioner och parametrar.

Tjänstkonfigurationer för att välja är tillgängliga i JS för besökare `getInstance()` som instansierar den globala `adobe` -objekt. I följande lista visas besökarens JS [konfigurationsinställningar](../../implementation-guides/opt-in-service/api.md#section-d66018342baf401389f248bb381becbf) för anmälningstjänst.

**Exempel på konfiguration för deltagande i initiering av den globala `Visitor` object**

```
// FORMAT: Object<adobe.OptInCategories enum: boolean> 
var preOptInApprovalsConfig = {}; 
preOptInApprovals[adobe.OptInCategories.ANALYTICS] = true; 
  
// FORMAT: Object<adobe.OptInCategories enum: boolean> 
// If you are storing the OptIn permissions on your side (in a cookie you manage or in a CMP), 
// you have to provide those permissions through the previousPermissions config. 
// previousPermissions will overwrite preOptInApprovals. 
var previousPermissionsConfig = {}; 
previousPermissionsConfig[adobe.OptInCategories.AAM] = true; 
previousPermissionsConfig[adobe.OptInCategories.ANALYTICS] = false; 
  
Visitor.getInstance("YOUR_ORG_ID", { 
    "doesOptInApply": true, // NOTE: This can be a function that evaluates to true or false. 
    "preOptInApprovals": preOptInApprovalsConfig, 
    "previousPermissions": previousPermissionsConfig, 
    "isOptInStorageEnabled": true 
});
```

**Hantera ändringar av samtycke**

När som helst under besökarens upplevelse på webbplatsen kan de göra inställningar för första gången eller ändra sina inställningar med hjälp av din CMP. När JS för besökare har initierats med initiala inställningar kan besökarens behörigheter ändras. Se [Ändringar i samtycke](../../implementation-guides/opt-in-service/api.md#section-c3d85403ff0d4394bd775c39f3d001fc) om du vill ha en lista över hur du hanterar funktioner för samtycke.

<!--
<p> *** <b>sample code block </b>*** </p>
-->

## Arbetsflöden för deltagande {#section-70cd243dec834c8ea096488640ae20a5}

Opt-in-tjänsten stöder ett arbetsflöde där behörigheter kan samlas in över mer än en begärandecykel och inställningarna anges en åt gången. Använda följande funktioner och *true* for `shouldWaitForComplete`kan er lösning samla in samtycke för en eller en del av de totala kategorierna och sedan samla in samtycke för nästa eller delmängd av kategorier. Från och med första samtalet visas `adobe.optIn.status` egenskapen kommer att vara *väntar* tills `adobe.optIn.complete()` anropas i slutet av flödet. Statusen ställs in på *complete*.

```
adobe.optIn.approve(['AAM', 'ECID'], true); 
adobe.optIn.deny(['ANALYTICS'], true); 
adobe.optIn.complete();
```

Se [Inställningar för arbetsflödeskonfiguration](../../implementation-guides/opt-in-service/api.md#section-2c5adfa5459c4e72b96d2693123a53c2).

## Inspect din besökares behörigheter {#section-f136a9024e054d84881e6667fb7c94eb}

När besökarna ändrar sina behörigheter måste ni få insikter i vilka behörigheter som krävs för att synkronisera ert godkännandearkiv med ändringar som gjorts i anmälningstjänsten. Inspect besökarens önskemål med [behörighetsfunktioner](../../implementation-guides/opt-in-service/api.md#section-7fe57279b5b44b4f8fe47e336df60155), till exempel:

**hämtaBehörighetsexempel**

```
optIn.fetchPermissions(function (permissions) { 
    // Here you can check if your category has been approved or not. 
    // We recommend using optIn.isApproved() to check for permissions because it abstracts out the details of knowing exactly how the permissions list looks like. 
    if (adobe.optIn.isApproved(MY_CATEGORY) { 
        sendBeacon(); // Or something 
    } 
});

OR: You can pass in shouldAutoSubscribe as true, your callback will be used to subscribe to all OptIn events going forward:

function callback() { 
    if (adobe.optIn.isApproved(MY_CATEGORY) { 
        sendBeacon(); // Or something 
    } 
}

optIn.fetchPermissions(callback, true);
```

Se [API-dokumentation](../../implementation-guides/opt-in-service/api.md#reference-4f30152333dd4990ab10c1b8b82fc867) om du vill ha mer information om dessa funktioner, egenskaper eller konfigurationer som nämns i det här dokumentet.

## Lagra besökarinställningar {#section-ef2884ae67e34879bf7c7c3372706c9f}

Med anmälningstjänsten kan du lagra medgivandeinställningar som är anpassade till en dev-miljö eller en miljö där det inte är möjligt att använda en CRM. Ange konfigurationsegenskapen `isOptInStorageEnabled` as *true* utlöser en Opt-in-tjänst för att skapa en cookie i besökarens system i din domän.

The `adobe.optIn` objektet är tillståndslöst och saknar lagringsmekanism. I stället ska du hantera inställningarna för medgivande från Adobe i din befintliga CMP-plattform (Consent Management Platform) om det tillåter lagring av anpassade data. Eller så kan du lagra besökarinställningar i en cookie i besökarens webbläsare. Det finns två alternativ för att ange användarens inställningar för tjänsten för anmälan:

* Om din lösning för samtyckesbeständighet, oavsett om det är en CMP eller en cookie i besökarens webbläsare, tillåter snabb hämtning av besökarens inställningar, kan du tillhandahålla inställningarna till Opt-in-tjänsten när besökaren initieras.
* Om hämtningen kan vara en lång process eller på annat sätt fungerar bäst som en asynkron process, kan du använda tjänstens `approve()` för att ange dessa inställningar när de har lästs in.
