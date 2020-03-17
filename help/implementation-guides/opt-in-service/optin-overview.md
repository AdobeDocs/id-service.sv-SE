---
description: Med anmälningstjänsten kan du konfigurera protokoll för besökaren för att avgöra om du kan ange en cookie på användarens enhet eller webbläsare när du besöker webbplatsen.
seo-description: Med anmälningstjänsten kan du konfigurera protokoll för besökaren för att avgöra om du kan ange en cookie på användarens enhet eller webbläsare när du besöker webbplatsen.
seo-title: Anmälningstjänst
title: Anmälningstjänst
uuid: aebd72ad-4118-471b-9755-d08a72caa0fd
translation-type: tm+mt
source-git-commit: 4fbfefddcf36855f32f2a4047e19ef0b22fc508c

---


# Anmälningstjänst{#opt-in-service}

Med anmälningstjänsten kan du konfigurera protokoll för besökaren för att avgöra om du kan ange en cookie på användarens enhet eller webbläsare när du besöker webbplatsen.

Opt-in-tjänsten är ett tillägg till Experience Cloud ID (ECID), som är utformat för att du ska kunna kontrollera om och vilka Experience Cloud-lösningar som kan skapa cookies på webbsidor för besökare innan användaren ger sitt samtycke. Med hjälp av Opt-in-tjänsten kan du också ange protokoll som ska integreras med CMP (Consent Management Platform) och befintliga system som en del av din större design.

Med hjälp av anmälningstjänsten kan du ange om en besökare kan välja Adobe-lösningar samtidigt eller presentera lösningar i sekvens för tillstånd. När godkännandeprocessen är klar och inspelad av kunden kan ni hämta CMP-godkännandena från alla Adobe-lösningar.

Opt-in-tjänsten implementeras och konfigureras enkelt med [Adobe Experience Platform Launch](https://docs.adobelaunch.com/) med [Opt-in-tillägget](../../implementation-guides/opt-in-service/launch.md). Den kan också implementeras och konfigureras med [DTM](../../implementation-guides/opt-in-service/optin-dtm.md).

Se [Konfigurera anmälningstjänsten](../../implementation-guides/opt-in-service/getting-started.md) för att komma igång.

>[!NOTE]
>
>Med anmälningstjänsten kan du konfigurera ett system för att endast godkänna eller neka nedladdning av Adobe-cookies. Det har inte stöd för att samla in användarens medgivandeinställningar, och det är inte heller en databas för inställningar.

>[!IMPORTANT]
>
>Innehållet i detta dokument är inte juridisk rådgivning och är inte avsett att ersätta juridisk rådgivning. Kontakta företagets juridiska avdelning för råd om samtycke och rutiner när du väljer implementering.

## Anmäl dig till Experience Cloud-lösningar {#section-053e6224505542cf961896f0ca869e52}

Opt-in-tjänsten är ett verktyg för att skapa ett medgivande i arbetsflöde efter dina egna behov, vilket gör att du kan utforma ett arbetsflöde för att reagera (brandmärken) innan och efter det att användaren eller den som har gett sitt medgivande har gett det.

Med tjänsten Opt-In kan ni ange rutiner för samtyckeshantering för Adobes lösningar för att

* Ange om kraven för insamling av samtycke gäller i allmänhet för en användare.
* Ange vilka lösningar som tillåts generera cookies.
* Använd standardinställningar för alla lösningar vars kategori inte uttryckligen godkänns eller avvisas av användaren.
* Utlös anpassat svar baserat på ändringar i användarens medgivandeinställningar, så att du kan behålla eller uppdatera användarens inställningar.

Med hjälp av anmälningstjänsterna kan du konfigurera din webbplats så att vissa cookies kan läsas in med förhandsgodkännande innan användaren väljer det. Du kan ställa in anmälningstjänster för nya kunder för att tillåta att cookies läses in efter att användaren har godkänt eller efter att ett val har gjorts tillgängligt. Du kan också lagra och hämta medgivande från din befintliga plattform för hantering av samtycke eller helt enkelt lagra behörigheter i en cookie.

![](assets/Opt-in-approval.png)

Adobes lösningar kan sedan kontrollera om taggen är godkänd, prenumerera på ändringar och sedan hämta alla kunder som har anmält sig. Med en anmälningstjänst kan du få behörigheter direkt via JavaScript-bibliotek i lösningen eller via ECID om det implementeras.
