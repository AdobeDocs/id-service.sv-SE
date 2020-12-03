---
description: Dessa instruktioner, verktyg och procedurer hjälper dig att avgöra om ID-tjänsten fungerar som den ska. Dessa tester gäller för ID-tjänsten i allmänhet och för olika kombinationer av ID-tjänster och Experience Cloud-lösningar.
keywords: ID Service
seo-description: Dessa instruktioner, verktyg och procedurer hjälper dig att avgöra om ID-tjänsten fungerar som den ska. Dessa tester gäller för ID-tjänsten i allmänhet och för olika kombinationer av ID-tjänster och Experience Cloud-lösningar.
seo-title: Testa och verifiera Experience Cloud Identity Service
title: Testa och verifiera Experience Cloud Identity Service
uuid: 442de9c3-c265-4412-89bd-aeaa286ddad6
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3
workflow-type: tm+mt
source-wordcount: '717'
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

Felsökaren [för](https://docs.adobe.com/content/help/en/analytics/implementation/validate/debugger.html) Adobe och [Charles HTTP-proxyn](https://www.charlesproxy.com/) kan hjälpa dig att avgöra om ID-tjänsten har konfigurerats för att fungera korrekt med Analytics. Informationen i det här avsnittet baseras på resultaten från felsökaren Adobe och Charles. Du bör dock kunna använda det verktyg eller den felsökare som passar dig bäst.

## Testa med felsökaren i Adobe {#section-861365abc24b498e925b3837ea81d469}

Din tjänstintegrering är korrekt konfigurerad när du ser ett [!DNL Experience Cloud ID] (MID) i [!DNL Adobe] felsökningssvaret. Mer information om MID finns i [Cookies och Experience Cloud Identity Service](../introduction/cookies.md) .

Så här verifierar du statusen för ID-tjänsten med [!DNL Adobe] felsökaren [](https://docs.adobe.com/content/help/en/analytics/implementation/validate/debugger.html):

1. Rensa dina webbläsarcookies eller öppna en anonym webbläsarsession.
1. Läs in testsidan som innehåller ID-tjänstkoden.
1. Öppna [!DNL Adobe] felsökningsprogrammet.
1. Kontrollera resultatet för ett MID.

## Om felsökningsresultat för Adobe {#section-bd2caa6643d54d41a476d747b41e7e25}

MID lagras i ett nyckelvärdepar som använder den här syntaxen: `MID= *`Experience Cloud ID`*`. Felsökaren visar den här informationen som visas nedan.

**Lyckades**

ID-tjänsten har implementerats korrekt om du ser ett svar som ser ut ungefär så här:

```
mid=20265673158980419722735089753036633573
```

Om du är en [!DNL Analytics] kund kan du se ett [!DNL Analytics] ID (AID) förutom MID. Det här händer:

* Med några av era tidiga/långa webbplatsbesökare.
* Om du har aktiverat en respitperiod.

**Fel**

Kontakta [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) om felsökaren:

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

Koden för din ID-tjänst fungerar korrekt när funktionen gör ett JavaScript-anrop till `Visitor.getInstance` `dpm.demdex.net`. En lyckad begäran innehåller ditt [organisations-ID](../reference/requirements.md#section-a02f537129a64ffbb690d5738d360c26). Organisations-ID skickas som ett nyckelvärdepar som använder den här syntaxen: `d_orgid= *`organisations-ID`*`. Leta efter `dpm.demdex.net` och JavaScript-anropen under [!UICONTROL Structure] fliken. Leta efter ditt organisations-ID på [!UICONTROL Request] fliken.

![](assets/charles_request.png)

**Slutförda ID-tjänstsvar i Charles**

Ditt konto har etablerats korrekt för ID-tjänsten när svaret från [datainsamlingsservrarna](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/system-components/components-data-collection.html) (DCS) returnerar ett MID. MID returneras som ett nyckelvärdepar som använder den här syntaxen: `d_mid: *`besökarens Experience Cloud-ID`*`. Leta efter MID på [!UICONTROL Response] fliken enligt nedan.

![](assets/charles_response_success.png)

**Misslyckade ID-tjänstsvar i Charles**

Ditt konto har inte etablerats korrekt om MID saknas i DCS-svaret. Ett misslyckat svar returnerar en felkod och ett felmeddelande på [!UICONTROL Response] fliken enligt nedan. Kontakta kundtjänst om det här felmeddelandet visas i DCS-svaret.

![](assets/charles_response_unsuccessful.png)

Mer information om felkoder finns i [DCS-felkoder, meddelanden och exempel](https://docs.adobe.com/content/help/en/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html).
