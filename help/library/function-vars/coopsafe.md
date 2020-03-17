---
description: En valfri boolesk konfiguration som avgör om ID-tjänsten skickar (eller inte skickar) data till Adobe Experience Cloud Device Co-op.
keywords: ID Service
seo-description: En valfri boolesk konfiguration som avgör om ID-tjänsten skickar (eller inte skickar) data till Adobe Experience Cloud Device Co-op.
seo-title: isCoopSafe
title: isCoopSafe
uuid: 4dfa1f35-0a88-48d1-9484-d88cb53ad461
translation-type: tm+mt
source-git-commit: c4c0b791230422f17292b72fd45ba5689a60adae

---


# isCoopSafe{#iscoopsafe}

En valfri boolesk konfiguration som avgör om ID-tjänsten skickar (eller inte skickar) data till Adobe Experience Cloud Device Co-op.

Innehåll:

<ul class="simplelist"> 
 <li> <a href="../../library/function-vars/coopsafe.md#section-4883eda6beb8437182bcc82bb58fae41" format="dita" scope="local"> Krav </a> </li> 
 <li> <a href="../../library/function-vars/coopsafe.md#section-d18af2b903f248e18ae8108aaf0a8ebb" format="dita" scope="local"> Användningsexempel </a> </li> 
 <li> <a href="../../library/function-vars/coopsafe.md#section-952f56724a2b4d349340e26fbaf33ddd" format="dita" scope="local"> Exempel på syntax och kod </a> </li> 
 <li> <a href="../../library/function-vars/coopsafe.md#section-fcd441933506493faefaa6b51f194a17" format="dita" scope="local"> POST-parametrar för händelseanrop </a> </li> 
 <li> <a href="../../library/function-vars/coopsafe.md#section-9281c39c8b6249d7864100b5cbca7dc6" format="dita" scope="local"> API:er efter instansiering </a> </li> 
</ul>

## Krav {#section-4883eda6beb8437182bcc82bb58fae41}

För att kunna använda `isCoopSafe` måste du:

* Använd ID-tjänstkoden version 2.4 eller senare.
* Delta i [Experience Cloud Device Co-op](https://marketing.adobe.com/resources/help/en_US/mcdc/). Medlemmar som arbetar med potentiella partners bör också granska denna dokumentation för att avgöra om `isCoopSafe` möjliga frågor om hur data används för att skapa enhetsgrafen tas upp.

* Samarbeta med din [!DNL Adobe] konsult för att ange en vitlistefärg eller svartlistningsflagga på ditt Device Co-op-konto. Det finns ingen självbetjäningsväg för att aktivera dessa flaggor.

## Användningsexempel {#section-d18af2b903f248e18ae8108aaf0a8ebb}

`isCoopSafe` hjälper till att lösa 2 användningsfall som rör datainsamling av aktuella eller potentiella medlemmar i Device Co-op. De här användningsexemplen gäller hur besöksdata för webbplatsen skickas vidare till Device co-op för att hjälpa till att skapa enhetsdiagrammet. I följande tabell beskrivs hur `isCoopSafe` fungerar med dessa användningsfall för att blockera eller skicka data till enhetsdiagrammet

<table id="table_A24C63D2A21F47EDBAC8FA5E7BE888D8"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Användningsfall </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Autentiserade besökare</b> </p> </td> 
   <td colname="col2"> <p>Lägg till <span class="codeph"> isCoopSafe </span> i ID-tjänstkoden för att styra hur data för autentiserade besökare som har eller inte har godkänt avtal för användning används av Device Co-op för att skapa enhetsgrafen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>DIL på tredjepartswebbplatser</b> </p> </td> 
   <td colname="col2"> <p>Lägg till <span class="codeph"> isCoopSafe </span> i din ID-tjänstkod för användning på tredjepartswebbplatser där du: </p> <p> 
     <ul id="ul_C27BB26510314834A2A7CD99D46DA4AC"> 
      <li id="li_4E6AE574F18646F09C0CF4553EEA1A9E">Det går inte att se till att autentiserade besökare har eller inte har godkänt användningsvillkor. </li> 
      <li id="li_26D0561BF32B4278B0A6B5082C17FED8">Måste styra hur dessa data används av Device Co-op för att skapa enhetsgrafen. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exempel på syntax och kod {#section-952f56724a2b4d349340e26fbaf33ddd}

**Syntax:** `isCoopSafe: true | false`

De booleska alternativen avgör hur kunddata används eller inte används av Device Co-op.

* `isCoopSafe: true`: Besöksdata som samlats in av en mobil SDK eller webbplats *kan* användas för att skapa enhetsgrafen.

* `isCoopSafe: false`: Besöksdata som samlats in av en mobil SDK eller webbplats *kan inte* användas för att skapa enhetsgrafen.

**Kodexempel**

Ange detta när ID-tjänstkoden instansieras:

```js
var visitor = Visitor.getInstance("Insert Experience Cloud organization ID here",{ 
     ... 
     isCoopSafe: true 
});
```

## POST-parametrar för händelseanrop {#section-fcd441933506493faefaa6b51f194a17}

Beroende på vilken flagga du anger ( `true` eller `false`) översätts ID-tjänsten `isCoopSafe` till dessa POST-parametrar och skickar dem till [!DNL Adobe] i ett händelseanrop:

* `d_coop_safe=1`
* `d_coop_unsafe=1`

POST-parametrarna anger för Device Co-op om det kan eller inte kan inkludera användardata i enhetsdiagrammet. [!DNL Experience Cloud] Tabellen nedan definierar relationen mellan de `isCoopSafe` booleska flaggorna och POST-parametrarna som skickas i ett händelseanrop. Om du inte använder `isCoopSafe`det skickas ingen av dessa i ett händelseanrop.

<table id="table_0A544534CA904F4D9836A34B8C1EACBB"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Konfigurationsstatus </th> 
   <th colname="col2" class="entry"> POST-parameter </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> isCoopSafe: true </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> d_coop_safe=1 </span> </p> <p>Device Co-op kan använda besöksdata för att skapa enhetsdiagrammet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> isCoopSafe: false </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> d_coop_unsafe=1 </span> </p> <p>Device Co-op kan inte använda besöksdata för att skapa enhetsdiagrammet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## API:er efter instansiering {#section-9281c39c8b6249d7864100b5cbca7dc6}

Med dessa API:er kan du åsidosätta `isCoopSafe` statusen. Dessa är nödvändiga eftersom de gör att du kan ändra en besökares status efter instansiering/efter inloggning på en webbplats eller i en app för en sida där sidan inte uppdateras. Du måste till exempel anropa dessa API:er om en användare autentiserar till din webbplats eller app och senare accepterar en användarvillkorsprincip som tillåter Device Co-op att använda deras data.

<table id="table_BAA96B1F82BE48C3A61A1AF1367BA45C"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> visitor.setAsCoopSafe(); </span> </p> </td> 
   <td colname="col2"> <p>Anger POST-parametern <span class="codeph"> d_coop_safe=1 </span> i alla efterföljande händelseanrop. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> visitor.setAsCoopUnsafe(); </span> </p> </td> 
   <td colname="col2"> <p>Anger POST-parametern <span class="codeph"> d_coop_unsafe=1 </span> i alla efterföljande händelseanrop. </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--
Wiki page https://wiki.corp.adobe.com/x/RCfFTg
-->

>[!MORELIKETHIS]
>
>* [DIL isCoopSafe](https://marketing.adobe.com/resources/help/en_US/aam/dil-coopsafe.html)

