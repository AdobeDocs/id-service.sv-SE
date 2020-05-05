---
description: I vissa implementeringar skickas besökar-ID:n från JavaScript till en server så att ytterligare analyshändelser (som ett köp) kan skickas av servern.
keywords: ID Service
seo-description: I vissa implementeringar skickas besökar-ID:n från JavaScript till en server så att ytterligare analyshändelser (som ett köp) kan skickas av servern.
seo-title: Implementering på serversidan blandad med JavaScript
title: Implementering på serversidan blandad med JavaScript
uuid: 256ea0e7-1eb4-4c92-9a7e-f61cb1ed13c7
translation-type: tm+mt
source-git-commit: d2bc0e7fedc4e48d51f5dad158f9f8bfcb0cb4f3

---


# Implementering på serversidan blandad med JavaScript {#server-side-implementation-mixed-with-javascript}

I vissa implementeringar skickas besökar-ID:n från JavaScript till en server så att ytterligare analyshändelser (som ett köp) kan skickas av servern.

ID-tjänstens API innehåller de metoder, [getMarketingCloudVisitorID](../../library/get-set/getmcvid.md) och [getAnalyticsVisitorID](../../library/get-set/getanalyticsvisitorid.md), som behövs för att hämta ID-värden som sedan kan skickas till servern.

Se till att du kontrollerar både besökar-ID:t för Experience Cloud och besökar-ID:t för Analytics, och skicka båda ID:n (om sådana finns) för att se till att skickade data är kopplade till den befintliga besökarprofilen för Analytics.

>[!IMPORTANT]
>
>AppMeasurement for Java stöder för närvarande inte Experience Cloud Identity Service.

## API för datainfogning {#section-955ce7664a4646d38b3005cb2df40baf}

Inkludera Analytics-besökar-ID (om det är angivet) i `<visitorID>` -elementet.

Inkludera besökar-ID:t för Experience Cloud i `<marketingCloudVisitorID>` elementet.

Se [XML-märkord](https://www.adobe.io)som stöds.

## AppMeasurement för Java {#section-d664b94934924d048300d9c2b6560085}

Experience Cloud Identity Service stöds för närvarande inte av AppMeasurement for Java.
