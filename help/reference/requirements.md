---
description: Granska det här avsnittet för att kontrollera att du använder rätt lösningar, tjänster och kodversioner som krävs av Experience Cloud Identity Service.
keywords: ID Service
seo-description: Granska det här avsnittet för att kontrollera att du använder rätt lösningar, tjänster och kodversioner som krävs av Experience Cloud Identity Service.
seo-title: Krav för Experience Cloud Identity Service
title: Krav för Experience Cloud Identity Service
uuid: 608b1082-6e9e-4101-b6cb-60027950109b
translation-type: tm+mt
source-git-commit: c4c0b791230422f17292b72fd45ba5689a60adae

---


# Requirements for the Experience Cloud Identity Service {#requirements-for-the-experience-cloud-id-service}

Granska det här avsnittet för att kontrollera att du använder rätt lösningar, tjänster och kodversioner som krävs av Experience Cloud Identity Service.

## Krav för att säkerställa att implementeringen lyckas och stöds {#section-15e54a9e9ad2443cb9dc950b4a78f1f1}

En lyckad implementering som stöds uppfyller (eller överskrider) kodkraven och följer instruktionerna så som de visas i [!DNL Adobe] hjälpen. En implementering som inte stöds ger oväntade resultat och förhindrar kundtjänst och våra tekniker från att hjälpa till med felsökning eller lösningar av dina problem med ID-tjänsten.

