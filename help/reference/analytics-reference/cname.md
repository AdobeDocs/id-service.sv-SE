---
description: Om du har en huvudwebbplats där kunder kan identifieras innan de besöker andra domäner kan en CNAME aktivera spårning av korsdomäner i webbläsare som inte accepterar cookies från tredje part (som Safari).
keywords: operationsordning;ID-tjänst
title: CNAME - implementeringsöversikt
exl-id: f95dda3c-7bb2-4c7d-a25a-a4d20b58fe27
source-git-commit: d2586fc722be25df1b82caaf2cc6de6a2a6c31bf
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# CNAME - implementeringsöversikt{#cname-implementation-overview}

Med CNAME-implementeringar kan du anpassa den samlingsdomän som används av Adobe så att de matchar din egen domän. Dessa domäner kallas även för samlingsdomäner från första part. Dessa implementeringar gör att Adobe kan ställa in cookies från första part på serversidan i stället för på klientsidan med JavaScript. Tidigare var dessa cookies på serversidan inte föremål för begränsningar som infördes enligt Apple ITP-policy (Intelligent Tracking Prevention). I november 2020 [!DNL Apple] uppdaterade sina principer så att dessa begränsningar även tillämpades på cookies som angetts via CNAME. För närvarande är både cookies som anges på serversidan via CNAME och cookies som anges på klientsidan via Javascript begränsade till en sjudagars eller 24 timmars förfallotid under ITP. Mer information om ITP-policyn finns i [!DNL Apple] dokument [om förebyggande av spårning](https://webkit.org/tracking-prevention/#intelligent-tracking-prevention-itp).

En CNAME-implementering ger inga fördelar vad gäller cookie-livstid, men det kan finnas andra fördelar. Fördelarna är annonsblockerare och mindre vanliga webbläsare som förhindrar att data skickas till domäner som de klassificerar som spårare. I dessa fall kan användning av CNAME förhindra att datainsamlingen avbryts för användare som använder dessa verktyg.

Dessutom kan du med CNAME-implementeringar [välj en anpassad RDC-typ](https://experienceleague.adobe.com/docs/analytics/technotes/rdc/regional-data-collection.html?lang=en) som styr var användarnas träffar dirigeras från början. De flesta kunder använder inte anpassade RDC-typer.
