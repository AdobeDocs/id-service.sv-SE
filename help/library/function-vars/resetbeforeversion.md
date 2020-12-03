---
description: Med den här konfigurationen kan du rensa överblivna eller inaktuella Experience Cloud-ID:n (ECID) baserat på den ID-tjänstversion som uppdateras.
keywords: ID Service
seo-description: Med den här konfigurationen kan du rensa överblivna eller inaktuella Experience Cloud-ID:n (ECID) baserat på den ID-tjänstversion som uppdateras.
seo-title: resetBeforeVersion
title: resetBeforeVersion
uuid: b00d18b8-6720-42f9-9c83-bd306184cc0c
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---


# resetBeforeVersion{#resetbeforeversion}

Med den här konfigurationen kan du rensa överblivna eller inaktuella Experience Cloud-ID:n (ECID) baserat på den ID-tjänstversion som uppdateras.

Om du anger din ID-tjänstversion som värde för `resetBeforeVersion` variabeln rensas inaktuella ECID:n från klientsidans ID:n.

Vissa villkor, till exempel timeout för sessioner, kan ibland leda till att ett klient-side-ID genereras utan att ID-tjänsten kan hämta ett server-side-ID. När detta inträffar spåras ett överblivet klient-ID av ID-tjänsten utan möjlighet att spåras över domäner eller synkroniseras korrekt med andra lösningar. Beteendet jämför versionen i den aktuella AMCV-cookien med värdet för `resetBeforeVersion`. Om cookie-filen inte finns eller om cookie-filens version är mindre (äldre) än den senaste versionen av `resetBeforeVersion`tas AMCV-cookien bort och ID-tjänsten begär ett nytt ECID.

För besökare som har Demdex-cookies från tredje part i sin webbläsare kontrolleras ECID för att se om det har genererats korrekt med UUID i Demdex-cookien. Om denna kontroll visar sig vara sann kommer det nya ECID att vara detsamma och besökaren kommer att betraktas som ny. Om det ECID som tas bort av någon anledning inte genererades med hjälp av Demdex-cookien, eller om det inte finns någon Demdex-cookie, får besökaren ett nytt ECID och kommer att betraktas som nytt.

**Syntax:** `resetBeforeVersion = "3.3"`

**Exempel på kod**

```js
//Call the ID service 
var visitor = Visitor.getInstance ("Insert Marketing Cloud organization ID here", { 
  
    //Same as s.trackingServer 
    trackingServer: "Insert tracking server here ", 
  
    //Same as s.trackingServerSecure 
    trackingServerSecure: "Insert secure tracking server here", 
  
    //For CNAME support only. Exclude these variables if you're not using CNAME 
    marketingCloudServer: "Insert tracking server here", 
    marketingCloudServerSecure: "Insert secure tracking server here", 
  
    //Changing the version 
    resetBeforeVersion: "3.3" 
});
```

