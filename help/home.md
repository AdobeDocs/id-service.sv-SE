---
description: 'Experience Cloud Identity Service tillhandahåller ett universellt, beständigt ID som identifierar era besökare i alla lösningar i Experience Cloud. '
keywords: ID Service
seo-description: Adobe Experience Cloud Identity Service (ID-tjänst) ger ett universellt, beständigt ID som identifierar era besökare i alla lösningar i Experience Cloud. Den kan ersätta ID-genereringskoden för tjänster som Analytics, Audience Manager, Target och andra Experience Cloud-lösningar eller -funktioner.
seo-title: Experience Cloud Identity Service
title: Experience Cloud Identity Service
uuid: b68194b5-e549-4f6f-bfaf-7744926aeaac
translation-type: tm+mt
source-git-commit: 21fb12b817b7c8cd34e6022ca6c188229228d1df

---


# Adobe Experience Cloud Identity Service {#experience-cloud-id-service}

Adobe Experience Cloud Identity Service (ID-tjänst) ger ett universellt, beständigt ID som identifierar era besökare i alla lösningar i Experience Cloud. Den kan ersätta ID-genereringskoden för tjänster som Analytics, Audience Manager, Target och andra Experience Cloud-lösningar eller -funktioner.

<table id="table_5E612F746A704FE095B809A013EE977F" class="simpletable"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <b>Komma igång</b> </p> <p> 
     <ul id="ul_D5EC6A54A03F4AB595B588116A7C1296"> 
      <li id="li_845F6DE25A1241439BCDCBC00459D7EB"> <a href="introduction/overview.md" format="dita" scope="local"> Översikt </a> </li> 
      <li id="li_47F399E1D4AF4F08BD647DF01A423BA7"> <a href="reference/requirements.md" format="dita" scope="local"> Krav för Experience Cloud Identity Service </a> </li> 
      <li id="li_CBEEE79B45644F28A52B58DDF23DAD4F"> <a href="implementation-guides/standard.md#concept-89cd0199a9634fc48644f2d61e3d2445" format="dita" scope="local"> Standardimplementering med DTM </a> </li> 
     </ul> </p> <p><b>JavaScript-bibliotek för Experience Cloud ID</b> </p> <p>JavaScript för Experience Cloud Identity Service finns på: <a href="https://github.com/Adobe-Marketing-Cloud/id-service/releases" format="https" scope="external"> https://github.com/Adobe-Marketing-Cloud/id-service/releases</a> </p> <p> <b>Nya eller aktuella objekt</b> </p> <p> 
     <ul id="ul_B0A25B6827734D55BB1E20D12334AC21"> 
      <li id="li_A66924F4948F4A5ABA545A89A28A6F6A"><a href="implementation-guides/opt-in-service/optin-overview.md#concept-f9b5db0d27a245fbadd3e19162319360" format="dita" scope="local"> Anmälningstjänst</a> </li> 
      <li id="li_92D49CB788AD478EA74BCF5328CB9A14"> <a href="library/get-set/getvisitorvalues.md#reference-b8c9e17c170c4291829a792df46ce279" format="dita" scope="local"> getVisitorValues </a> </li> 
      <li id="li_9E512C6DD15C46C3ABD06ACD60D97E4A"> <a href="faq-intro/faq-intro.md" format="dita" scope="local"> Vanliga frågor </a> </li> 
      <li id="li_B28082F3D075413D89E5AFB718657E17"> <a href="library/function-vars/coopsafe.md#reference-7fbed36f38a048d1a5883c53d430ddf4" format="dita" scope="local"> isCoopSafe </a> </li> 
      <li id="li_7744A4898EA542B9BF009D2066810050"> <a href="library/function-vars/idsyncontainerid.md#reference-5cfbed2240fa4def90f535f017a36015" format="dita" scope="local"> idSyncContainerID </a> </li> 
     </ul> </p> 
    <draft-comment> 
     <p> <b>Meddelanden:</b> </p> 
     <p> <p>Viktigt:  Stöd för ID-tjänster i Internet Explorer 6, 7 och 8 är föråldrat och kommer att upphöra i en framtida version. </p> </p> 
    </draft-comment> </td> 
   <td colname="col2"> <p> <b>Versionsinformation</b> </p> <p><b>Version 4.4</b> 17 juli 2019 innehåller stöd för <a href="reference/hashing-support.md" format="dita" scope="local"> SHA-256-hash-algoritmen</a> som gör att du kan skicka in kund-ID:n eller e-postadresser och skicka ut hash-kodade ID:n.</p><p><b>Version 4.0</b> 12 februari 2019 innehåller <a href="implementation-guides/opt-in-service/optin-overview.md#concept-f9b5db0d27a245fbadd3e19162319360" format="dita" scope="local"> anmälningstjänsten</a> som används för att identifiera om du kan placera en cookie på en användares enhet eller webbläsare när du besöker webbplatsen. </p> <p> 
     <ul id="ul_4F06F170F214492780C7D25A069F799F"> 
      <li id="li_45A7CD556FE44F4DAB035C736A058F36"> I den senaste versionsinformationen <a href="https://marketing.adobe.com/resources/help/en_US/whatsnew/" format="https" scope="external"> om</a> Experience Cloud finns nya funktioner och korrigeringar. </li> 
      <li id="li_10CC4FBFEFC947CA9AD15F52D9715257">Mer information om äldre versioner finns i den <a href="https://marketing-stage.adobe.com/resources/help/en_US/whatsnew/c_legacy_releases.html" format="html" scope="external"> föregående versionsinformationen</a> . </li> 
     </ul> </p> <p> <b>Experience Cloud-resurser</b> </p> <p> 
     <ul id="ul_E30EC96BDC624B5591F0470D430B7F41"> 
      <li id="li_F3A5CCFAE0F247CEB41A03CA8E03106B"> <a href="http://www.adobe.com/privacy.html" format="http" scope="external"> Adobes sekretesscenter</a> </li> 
      <li id="li_A54C1EB170EA4B8FA6A81B90AB0C39DD"> <a href="http://www.adobe.com/marketing-cloud.html" scope="external" format="http"> Adobe Experience Cloud</a> </li> 
      <li id="li_1938F7044F544481A6CC0F45CC22B80A"> <a href="http://helpx.adobe.com/learning.html?promoid=KAUDK" scope="external" format="http"> Adobe Training and Tutorials</a> </li> 
      <li id="li_C71459E0D1464C05B8B9387C43541F17"> <a href="https://marketing.adobe.com/resources/help/en_US/home/index.html" scope="external" format="https"> Produktdokumentation - startsida</a> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