<table id="table_2216C44AA66248DCAA13BF64BDF2D88A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Implementeringstyp </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <a href="../implementation-guides/standard.md#concept-89cd0199a9634fc48644f2d61e3d2445" format="dita" scope="local"> Standard</a> </p> </td> 
   <td colname="col2"> <p>För en standardimplementering med dynamisk tagghantering (DTM) måste du: </p> 
    <ul id="ul_59CDE179566844B494F3068FF6333809"> 
     <li id="li_CCCB6AFC08EE405F94C42216D3CE50AC"> Placera den inbäddade huvudkoden i <span class="codeph"> &lt;head&gt;</span> -avsnittet på sidan. </li> 
     <li id="li_13962F2CB1764091A84863BE499675A2">Placera den inbäddade sidfotskoden före den avslutande <span class="codeph"> &lt;/body&gt;</span> -taggen. </li> 
    </ul> <p>En standardimplementering stöds inte när du: </p> 
    <ul id="ul_3B62559317ED4C7AA548C3B8DBA281F7"> 
     <li id="li_1F16C6D412944197BEA56BC24730782C"> Placera någon av dessa DTM-inbäddningskoder någon annanstans i koden och/eller sidkoden. </li> 
     <li id="li_05615C01F3A947BBBD41046E68377224"> Lägg till, lägg till eller läs in DTM-kod med asynkrona metoder, anrop/callback-metoder eller wrappers. </li> 
     <li id="li_B2137DFF627B473FA876580449026D2B">Inkludera flera instanser av inbäddningskod på samma sida. </li> 
    </ul> <p>Se även <a href="https://marketing.adobe.com/resources/help/en_US/dtm/?f=deployment.html" format="https" scope="external"> Bädda in kod och Värdalternativ</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <a href="../implementation-guides/implementation-guides.md#section-2c4f2db1f9704315a7cccab6d2e07113" format="dita" scope="local"> Implementeringar som inte är standard </a> </p> </td> 
   <td colname="col2"> <p>För icke-standardiserade eller manuella implementeringar måste du konfigurera ID-tjänsten enligt anvisningarna i den här handboken. Precis som med DTM-riktlinjerna ovan skapar felaktig kodplacering och inläsning en implementering som inte stöds. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Krav för Experience Cloud: Organisations-ID {#section-a02f537129a64ffbb690d5738d360c26}

Om du vill använda ID-tjänsten måste ditt företag vara aktiverat för [!DNL Experience Cloud] och ha ett organisations-ID. Kontrollera följande lista om du är osäker på företagets [!DNL Experience Cloud] status och behöver hitta ditt organisations-ID.

>[!IMPORTANT]
>
>Organisations-ID är skiftlägeskänsligt och måste användas exakt som angivet.

<table id="table_6C74B676EB094C568D2439FDCC9A7830"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Experience Cloud-status </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Aktiverad</b> </p> </td> 
   <td colname="col2"> <p>Om ditt företag är aktiverat för <span class="keyword"> Experience Cloud</span> men du inte har ditt företags-ID, se Organisations-ID <a href="https://marketing.adobe.com/resources/help/en_US/mcloud/organizations.html" format="https" scope="external"> (rulla ned till avsnittet</a> Hitta ditt företags-ID <i></i>). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Osäker</b> </p> </td> 
   <td colname="col2"> <p> Om du inte känner till ditt företags <span class="keyword"> Experience Cloud</span> -status kan du fråga vem som hanterar ditt Adobe-konto om medlemmar i ditt företag kan logga in på <a href="https://marketing.adobe.com" format="https" scope="external"> marketing.adobe.com</a> med ett Adobe-ID. Om du kan det är du aktiverad och en administratör kan visa ditt organisations-ID. Information om organisation-ID finns i avsnittet Administrationssida i <a href="https://marketing.adobe.com/resources/help/en_US/mcloud/?f=admin_getting_started" format="https" scope="external"> Experience Cloud-administration</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b>Ej aktiverad</b> </p> </td> 
   <td colname="col2"> <p> Om ditt företag inte har aktiverats för Experience Cloud läser du <a href="https://marketing.adobe.com/resources/help/en_US/mcloud/?f=core_services.html" format="https" scope="external"> Core Services - Aktivera dina lösningar</a> för att komma igång. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Analyskrav: Regional datainsamling (RDC) {#section-7d04bb013bc84a25bae3b148bc0ca25f}

Alla spårningsservrar har konverterats till RDC, så det finns inget behov av att ändra analysspårningsservern. [Mer information...](https://docs.adobe.com/content/help/en/analytics/admin/data-collection/regional-data-collection/regional-data-collection.html)

## Kodbibliotek och versionskrav {#section-ad7542a4317d430fa79fc6b095beb84d}

I följande avsnitt listas de lägsta kodversionerna som krävs för att använda [!DNL Experience Cloud] ID-tjänsten.

>[!TIP]
>
>Vi rekommenderar att du använder de senaste kodversionerna i stället för de nödvändiga minimumen.

**JavaScript**

<table id="table_8E773F76DBCB4797A0C117080CA8707C"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Experience Cloud-lösning </th> 
   <th colname="col3" class="entry"> Kodbibliotek </th> 
   <th colname="col4" class="entry"> Versionskrav </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b> <span class="keyword"> Experience Cloud</span> ID-tjänst</b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> VisitorAPI.js</span> </p> </td> 
   <td colname="col4"> <p>2.0 eller senare </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="2"> <p> <b> <span class="keyword"> Analytics </span></b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> AppMeasurement.js</span> </p> <p>Se <a href="https://marketing.adobe.com/resources/help/en_US/sc/implement/?f=appmeasure_mjs.html" format="https" scope="external"> AppMeasurement for JavaScript </a>. </p> </td> 
   <td colname="col4"> <p>1.6.4 eller senare. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col3"> <p> <span class="codeph"> s_code.js</span> </p> </td> 
   <td colname="col4"> <p>H.27 </p> <p> <p>Obs!  <span class="keyword"> Analytics</span> s_code version H.27 stöds inte längre i ID-tjänstversion 1.6.0. Uppgradera koden till den senaste versionen av AppMeasurement. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col3"> <p>Videopulsslag </p> <p>Se <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/index.html" format="https" scope="external"> Video Heartbeat 2.x för JavaScript</a>. </p> </td> 
   <td colname="col4"> <p>2.0 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <b> <span class="keyword"> Audience Manager </span></b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> dil.js</span> </p> <p> Se <a href="https://marketing.adobe.com/resources/help/en_US/aam/?f=c_dil.html" format="https" scope="external"> Dataintegreringsbibliotek</a> (DIL). </p> </td> 
   <td colname="col4"> <p>5.0 </p> <p> 
     <draft-comment>
       uppdaterat från 4.9 
     </draft-comment> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="1"> <p> <b> <span class="keyword"> Mål </span></b> </p> </td> 
   <td colname="col3"> <p> <span class="codeph"> mbox.js</span> </p> <p>Se <a href="https://marketing.adobe.com/resources/help/en_US/target/ov/?f=c_mbox_technical.html" format="https" scope="external"> Mbox Code</a>. </p> </td> 
   <td colname="col4"> <p>61 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col3"> <p> <span class="codeph"> at.js</span> </p> <p>Se implementering <a href="https://marketing.adobe.com/resources/help/en_US/target/ov2/c_target-atjs-implementation.html" format="https" scope="external"> av</a>at.js. </p> </td> 
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

SDK-koden måste vara aktiverad för ID-tjänsten. Aktivera och hämta den senaste SDK-koden för varje app från ditt [Adobe Mobile Services](https://mobilemarketing.adobe.com/) -konto. Se även:

* [Konfigurera tjänstalternativ för SDK Visitor ID](https://marketing.adobe.com/resources/help/en_US/mobile/t_config_visitor.html)
* [Android SDK-metoder](https://marketing.adobe.com/resources/help/en_US/mobile/android/c_marketing_cloud.html)
* [iOS SKD-metoder](https://marketing.adobe.com/resources/help/en_US/mobile/ios/marketing_cloud.html)

>[!MORELIKETHIS]
>
>* [Kodbibliotek](../library/library.md#concept-ff27497375644a898d47984aefb21c97)
