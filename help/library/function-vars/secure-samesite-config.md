---
description: En konfiguration inom ECID som kan användas för att stödja AMCV-cookies på Google AMP-sidor.
keywords: ID-tjänst
seo-description: En konfiguration inom ECID som kan användas för att stödja AMCV-cookies på Google AMP-sidor.
seo-title: Säkra konfigurationer och samma webbplats
title: Säkra konfigurationer och samma webbplats
translation-type: tm+mt
source-git-commit: 702d20f3989f7749fb173496765d94c3a5af46dc
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 1%

---


# Säkra konfigurationer och samma webbplats

Med den här konfigurationen kan du ändra inställningarna för dina cookies och ha stöd för [AMCV-cookies](../../introduction/cookies.md) på Google AMP-sidor.

Adobe besökar-ID-tjänsten ställer in ECID-cookies med webbläsarens standardinställning `SameSite = Lax`, som inte är tillgänglig om sidan läses in i en iframe som en Google AMP-sida. Använd nedanstående konfigurationer för att uppdatera inställningen för SameSite till `SameSite = None` för att få åtkomst till ECID-cookies.

>[!NOTE]
>
>När du använder `SameSite = None` måste cookies anges till `Secure`, så att data bara kan skickas via HTTPS-anslutningar.

**Implementering**:

Om du använder Adobe Experience Platform Launch uppgraderar du ditt Experience Cloud ID-tillägg till version 5.1.0 och konfigurerar `secureCookie: true` och `sameSiteCookie: none`.

Om du inte använder Experience Platform Launch uppdaterar du till det senaste Visitor 5.1.0-biblioteket och följer konfigurationerna nedan när du initierar Visitor-instansen:

**Exempel på kod**

```js
var visitor = Visitor.getInstance("IMSORG_ID", {

     secureCookie: true,

     sameSiteCookie: "None"

});
```
