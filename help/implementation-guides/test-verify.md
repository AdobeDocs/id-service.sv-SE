---
description: Dessa instruktioner, verktyg och procedurer hjälper dig att avgöra om ID-tjänsten fungerar som den ska. Dessa tester gäller för ID-tjänsten i allmänhet och för olika kombinationer av ID-tjänster och Experience Cloud-lösningar.
keywords: ID-tjänst
title: Testa och verifiera Experience Cloud Identity Service
exl-id: afdf9778-e73d-46ca-9d2f-a65abaae2fe6
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Testa och verifiera Experience Cloud Identity Service{#test-and-verify-the-experience-cloud-id-service}

Dessa instruktioner, verktyg och procedurer hjälper dig att avgöra om ID-tjänsten fungerar som den ska. Dessa tester gäller för ID-tjänsten i allmänhet och för olika kombinationer av ID-tjänster och Experience Cloud-lösningar.

## Innan du börjar {#section-b1e76ad552ed4eb793b6e521a55127d4}

Viktig information innan du börjar testa och verifiera ID-tjänsten.

**Webbläsarmiljöer**

När du testar i en normal webbläsarsession bör du rensa webbläsarcachen före varje test.

Du kan också testa ID-tjänsten i en anonym eller inkognitiv webbläsarsession. I en anonym session behöver du inte rensa dina webbläsarcookies eller cacheminnen före varje test.

**Verktyg**

The [Adobe-felsökning](https://experienceleague.adobe.com/docs/analytics/implementation/validate/debugger.html) och [Charles HTTP-proxy](https://www.charlesproxy.com/) kan hjälpa dig att avgöra om ID-tjänsten har konfigurerats för att fungera korrekt med Analytics. Informationen i det här avsnittet baseras på resultaten från felsökaren Adobe och Charles. Du bör dock kunna använda det verktyg eller den felsökare som passar dig bäst.

## Testa med felsökaren i Adobe {#section-861365abc24b498e925b3837ea81d469}

Din tjänstintegrering är korrekt konfigurerad när du ser en [!DNL Experience Cloud ID] (MID) i [!DNL Adobe] felsökningssvar. Se [Cookies och Experience Cloud Identity Service](../introduction/cookies.md) för mer information om MID.

Verifiera ID-tjänstens status med [!DNL Adobe] [debugger](https://experienceleague.adobe.com/docs/analytics/implementation/validate/debugger.html):

1. Rensa dina webbläsarcookies eller öppna en anonym webbläsarsession.
1. Läs in testsidan som innehåller ID-tjänstkoden.
1. Öppna [!DNL Adobe] felsökare.
1. Kontrollera resultatet för ett MID.

## Om felsökningsresultat för Adobe {#section-bd2caa6643d54d41a476d747b41e7e25}

MID lagras i ett nyckelvärdepar som använder den här syntaxen: `MID= *`Experience Cloud ID`*`. Felsökaren visar den här informationen som visas nedan.

**Lyckades**

ID-tjänsten har implementerats korrekt om du ser ett svar som ser ut ungefär så här:

```
mid=20265673158980419722735089753036633573
```

Om du är en [!DNL Analytics] kunder kan du se [!DNL Analytics] ID (AID) utöver MID. Det här händer:

* Med några av era tidiga/långa webbplatsbesökare.
* Om du har aktiverat en respitperiod.

**Fel**

Kontakt [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) om felsökaren:

* Returnerar inget MID.
* Returnerar ett felmeddelande som anger att ditt partner-ID inte har etablerats.

## Testa med Charles HTTP-proxy {#section-d9e91f24984146b2b527fe059d7c9355}

Så här verifierar du ID-tjänstens status med Charles:

1. Rensa dina webbläsarcookies eller öppna en anonym webbläsarsession.
1. Starta Charles.
1. Läs in testsidan som innehåller ID-tjänstkoden.
1. Kontrollera om det finns förfrågningar, svarssamtal och data som beskrivs nedan.

## Charles results {#section-c10c3dc0bb9945cbaffcf6fec7082fab}

I det här avsnittet finns information om var du ska söka och vad du ska leta efter när du använder Charles för att övervaka HTTP-anrop.

**Slutförda ID-tjänstbegäranden i Charles**

ID-tjänstkoden fungerar korrekt när `Visitor.getInstance` funktionen gör ett JavaScript-anrop till `dpm.demdex.net`. En lyckad begäran innehåller [Organisations-ID](../reference/requirements.md#section-a02f537129a64ffbb690d5738d360c26). Organisations-ID skickas som ett nyckelvärdepar som använder den här syntaxen: `d_orgid= *`organisations-ID`*`. Leta efter `dpm.demdex.net` och JavaScript-anropen under [!UICONTROL Structure] -fliken. Sök efter ditt organisations-ID under [!UICONTROL Request] -fliken.

![](assets/charles_request.png)

**Slutförda ID-tjänstsvar i Charles**

Ditt konto har etablerats korrekt för ID-tjänsten när svaret från [Datainsamlingsservrar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/system-components/components-data-collection.html) (DCS) returnera ett MID. MID returneras som ett nyckelvärdepar som använder den här syntaxen: `d_mid: *`besökarens Experience Cloud-ID`*`. Leta efter MID i [!UICONTROL Response] enligt nedan.

![](assets/charles_response_success.png)

**Misslyckade ID-tjänstsvar i Charles**

Ditt konto har inte etablerats korrekt om MID saknas i DCS-svaret. Ett misslyckat svar returnerar en felkod och ett felmeddelande i [!UICONTROL Response] enligt nedan. Kontakta kundtjänst om det här felmeddelandet visas i DCS-svaret.

![](assets/charles_response_unsuccessful.png)

Mer information om felkoder finns i [Felkoder, meddelanden och exempel för DCS](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html).
