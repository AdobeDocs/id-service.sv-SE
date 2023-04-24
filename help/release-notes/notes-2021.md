---
description: Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.
keywords: ID-tjänst
title: Versionsinformation 2021
source-git-commit: dce2c0036f697507381d0763c2f6a9538155681c
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---

# Versionsinformation om Experience Cloud Identity Service - 2021

Funktionsreleaser, uppdateringar eller ändringar av Experience Cloud Identity Service.

## Besökare 5.3.0

Följande uppdateringar ingick i Visitor 5.3.0:

* Uppdaterad algoritm för att generera lokalt ECID.
* Senaste deltagande med `Secure` och `SameSite` flaggar för sekretesskaka.
* Korrigering för ett Firefox-webbläsarproblem när en sida läses in i en underordnad iFrame.

## Besökare 5.2.0

Följande uppdateringar ingick i Visitor 5.2.0:

* Den här versionen introducerar en händelse `onRecieveEcid`som anropas när ett ECID tas emot från identitetstjänsten. Exempel:

```js
visitorInstance.onRecieveEcid(callback(ecid){
 console.log(ecid)
})
```
