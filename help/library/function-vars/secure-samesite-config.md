---
description: En konfiguration inom ECID som kan användas för att stödja AMCV-cookies på Google AMP-sidor.
keywords: ID-tjänst
title: Säkra konfigurationer och samma webbplats
exl-id: c3bc44fc-5adc-4eae-8169-9d731d148458
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Säkra konfigurationer och samma webbplats

Med den här konfigurationen kan du ändra inställningarna för dina cookies och ha stöd för [AMCV-cookies](../../introduction/cookies.md) på Google AMP-sidor.

Adobe besökar-ID-tjänsten ställer in ECID-cookies med webbläsarens standardinställning `SameSite = Lax`, som inte är tillgänglig om sidan läses in i en iframe som en Google AMP-sida. Om du vill få åtkomst till ECID-cookies använder du nedanstående konfigurationer för att uppdatera inställningen för SameSite till `SameSite = None`.

>[!NOTE]
>
>När du använder `SameSite = None` måste cookies anges till `Secure`, så att data bara kan skickas via HTTPS-anslutningar.

**Implementering**:

Om du använder Adobe Experience Platform Launch uppgraderar du ditt Experience Cloud ID-tillägg till version 5.1.0 och konfigurerar `secureCookie: true` och `sameSiteCookie: none`.

Om du inte använder Experience Platform Launch uppdaterar du till det senaste Visitor 5.1.0-biblioteket och följer konfigurationerna nedan när du initierar Visitor-instansen:

**Kodexempel**

```js
var visitor = Visitor.getInstance("IMSORG_ID", {

     secureCookie: true,

     sameSiteCookie: "None"

});
```
