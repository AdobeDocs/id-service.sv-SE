---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID Service
seo-description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
seo-title: Versionsinformation 2019
title: Versionsinformation 2019
uuid: a5a59410-7f85-48f9-a30a-fef1c2e2b558
translation-type: tm+mt
source-git-commit: 8ece066545f4ca4a7bd1eca67c8f02dcd2a88369
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---


# Experience Cloud release notes - 2019 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.

## Version 4.4.1

Lägg till kryssrutan för godkännande före anmälan för medieanalys i ECID Launch Extension.

**Korrigeringar**

* Problem med att ECID-starttillägget preOptInApprovals tolkar indatasträngen.
* Prestandafall när trackingServer används.

## Version 4.4 {#version-4point4}

**Ny funktion**

[SHA256 Hash-stöd för setCustomerID](/help/reference/hashing-support.md). Experience Cloud ID-tjänsten (ECID) stöder SHA-256-algoritmen som gör att du kan skicka in kund-ID:n eller e-postadresser och skicka ut hash-kodade ID:n.

**Korrigeringar, förbättringar, förbättringar**

* Vi har gjort en konfigurationsuppdatering till `cookieDomain`. ECID-biblioteket filtrerar nu bort den tomma strängen `cookieDomain` i `initConfig` och använder cookie-domänen på den översta nivån, som returneras av metoden getDomain.
* Vi har åtgärdat ett fel relaterat till `getVisitorValues` i `localVisitor`.
* Vi har åtgärdat ett fel där det fanns en inkonsekvens för MCOPTOUT-värdet i webbläsaren Safari, som returnerades av `getVisitorValue` metoden.
* Vi uppdaterade avanmälningsbiblioteket genom `optIn.off` att lägga till för att avbryta prenumerationen på händelser.
* Vi har åtgärdat ett fel som är relaterat till funktionen setTimeout, där `setTimeout` Content Security Policy (CSP) har överträtts på vissa kundsajter.

## Version 4.3 {#version-4point3}

**Stöd för ITP 2.1**. Om en spårningsserver anges i en CNAME från en första part placeras en ny cookie (s_ecid) med ECID-värdet. ECID-biblioteket refererar till värdet för att behålla ID:t längre än 7 dagar. Se [ECID-biblioteksmetoder i en Safari ITP-värld](/help/reference/ecid-library-methods.md).

**Felkorrigering för secureCookie-konfiguration.**

## Version 4.1

Uppdatera `publishDestinations` per ny API-ändring. Med den här uppdateringen kan sidans referensinformation visas under ID - synkronisera om så önskas.

## Version 4.2

Stöd för plugin-programmet Audience Manager för IAB TCF, tillgängligt via ECID-objektet Opt-in.

**Korrigeringar**

* IAB + OptIn får inte MID för att besöka kunder.
* Korrigerat fel vid konfiguration av opt-in doesOptInApply i DTM.
* Avanmäl dig från ECID inaktiverar ID-synkronisering.

## Version 4.0 {#section-51a4be943bbe41558f196ef2654513e2}

**Anmälningstjänst**. Opt-in är ett tillägg till Experience Cloud ID (ECID) som gör att du kan kontrollera om (och sedan vilka) Experience Cloud-bibliotek kan skapa cookies på webbsidor för besökare. Med [Experience Platform Launch](https://docs.adobelaunch.com/)kan ni förenkla insamlandet av besökares deltagande i Experience Cloud-lösningar genom att aktivera Analytics, Target, Audience Manager och andra eller alla utvalda Experience Cloud-lösningar för att utnyttja ert system för samtyckeshantering.

## Version 3.4 {#section-046ce29b43af47cc849d4091098f5927}

| Objekt | Beskrivning |
|---|---|
| `disableIdSyncs` -flaggan fungerar inte när en sträng skickas. | Åtgärdat. Värden som angetts för `disableidSyncs` parametern för `getInstance` funktionen respekteras nu. |
| iFrames från tredje part hämtar inte ECID | ECID för Safari Mobil och ECID i olika iFrames som inte fungerade har åtgärdats. |
