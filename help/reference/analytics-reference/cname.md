---
description: Om du har en huvudwebbplats där kunder kan identifieras innan de besöker andra domäner kan en CNAME aktivera spårning av korsdomäner i webbläsare som inte accepterar cookies från tredje part (som Safari).
keywords: operationsordning;ID-tjänst
title: CNAME - implementeringsöversikt
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# CNAME - implementeringsöversikt{#cname-implementation-overview}

Med CNAME-implementeringar kan du anpassa den samlingsdomän som används av Adobe så att de matchar din egen domän. Detta gör att Adobe kan ställa in cookies från första part på serversidan i stället för på klientsidan med JavaScript. Tidigare var dessa cookies på serversidan inte föremål för begränsningar som infördes enligt Apples ITP-policy (Intelligent Tracking Prevention). I november 2020 uppdaterade [!DNL Apple] dock sina principer så att dessa begränsningar även tillämpades på cookies som angetts via CNAME. För närvarande är både cookies som anges på serversidan via CNAME och cookies som anges på klientsidan via Javascript begränsade till en sjudagars eller 24 timmars förfallotid under ITP. Mer information om ITP-principen finns i det här [!DNL Apple]-dokumentet [om spårningsskydd](https://webkit.org/tracking-prevention/#intelligent-tracking-prevention-itp).

En CNAME-implementering ger inga fördelar vad gäller cookie-livstid, men det kan finnas andra fördelar som annonsblockerare och mindre vanliga webbläsare som förhindrar att data skickas till domäner som de klassificerar som spårare. I sådana fall kan användning av CNAME förhindra att datainsamlingen avbryts för användare som använder dessa verktyg.