---
description: Granska det här avsnittet för att kontrollera att du använder rätt lösningar, tjänster och kodversioner som krävs av Experience Cloud identitetstjänst.
keywords: ID-tjänst
title: Krav för Experience Cloud Identity Service
exl-id: ebeac4c7-b36c-4a4e-9378-351fac5baf53
source-git-commit: 00ebcaa16ec6b432b480d96fbf79b6a745515b1b
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# Krav för Experience Cloud Identity Service {#requirements-for-the-experience-cloud-id-service}

Granska det här avsnittet för att kontrollera att du använder rätt lösningar, tjänster och kodversioner som krävs av Experience Cloud identitetstjänst.

## Krav för att säkerställa att implementeringen lyckas och stöds {#section-15e54a9e9ad2443cb9dc950b4a78f1f1}

En lyckad implementering som stöds uppfyller (eller överskrider) kodkraven och följer instruktionerna så som de visas i hjälpen för [!DNL Adobe]. En implementering som inte stöds ger oväntade resultat och förhindrar kundtjänst och våra tekniker från att hjälpa till med felsökning eller lösningar av dina problem med ID-tjänsten.

### Standardimplementeringar

Se [Experience Platform-taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv) för din standardimplementering.

### Implementeringar som inte är standard

För icke-standardiserade eller manuella implementeringar måste du konfigurera ID-tjänsten enligt anvisningarna i den här handboken. Precis som med DTM-riktlinjerna ovan skapar felaktig kodplacering och inläsning en implementering som inte stöds.

## Krav för Experience Cloud: Organisations-ID {#section-a02f537129a64ffbb690d5738d360c26}

Om du vill använda ID-tjänsten måste ditt företag vara aktiverat för [!DNL Experience Cloud] och ha ett organisations-ID. Kontrollera följande lista om du är osäker på företagets [!DNL Experience Cloud]-status och behöver hitta ditt organisations-ID.

>[!IMPORTANT]
>
>Organisations-ID är skiftlägeskänsligt och måste användas exakt som angivet.

<table id="table_6C74B676EB094C568D2439FDCC9A7830"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Status för Experience Cloud </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Aktiverad</b> </p> </td> 
   <td colname="col2"> <p>Om ditt företag är aktiverat för <span class="keyword"> Experience Cloud</span> men du inte har ditt företags-ID, se <a href="https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/organizations.html?lang=sv-SE" format="https" scope="external"> Organisations-ID </a> (rulla ned till avsnittet <i>Hitta ditt företags-ID</i>). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Inte säker</b> </p> </td> 
   <td colname="col2"> <p> Om du inte känner till ditt företags <span class="keyword"> Experience Cloud</span>-status kan du fråga vem som hanterar ditt Adobe-konto om medlemmar i ditt företag kan logga in på <a href="https://experiencecloud.adobe.com" format="https" scope="external"> marketing.adobe.com </a> med hjälp av en Adobe ID. Om du kan det är du aktiverad och en administratör kan visa ditt organisations-ID. Information om organisation-ID finns i avsnittet Administrationssida i <a href="https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=sv-SE" format="https" scope="external"> Administrationssida för Experience Cloud </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Inte aktiverad</b> </p> </td> 
   <td colname="col2"> <p> Om ditt företag inte är aktiverat för Experience Cloud kan du läsa <a href="https://experienceleague.adobe.com/docs/core-services/interface/about-core-services/core-services.html" format="https" scope="external"> Core Services - Aktivera dina lösningar</a> för att komma igång. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Analyskrav: Regional Data Collection (RDC) {#section-7d04bb013bc84a25bae3b148bc0ca25f}

Alla spårningsservrar har konverterats till RDC, så det finns inget behov av att ändra analysspårningsservern. [Mer information..](https://experienceleague.adobe.com/docs/analytics/technotes/rdc/regional-data-collection.html?lang=sv-SE)

## Kodbibliotek och versionskrav {#section-ad7542a4317d430fa79fc6b095beb84d}

I följande avsnitt listas de lägsta kodversionerna som krävs för att använda ID-tjänsten [!DNL Experience Cloud].

>[!TIP]
>
>Vi rekommenderar att du använder de senaste kodversionerna i stället för de nödvändiga minimumen.

**JavaScript**

<table id="table_8E773F76DBCB4797A0C117080CA8707C"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Experience Cloud Solution </th> 
   <th colname="col3" class="entry"> Kodbibliotek </th> 
   <th colname="col4" class="entry"> Versionskrav </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b> <span class="keyword"> Experience Cloud </span> ID-tjänst </b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> VisitorAPI.js</span> </p> </td> 
   <td colname="col4"> <p>2.0 eller senare </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="2"> <p> <b> <span class="keyword"> Analys </span> </b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> AppMeasurement.js</span> </p> <p>Se AppMeasurementet <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=sv-SE" format="https" scope="external"> för JavaScript </a>. </p> </td> 
   <td colname="col4"> <p>1.6.4 eller senare. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col3"> <p> <span class="codeph"> s_code.js</span> </p> </td> 
   <td colname="col4"> <p>H.27 </p> <p> <p>Obs! <span class="keyword"> Analytics</span> s_code version H.27 stöds inte längre i ID-tjänstversionen 1.6.0. Uppgradera koden till den senaste versionen av AppMeasurementet. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col3"> <p>Videopulsslag </p> <p>Se <a href="https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=sv-SE" format="https" scope="external"> Videopulsslag 2.x för JavaScript</a>. </p> </td> 
   <td colname="col4"> <p>2,0 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b> <span class="keyword"> Audience Manager </span> </b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> dil.js</span> </p> <p> Se <a href="https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=sv-SE" format="https" scope="external"> Data Integration Library </a> (DIL). </p> </td> 
   <td colname="col4"> <p>5,0 </p></td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="1"> <p> <b> <span class="keyword"> Mål </span> </b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> mbox.js</span> </p> <p>Se <a href="https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=sv-SE" format="https" scope="external"> mbox-kod</a>. </p> </td> 
   <td colname="col4"> <p>61 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col3"> <p> <span class="codeph"> at.js</span> </p> <p>Se <a href="https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=sv-SE" format="https" scope="external"> at.js-implementering</a>. </p> </td> 
   <td colname="col4"> <p>0.9.1 </p> </td> 
  </tr> 
 </tbody> 
</table>

## SDK-krav för Android och iOS {#section-73b2446fba8e463888642c7d7dfd94f1}

Åtminstone ID-tjänsten kräver SDK-versionerna som listas nedan.

* Android: 4.11.0
* iOS: 4.11.0

>[!TIP]
>
>Vi rekommenderar att du använder de senaste kodversionerna i stället för de nödvändiga minimumen.

SDK-koden måste vara aktiverad för ID-tjänsten. Aktivera och hämta den senaste SDK-koden för varje app från ditt [Adobe Mobile Services](https://mobilemarketing.adobe.com/)-konto. Se även:

* [Konfigurera tjänstalternativ för SDK Visitor ID ](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/t-config-visitor.html?lang=sv-SE)
* [Android SDK-metoder](https://experienceleague.adobe.com/docs/mobile-services/android/experience-cloud-android/c-marketing-cloud.html?lang=sv-SE)
* [iOS SKD-metoder](https://experienceleague.adobe.com/docs/mobile-services/ios/exp-cloud-ios/marketing-cloud.html?lang=sv-SE)

>[!MORELIKETHIS]
>
>* [Kodbibliotek](../library/library.md#concept-ff27497375644a898d47984aefb21c97)
