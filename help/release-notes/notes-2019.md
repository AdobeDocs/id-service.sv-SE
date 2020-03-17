---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID Service
seo-description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
seo-title: Versionsinformation 2019
title: Versionsinformation 2019
uuid: a5a59410-7f85-48f9-a30a-fef1c2e2b558
translation-type: tm+mt
source-git-commit: 25a9af7a28462bc0bd26cf4a5a58203e76a83366

---


# Versionsinformation om Experience Cloud - 2019 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.

## Version 4.4.1

Lägg till kryssrutan för godkännande före anmälan för medieanalys i ECID Launch Extension (CORE-33185)

**Korrigeringar**

* Problem med ECID-starttillägg för parsning av indatasträngen preOptInApprovals (CORE-34041)
* Prestandafall när trackingServer används (CORE-32387)

## Version 4.4 {#version-4point4}

**Ny funktion**

[SHA256 Hash-stöd för setCustomerID](/help/reference/hashing-support.md). Experience Cloud ID Service (ECID) stöder SHA-256-algoritmen som gör att du kan skicka in kund-ID:n eller e-postadresser och skicka ut hash-kodade ID:n.

**Korrigeringar, förbättringar, förbättringar**

* Vi har gjort en konfigurationsuppdatering till `cookieDomain`. ECID-biblioteket filtrerar nu bort den tomma strängen `cookieDomain` i `initConfig` och använder cookie-domänen på den översta nivån, som returneras av metoden getDomain. (CORE-29223)
* Vi har åtgärdat ett fel relaterat till `getVisitorValues` i `localVisitor`. (CORE-31287)
* Vi har åtgärdat ett fel där det fanns en inkonsekvens för MCOPTOUT-värdet i webbläsaren Safari, som returnerades av `getVisitorValue` metoden. (CORE-29719)
* Vi uppdaterade avanmälningsbiblioteket genom `optIn.off` att lägga till för att avbryta prenumerationen på händelser.
* Vi har åtgärdat ett fel som är relaterat till funktionen setTimeout, där `setTimeout` Content Security Policy (CSP) har överträtts på vissa kundsajter. (CORE-30623)

## Version 4.3 {#version-4point3}

**Stöd för ITP 2.1**. Om en spårningsserver anges i en CNAME från en första part placeras en ny cookie (s_ecid) med ECID-värdet. ECID-biblioteket refererar till värdet för att behålla ID:t längre än 7 dagar. Se [ECID-biblioteksmetoder i en Safari ITP-värld](/help/reference/ecid-library-methods.md).

**Felkorrigering för secureCookie-konfiguration.**

## Version 4.1

Uppdatera `publishDestinations` per ny API-ändring. Med den här uppdateringen kan sidans referensinformation visas under ID - synkronisera om så önskas. (CORE-23693)

## Version 4.2

Stöd för plugin-programmet Audience Manager för IAB TCF, tillgängligt via ECID-objektet Opt-in.

**Korrigeringar**

* IAB + OptIn får inte MID för att besöka kunder (CORE-26022)
* Korrigerat fel vid konfiguration av opt-in doesOptInApply i DTM (DTM-12958)
* Avanmäl dig från ECID och inaktivera ID-synk (CORE-23814)

## Version 4.0 {#section-51a4be943bbe41558f196ef2654513e2}

**Anmälningstjänst**. Opt-in är ett tillägg till Experience Cloud ID (ECID) som gör att du kan kontrollera om (och sedan vilka) Experience Cloud-bibliotek kan skapa cookies på webbsidor för besökare. Med hjälp av [Experience Platform Launch](https://docs.adobelaunch.com/)kan ni förenkla insamling av besökares godkännande av deltagande för Experience Cloud-lösning genom att aktivera Analytics, Target, Audience Manager och andra eller alla utvalda Experience Cloud-lösningar för att anmäla sig till ert system för samtyckeshantering.

## Version 3.4 {#section-046ce29b43af47cc849d4091098f5927}

| Objekt | Beskrivning |
|---|---|
| `disableIdSyncs` -flaggan fungerar inte när en sträng skickas. | Åtgärdat. Värden som angetts för `disableidSyncs` parametern för `getInstance` funktionen respekteras nu. |
| iFrames från tredje part hämtar inte ECID | ECID för Safari Mobil och ECID i olika iFrames som inte fungerade har åtgärdats. |
