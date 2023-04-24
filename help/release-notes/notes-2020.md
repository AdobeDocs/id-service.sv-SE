---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID-tjänst
title: Versionsinformation 2020
exl-id: c9d7876e-debc-4c8e-8ebc-91646610c876
source-git-commit: dce2c0036f697507381d0763c2f6a9538155681c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# Versionsinformation för Experience Cloud - 2020 {#release-notes}

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.

## Version 5.1.1

* Korrigering för inställning av AMCV-cookie med `SameSite=None` när VisitorJS läses in i en iFrame.

## Version 5.1.0

* Lägger till `sameSiteCookie` konfigurera för att ange `SameSite` för AMCV-cookie. Denna konfiguration stöder följande värden för `SameSite` attribute:
   * `Strict`
   * `Lax`
   * `None`

Mer information om attributvärdena finns på [web.dev](https://web.dev/samesite-cookies-explained/) och [SammaWebbplatsuppdateringar av Chromium-projekten](https://www.chromium.org/updates/same-site/).

## Version 5.0.1

* Korrigera för att inkludera `d_cf` flagga när en ny IAB-medgivandesträng skickas till Adobe Data Collection-kanterna.

## Version 5.0.0

* Besöksversion 5.0.0 med stöd för `IAB 2.0`.

## Version 4.6

* Gjord `loadSSL` flagga som standard. Alla anrop till identitetstjänsten är aktiverade `https` som standard.  Kunderna kan ange det till false om de vill anropa Identity Services på http från sina `non-ssl` sidor.
* Uppdaterad funktion som används för att identifiera `Internet-Explorer (IE)` version, för att åtgärda ett problem som rapporterats av `ESLint`.
Åtgärda prestandaproblem på `Internet-Explorer (IE) 11` när ECID ges optIn `pre-approval` och uppdateras senare.

## Version 4.5

* Från och med version 4.5 avvisar ECID alla tomma ID:n som skickas till `setCustomerIDs` -metod.
* Ett problem som uppstod när anmälan konfigurerades som har åtgärdats `doesOptInApply=false` och `isIabContext=true`.

Se [Versionsinformation för Experience Cloud](https://experienceleague.adobe.com/docs/release-notes/experience-cloud/current.html?lang=sv) för månatlig versionsinformation för alla produkter.
