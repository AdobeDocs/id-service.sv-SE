---
description: ID-tjänsten använder ditt företags-ID, Experience Cloud AMCV-cookie och en demdex-cookie för att skapa och lagra unika, beständiga identifierare för webbplatsens besökare. Med dessa cookies kan ID-tjänsten spåra besökare i olika domäner och möjliggöra datadelning mellan olika Experience Cloud-lösningar.
keywords: spelstation;ID-tjänst
title: Cookies och Experience Cloud Identity Service
exl-id: 727c6381-56b9-44b8-8e59-355d072769be
source-git-commit: 33e467ade389144423abf14539aad8a5a5f69d21
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 2%

---

# Cookies och Experience Cloud Identity Service{#cookies-and-the-experience-cloud-id-service}

ID-tjänsten använder ditt företags-ID, Experience Cloud AMCV-cookie och en demdex-cookie för att skapa och lagra unika, beständiga identifierare för webbplatsens besökare. Med dessa cookies kan ID-tjänsten spåra besökare i olika domäner och möjliggöra datadelning mellan olika Experience Cloud-lösningar.

## Om cookies i ID-tjänsten {#section-f438168beaec409ab8b2cc58bd021e26}

ID-tjänsten förlitar sig på cookies från AMCV, AMCVS och demdex för att fungera korrekt. Dessa cookies är bara filer som lagrar data som används av ID-tjänsten. Dessa ID-tjänstcookies är inte farliga, skadliga eller skiljer sig från andra cookies från första eller tredje part som lagras av en webbplats eller tjänst i en webbläsare, enligt samma regler som styr andra cookies från första och tredje part. Mer information om cookies som används av ID-tjänsten finns i följande avsnitt nedan.

### Vad ID-tjänstens cookies kan göra

* Ange och lagra ett unikt ID för webbplatsbesökarna (MID).
* Behåll detta unika ID så att ID-tjänsten kan samla in och dela data med andra Experience Cloud-lösningar.
* Spåra användare i alla domäner. Detta kräver dock att du äger dessa andra domäner och har ID-tjänstkoden distribuerad till dem.

### Vad ID-tjänstcookies inte kan göra

* Lagra, överföra eller köra datorvirus.
* Få åtkomst till eller lagra personligt identifierbar information (PII), t.ex. din e-postadress.
* Styr datorns maskinvara eller programvara.
* Gör datorer instabila eller orsaka prestandaproblem.
* Spåra användare på webbplatser som inte använder ID-tjänsten.

## AMCV-cookie {#section-c55af54828dc4cce89f6118655d694c8}

Följande attribut för cookien som angetts av ID-tjänsten.

**Namn**

AMCV-cookie-namnet följer syntaxen `AMCV_<variable name>@AdobeOrg`. I namnet `<variable name>` -element är platshållare för en del av ditt Experience Cloud-organisations-ID. Detta ID skickas till DCS av `Visitor.getInstance` i ID-tjänstkoden.

Ett fullständigt cookie-namn ser ut ungefär så här:

```
AMCV_1FD6776A524453CC0A490D44%40AdobeOrg
```

**Innehåll**

AMCV-cookien innehåller Experience Cloud besökar-ID eller MID. MID lagras i ett nyckelvärdepar som följer syntaxen, `MCMID|<Experience Cloud ID>`.

Ett nyckelvärdepar med helt format ser ut ungefär så här:

```
MCMID|20265673158980419722735089753036633573
```

Denna beständiga identifierare möjliggör datadelning mellan lösningar.

**Domän**

AMCV-cookien anges i en webbläsares förstapartsdomän. Det innebär att den anges i domänen för den webbplats som användaren just nu besöker. Därför kan ID-tjänstkoden och andra Experience Cloud-kodbibliotek läsa MID som lagras i AMCV-cookien.

Eftersom AMCV-cookien är inställd i den första domänen kan den inte användas för att spåra och identifiera användare i olika domäner. Istället förlitar sig ID-tjänsten på organisations-ID:t och demdex-ID:t för att returnera rätt MID när en besökare navigerar till en annan domän.

