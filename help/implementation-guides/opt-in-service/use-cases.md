---
description: Exempel på användningsexempel och lösningar för att hantera avanmälningstjänsten.
seo-description: Exempel på användningsexempel och lösningar för att hantera avanmälningstjänsten.
seo-title: Användningsexempel
title: Användningsexempel
uuid: d75a44d5-b713-43d1-b5b6-95d1d0d213a7
translation-type: tm+mt
source-git-commit: 0c300aa92991c0dec2ccdeeb34f9d886dcac7671
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Användningsexempel {#opt-in-use-cases}

Exempel på användningsexempel och lösningar för att hantera avanmälningstjänsten.

## Tips och felsökning {#section-5c566366410f4a8f89eca0d3f556d99f}

* JS-initieringen för besökare är synkron och körs under sidinläsning. Om du interagerar med en CMP- eller permissions-beständighet med hög fördröjning kan det vara bättre att använda de asynkrona funktionerna som beskrivs i [Opt-in-inställningar](../../implementation-guides/opt-in-service/getting-started.md#section-cf9ab638780141c9b62dc57cf00b7047).
* Opt-in är en implementering per domän. Det hanterar inte implementeringar över domäner.
* Om du vill inaktivera tredjepartssamtal för ett visst bibliotek måste du konfigurera den inställningen separat i varje bibliotek.

## Opt-in-scenarier {#section-1178053c065c430bba26f82ef383a71c}

De här användningsexemplen är exempel på hur du använder Opt-in-tjänsten.

<table id="table_83C85343611344D8A8315157C1B4240F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Krav </th> 
   <th colname="col2" class="entry"> Lösningar </th> 
   <th colname="col3" class="entry"> Effekt </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Det går bra att samla in analyser i förhandstillstånd, men alla andra bibliotek kan inte läsas in förrän samtycke tas emot </p> </td> 
   <td colname="col2"> <p>Aktivera Analytics-kategorin i läget för förhandsgodkännande genom att använda Opt-in </p> </td> 
   <td colname="col3"> <p>Analyserna använder analysidentifieraren i stället för ECID i förhandsmedgivandesamlingen. När ECID har godkänts används en ny identifierare och besökaren får ett ECID som kan användas för aktivering och integrering. </p> <p>Besökarfragmentering i pre-/post-medgivande förväntas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Första parts mätning är bra att samla in i förhandstillstånd. Alla andra typer av dataanvändning förhindras tills samtycke erhålls. </p> </td> 
   <td colname="col2"> <p>Använd Opt-in för att aktivera Analytics + ECID-bibliotek i förhandstillstånd. </p> <p>Lägg till konfigurationen"disablethirdpartycookies" i ECID-biblioteket för att blockera cookie-filer från tredje part + ID-synk i förhandstillstånd </p> </td> 
   <td colname="col3"> <p>Adobe Demdex-anrop kommer att utlösas för ECID-hämtning, men ingen Demdex-cookie, annan cookie från tredje part eller ID-synk kommer att finnas. </p> <p>Behåller en konsekvent besökare i pre-/post-medgivande-läge för Analytics. Insamling i förhandstillstånd är knuten till datainsamling efter samtycke. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Mätning från första part plus målgruppsanpassning är acceptabelt i ett förhandstillstånd. Alla andra typer av dataanvändning förhindras tills samtycke erhålls. </p> </td> 
   <td colname="col2"> <p>Använd Opt-in för att aktivera Analytics + ECID + Target Libraries i förhandstillstånd. </p> <p>Lägg till konfigurationen för <span class="codeph"> inaktiveringsbar cookies</span> i ECID-biblioteket för att blockera cookie-filer från tredje part + ID-synk i förhandstillstånd. Ta bort flagga i tillstånd efter samtycke. </p> </td> 
   <td colname="col3"> <p>Adobe Demdex-anropet utlöses för ECID-hämtning, men ingen Demdex-cookie, annan cookie från tredje part eller ID-synk kommer att finnas. </p> <p>Behåller en konsekvent besökare i pre-/post-medgivande-läge för förstahandslösningar. Insamling i förhandstillstånd är knuten till datainsamling efter samtycke. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Inga cookies får anges i ett förhandsmedgivande </p> </td> 
   <td colname="col2"> <p>Använd Opt-in för att blockera alla bibliotek från inläsning tills samtycke tas emot </p> </td> 
   <td colname="col3"> <p>Implementeringen är som förväntat och alla bibliotek, inklusive ECID, läses in i rätt sekvens efter medgivande. </p> <p>Dataförlust för kunder som aldrig ger sitt samtycke till att spåras. </p> </td> 
  </tr> 
 </tbody> 
</table>

