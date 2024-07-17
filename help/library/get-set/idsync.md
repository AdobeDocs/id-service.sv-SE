---
description: Med ID-tjänstfunktionerna idSyncByURL och idSyncByDataSource kan du manuellt implementera en ID-synkronisering i iFrame för målpublicering. Dessa finns i VisitorAPI.js version 1.10 eller senare.
keywords: ID-tjänst
title: ID-synkronisering efter URL eller Data Source
exl-id: a22e6b47-00ff-4b51-9958-ddeccc1e507e
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---

# ID-synkronisering efter URL eller Data Source{#id-synchronization-by-url-or-data-source}

Med ID-tjänstfunktionerna idSyncByURL och idSyncByDataSource kan du manuellt implementera en ID-synkronisering i iFrame för målpublicering. Dessa finns i VisitorAPI.js version 1.10 eller senare.

## Syntax, egenskaper och makron {#section-90ac61617482463aaf4c57009b830332}

**Syntax**

<table id="table_ADC7501511914805A6A6B24B2DFEBA51"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Code </th> 
   <th colname="col2" class="entry"> Synkroniserar användar-ID:n </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr valign="top"> 
   <td colname="col1"> <p> <span class="codeph"> visitor.idSyncByURL(); </span> </p> </td> 
   <td colname="col2"> <p>Mellan olika datapartners och <span class="keyword"> Audience Manager </span> med hjälp av en anpassad URL för ID-synkronisering. </p> </td> 
  </tr> 
  <tr valign="top"> 
   <td colname="col1"> <p> <span class="codeph"> visitor.idSyncByDataSource(); </span> </p> </td> 
   <td colname="col2"> <p>När du redan känner till DPID och DPUID och vill skicka det till <span class="keyword"> Audience Manager </span> i standardformatet för ID-synkronisering. </p> <p></p> </td> 
  </tr> 
 </tbody> 
</table>

**Egenskaper**

I följande tabell visas och definieras de egenskaper som är tillgängliga för båda funktionerna.

<table id="table_5343BE784E694C67B09A0A8878CF8001"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Namn </th> 
   <th colname="col2" class="entry"> Typ </th> 
   <th colname="col3" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr valign="top"> 
   <td colname="col1"> <span class="codeph"> dpid </span> </td> 
   <td colname="col2"> Sträng </td> 
   <td colname="col3"> <p>Data provider-ID tilldelat av Audience Manager. </p> </td> 
  </tr> 
  <tr valign="top"> 
   <td colname="col1"> <span class="codeph"> dpuuid </span> </td> 
   <td colname="col2"> Sträng </td> 
   <td colname="col3"> <p>Dataleverantörens unika ID för användaren. </p> </td> 
  </tr> 
  <tr valign="top"> 
   <td colname="col1"> <span class="codeph"> minuterToLive </span> </td> 
   <td colname="col2"> Nummer </td> 
   <td colname="col3"> <p> <i>(Valfritt)</i> Anger förfallotid för cookie. Måste vara ett heltal. Standardvärdet är 2 0160 minuter (14 dagar). </p> </td> 
  </tr> 
  <tr valign="top"> 
   <td colname="col1"> <span class="codeph"> url </span> </td> 
   <td colname="col2"> Sträng </td> 
   <td colname="col3"> <p>Mål-URL. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Makron**

Båda funktionerna kan hantera följande makron:

* `%TIMESTAMP%`: Skapar en tidsstämpel (i millisekunder). Används för cachebusting.
* `%DID%`: Infogar användarens Audience Manager-ID.
* `%HTTP_PROTO%`: Anger kommunikationsprotokollet (`http` eller `https`).

## Exempelkod och utdata {#section-0115615c37584a19a2ab11e917c4e7e9}

Båda funktionerna returnerar `Successfully queued` om de lyckas. De returnerar en felmeddelandesträng om de inte gör det.

### visitor.idSyncByURL

**Exempelkod**

```javascript
   //Instatiate Visitor
    var visitor = Visitor.getInstance
    ("MARKETING-CLOUD-ORG-ID-HERE",{}); 
   // Fires url with macros replaced 
    visitor.idSyncByURL({ 
    dpid: '24', // must be a string 
    url: '//su.addthis.com/red/usync?pid=16&puid=%DID%&url=%HTTP_PROTO%://
    dpm.demdex.net/ibs:dpid=420&dpuuid={{uid}}', 
    minutesToLive: 20160 // optional, defaults to 20160 minutes (14 days) });
```

**Exempelutdata**

```
http://su.addthis.com/red/usync?pid=16&puid=28777806459181003670799219185178493848&url=http%3A%2F%2Fdpm.demdex.net%2Fibs%3Adpid%3D420%26dpuuid%3D%7B%7Buid%7D%7D
```

### visitor.idSyncByDataSource

**Exempelkod**

```javascript
  //Instantiate Visitor
   var visitor = Visitor.getInstance
   ("MARKETING-CLOUD-ORG-ID-HERE",{}); 
  // Fires 'http:/https:' + '//dpm.demdex.net/ibs:dpid=&dpuuid='
   visitor.idSyncByDataSource({ 
     dpid: '24', // must be a string
     dp     minutesToLive: 20160 // optional, defaults to 20160 minutes (14 days) });
```

**Exempelutdata**

```
http://dpm.demdex.net/ibs:dpid=24&dpuuid=98765
```

>[!MORELIKETHIS]
>
>* [DIL idSync](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-instance-methods.html#idsync)