## AMCVS cookie {#section-92a9454f1ac645948f9059b9fad928bf}

**Namn**

AMCVS-cookie-namnet följer syntaxen `AMCVS_####@AdobeOrg`. I namnet är ####-elementen platshållare för en del av ditt Experience Cloud-organisations-ID. Detta ID skickas till DCS av `theVisitor.getInstance` i ID-tjänstkoden.

Ett fullständigt cookie-namn ser ut ungefär så här:

```
AMCVS_1FD6776A524453CC0A490D44%40AdobeOrg
```

**Innehåll**

AMCVS-cookien fungerar som en flagga som anger att sessionen har initierats. Dess värde är alltid `1` och avbryts när sessionen har avslutats.

**Domän**

AMCVS-cookien anges i en webbläsares förstapartsdomän. Det innebär att den anges i domänen för den webbplats som användaren just nu besöker.

![](assets/AMCVS-cookie.png)

## Demdex cookie {#section-7ff7d96d6e4141b08a84a75a63d7814c}

I följande tabell listas och definieras några viktiga attribut i demodex-cookien.

<table id="table_18E3CAF3550E4BB6A199736AACE39202"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Attribut </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Namn</b> </p> </td> 
   <td colname="col2"> <p>Cookie-namnet är "demdex". </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Innehåll</b> </p> </td> 
   <td colname="col2"> <p>Demdex-cookien innehåller demdex-ID:t, som genereras av DCS. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Domän</b> </p> </td> 
   <td colname="col2"> <p>Demdex-cookie anges i domänen demdex.net från tredje part i webbläsaren. Den här domänen är skild från den webbplats som användaren just nu besöker. </p> <p>Till skillnad från den första parten, AMCV cookie, finns demonstrationscookien och ID kvar i olika domäner. ID:t och ditt organisations-ID är de gemensamma värden som gör att ID-tjänsten kan returnera och identifiera en besökare med rätt besökar-ID. </p> </td> 
  </tr> 
 </tbody> 
</table>

Information om information om Demdex finns på [Lagringsinformation för Audience Manager-enheter](https://aam-iab-tcf-vendor.s3.amazonaws.com/aam_device_storage_disclosures.json).

Mer information finns i dokumentationen om [förstå anrop till Demdex-domänen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=en).

## Genererar Experience Cloud-ID {#section-15f69c0bac394b4b9966a23fbc586d17}

Experience Cloud ID (MID) härleds matematiskt från ditt företags-ID och demdex-ID. Så länge dessa ID:n är konstanta är det helt enkelt ett viktigt problem att generera rätt MID för en viss användare. Med samma organisations-ID och demdex-ID får du samma MID-värde varje gång. Detta gör att ID-tjänsten kan spåra besökare över domäner som du kontrollerar och har konfigurerat med ID-tjänstkoden.

ID-tjänsten börjar skapa ett MID när sidan läses in. Under den här processen tillhandahålls kod från `visitorAPI.js` kodbiblioteket skickar ditt organisations-ID i ett händelseanrop till ID-tjänsten. ID-tjänsten skapar och returnerar MID och ett demdex-ID i AMCV- respektive demdex-cookies.

## Cookies-flaggor

I följande tabell beskrivs flaggorna för Experience Cloud Cookies:

| Cookie (anges av) | httpOnly | Säker | SameSite |
|--- |--- |--- |--- |
| demdex (http-svar) | Nej | Ja | &quot;Ingen&quot; |
| AMCV (Javascript) | Nej | Konfigurerbar | Ta bort (standard är Lax) |
| AMCVS (Javascript) | Nej | Konfigurerbar | Ta bort (standard är Lax) |

*Obs! Information om hur du konfigurerar AMCV- och AMCVS-cookie med säkra attribut finns i avsnittet för [secureCookie](../library/function-vars/securecookie.md).*

## Nästa steg {#section-8db1727a63bc4ff68b495f270315d453}

Se [Hur Experience Cloud Identity Service begär och anger ID:n...](../introduction/id-request.md#concept-2caacebb1d244402816760e9b8bcef6a).
