---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID-tjänst
title: Versionsinformation 2020
exl-id: c9d7876e-debc-4c8e-8ebc-91646610c876
source-git-commit: dce2c0036f697507381d0763c2f6a9538155681c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Versionsinformation för Experience Cloud - 2020 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.

## Version 5.1.1

* Korrigering för inställning av AMCV-cookie med `SameSite=None` när VisitorJS läses in i en iFrame.

## Version 5.1.0

* Lägger till `sameSiteCookie`-konfig för att ange attributet `SameSite` för AMCV-cookie. Den här konfigurationen stöder följande värden för attributet `SameSite`:
   * `Strict`
   * `Lax`
   * `None`

Mer information om dessa attributvärden finns på [web.dev](https://web.dev/samesite-cookies-explained/) och [SameSite Updates by The Chromium Projects](https://www.chromium.org/updates/same-site/).

## Version 5.0.1

* Korrigering för att inkludera `d_cf`-flaggan när en ny IAB-medgivandesträng skickas till Adobe Data Collection-kanter.

## Version 5.0.0

* Besöksversion 5.0.0 med stöd för `IAB 2.0`.

## Version 4.6

* Flagga `loadSSL` är aktiverad som standard. Alla anrop till identitetstjänsten är som standard på `https`.  Kunder kan ange det som false om de vill anropa Identity Services på http från sina `non-ssl` sidor.
* Uppdaterade funktionen som används för att identifiera version `Internet-Explorer (IE)`, för att åtgärda ett problem som rapporterats av `ESLint`.
Åtgärda prestandaproblem på `Internet-Explorer (IE) 11` när ECID ges optIn `pre-approval` och uppdateras senare.

## Version 4.5

* Från och med version 4.5 avvisar ECID alla tomma ID:n som skickas till metoden `setCustomerIDs`.
* Ett problem som uppstod när anmälan konfigurerades som `doesOptInApply=false` och `isIabContext=true` har korrigerats.

I [Versionsinformation för Experience Cloud](https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html?lang=sv) finns månadsinformation om alla produkter.
