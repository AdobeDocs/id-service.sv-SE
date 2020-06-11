---
description: Anslut deras CMP (Consent Management Platform) med plugin-programmet Audience Manager för IAB Transparency and Consent Framework (TCF).
seo-description: Anslut deras CMP-plattform (Consent Management Platform) med Audience Manager-plugin för IAB Transparency och Consent Framework (TCF).
seo-title: Använda Opt-in-tjänster med IAB Framework
title: Använda Opt-in-tjänster med IAB Framework
uuid: 8df39d9c-c016-490e-b4db-d02e4044b480
translation-type: tm+mt
source-git-commit: 4c37c8dd3b76dbf17b955864f0562363350eaecd
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Använda Opt-in-tjänster med IAB Framework{#using-opt-in-services-with-iab-framework}

>[!IMPORTANT] Följande dokument gäller endast IAB 2.0. Användare måste använda Visitor.js version 5.0 för att arbeta med IAB 2.0.

Anslut CMP (Consent Management Platform) med plugin-programmet IAB Transparency and Consent Framework (TCF).

Adobe Audience Manager-kunder som använder [IAB TCF](https://iabtechlab.com/standards/gdpr-transparency-and-consent-framework/) kan ansluta sin CMP-plattform (Consent Management Platform) till Opt-ins IAB TCF-plugin. Opt-in är en funktion som är inbäddad i ECID JavaScript-biblioteket och som kan inaktivera enskilda Adobe-lösningsbibliotek beroende på vilka besökarinställningar som har angetts i en CMP. När Opt-ins IAB TCF plugin implementeras med ECID-biblioteket mappas besökarinställningarna från din CMP som stöder IAB TCF automatiskt till Opt-in. Dessa inställningar aktiverar Audience Manager-baserade bibliotek (DIL och ECID) och tillhörande samtal när samtycke tas emot.

## Implementera en CMP som stöder IAB {#section-9fd2403b548947dbb1921ac6ff9d0c82}

Om du vill använda Opt-In för att integrera med IAB TCF måste du slutföra följande:

1. Implementera en CMP som har stöd för IAB och är [registrerad som IAB-leverantör](https://vendorlist.consensu.org/vendorlist.json) eller utveckla en intern CMP som implementerar IAB TCF-specifikationen och registrerar sig som CMP med IAB TCF.
1. Definiera/läs in `__tcfapi` innan Adobe JS läses in.

Mer information finns i [Interactive Advertising Bureau docs](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/TCF-Implementation-Guidelines.md).

## Aktivera plugin-programmet IAB TCF i ditt ECID Javascript-bibliotek {#section-77bf1b9ed67241a59e56c21ab752e82f}

>[!NOTE]
>
>Anmäl dig endast i ECID 4.0+.

Använd Adobe Experience Platform Launch för att implementera plugin-programmet IAB TCF för din webbplats. När du aktiverar IAB för anmälan manuellt bör du kontrollera att följande inställningar är inställda på true i Visitor-objektet:

```javascript
Visitor.getInstance("YOUR_ORG_ID", {  
  doesOptInApply: true,
  isIabContext: true
});
```

När inställningarna har konfigurerats på rätt sätt kommer ECID- och DIL-bibliotek att aktiveras/inaktiveras beroende på medgivandekriterier från CMP och IAB TCF.

>[!IMPORTANT]
>
>Audience Manager behöver samtycke för *Syfte 1 och Syfte 10, plus leverantörssamtycke* för att kunna distribuera cookies och initiera eller respektera ID-synkroniseringar. Läs mer om plugin-programmet IAB TCF för deltagande i dokumentationen för Audience Manager [här](https://docs.adobe.com/help/en/audience-manager/user-guide/overview/gdpr/aam-iab-plugin.html).

Mer information om hur du validerar Opt-ins IAB TCF plugin finns i användningsfall nr 4 i valideringsguiden [här](../../implementation-guides/opt-in-service/testing-optin-and-iab-plugin.md#section-ca5c6f92fbdf4fd29b4acb6b644efbd0).

## Relaterad dokumentation {#section-55da1110051a4b39b1037803f4a7b264}

* [IAB Transparency and Consent Framework (TCF)](https://iabtechlab.com/standards/gdpr-transparency-and-consent-framework/) - Mer information om IAB-standarden
* [Adobe-deltagande](../../implementation-guides/opt-in-service/optin-overview.md#concept-f9b5db0d27a245fbadd3e19162319360) - För mer information om deltagande, en nödvändig komponent för samtyckeshantering i plattformslösningar
* Stöd för IAB Transparency och Consent Framework (TCF) [i Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)
* [Dina sekretessval](https://www.adobe.com/privacy/opt-out.html#customeruse) - Ett annat sekretessalternativ som dina användare har tillgång till är möjligheten att avanmäla all datainsamling med andra globala avanmälningsverktyg. Global avanmälan har företräde framför avanmälan och IAB TCF-verifiering