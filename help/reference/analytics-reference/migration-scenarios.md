---
description: Innehåller exempelkonfigurationer för servern och nödvändiga migreringssteg.
keywords: ID-tjänst
title: Migreringsscenarier för Experience Cloud Identity Service
exl-id: 419532bf-399f-4646-a95f-31c35535d6fc
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Migreringsscenarier för Experience Cloud Identity Service {#experience-cloud-id-service-migration-scenarios}

Innehåller exempelkonfigurationer för servern och nödvändiga migreringssteg.

## Enskild webbegenskap {#section-6ccfea84628d46c99507cb124e7f5445}

* **Kund**: Exempel på Company Inc.
* **Experience Cloud aktiverad**: Nej
* **Webbegenskaper**: example.com
* **Datainsamlingsservrar**: metrics.example.com, smetrics.example.com
* **Analyserar JavaScript-fil**: En enda fil för alla webbplatssidor

Först måste den här kunden aktiveras för Experience Cloud (se [kraven](../../reference/requirements.md)). Och eftersom de har en enda JavaScript-fil behöver kunden ingen respitperiod. Den här kunden kommer också att konfigurera migrering av besökare och sedan migrera bort från sin datainsamling CNAME, vilket inte är nödvändigt.

## Flera JavaScript-filer, hårdkodade bildtaggar {#section-a665f6ee202940449198e4e7a5dcac54}

* **Kund**: Ett annat exempel på Company Inc.
* **Experience Cloud aktiverad**: Ja
* **Webbegenskaper**: anotherexample.com
* **Datainsamlingsservrar**: anotherexampleco.112.2o7.net
* **Analyserar JavaScript-fil**: Flera JavaScript-filer. En fil för huvudplatsen, en annan fil för supportavsnittet som finns i ett separat CMS-system.
* **Andra datainsamlingsmetoder**: Hårdkodade bildtaggar i ett webbplatsavsnitt

Först ska kunden hitta sitt Adobe Experience Cloud Organization ID (se [kraven](../../reference/requirements.md)). Därefter bör de konfigurera en tidsgräns för migrering eftersom de använder flera JavaScript-filer. Den här kunden konfigurerar även migrering av besökare och migrerar sedan från `*.2o7.net` till `*.sc.omtrdc.net`.

När den här kunden uppdaterar den senaste Analytics JavaScript-koden som förberedelse för lanseringen av [!DNL Experience Cloud] ID-tjänsten kommer de även att uppdatera alla hårdkodade bildtaggar så att de använder JavaScript i stället.

## Flera webbegenskaper, flera JavaScript-filer och en Flash-baserad videospelare {#section-34647995ff3740b999fdee22d885e515}

* **Kund**: En bra kund, LLC
* **Experience Cloud aktiverad**: Ja
* **Webbegenskaper**: mymainsite.com, myothersiteA.com, myothersiteB.com
* **Datainsamlingsservrar**: metrics.mymainsite.com, smetrics.mymainsite.com
* **Analyserar JavaScript-fil**: Flera JavaScript-filer. En fil för varje webbegenskap.
* **Andra datainsamlingsmetoder**: En Flash-baserad videospelare

Först ska kunden hitta sitt Adobe Experience Cloud Organization ID (se [kraven](../../reference/requirements.md)). Därefter bör de konfigurera en tidsgräns för migrering eftersom de använder flera JavaScript-filer. Den här kunden spårar besökare mellan sin primära domän och sina underdomäner, så de kommer att fortsätta använda sin datainsamling CNAME med besökar-ID-tjänsten.

När den här kunden uppdaterar den senaste Analytics JavaScript-koden som förberedelse för lanseringen av [!DNL Experience Cloud] ID-tjänsten kommer de också att uppdatera sin videospelare till den senaste Flashen av AppMeasurementet för Flash.
