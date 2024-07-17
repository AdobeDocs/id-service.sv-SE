---
description: I vissa implementeringar skickas besökar-ID:n från JavaScript till en server så att ytterligare analyshändelser (som ett köp) kan skickas av servern.
keywords: ID-tjänst
title: Implementering på serversidan blandat med JavaScript
exl-id: 1986ee11-2021-4f34-bb56-6eaa87b6dd6d
source-git-commit: fa2549090e6790763a7ac6b87348789678d18ab6
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Implementering på serversidan blandat med JavaScript {#server-side-implementation-mixed-with-javascript}

I vissa implementeringar skickas besökar-ID:n från JavaScript till en server så att ytterligare analyshändelser (som ett köp) kan skickas av servern.

ID-tjänstens API innehåller metoderna [getMarketingCloudVisitorID](../../library/get-set/getmcvid.md) och [getAnalyticsVisitorID](../../library/get-set/getanalyticsvisitorid.md) för att hämta ID-värden som sedan kan skickas till servern.

Kontrollera att du har både besökar-ID och besökar-ID för Analytics och skicka båda ID:n (om sådana finns) för att se till att skickade data är kopplade till den befintliga besökarprofilen för Analytics.

>[!IMPORTANT]
>
>AppMeasurementet för Java stöder för närvarande inte Experience Cloud Identity Service.

## API för datainfogning {#section-955ce7664a4646d38b3005cb2df40baf}

Inkludera Analytics-besökar-ID (om det har angetts) i elementet `<visitorID>`.

Inkludera besökar-ID:t för Experience Cloud i elementet `<marketingCloudVisitorID>`.

Se [XML-taggar som stöds](https://developer.adobe.com/).

## AppMeasurement för Java {#section-d664b94934924d048300d9c2b6560085}

Identitetstjänsten Experience Cloud stöds för närvarande inte av AppMeasurementet för Java.
