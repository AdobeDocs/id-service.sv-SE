---
description: Innan du distribuerar Experience Cloud Identity Service bör du förstå hur den här tjänsten påverkar besöksspårning på flera domäner och eventuella problem om du samlar in data med olika metoder eller via JavaScript-filer.
keywords: ID-tjänst
seo-description: Innan du distribuerar Experience Cloud Identity Service bör du förstå hur den här tjänsten påverkar besöksspårning på flera domäner och eventuella problem om du samlar in data med olika metoder eller via JavaScript-filer.
seo-title: Beslutspunkter för migrering av identitetstjänst från Experience Cloud
title: Beslutspunkter för migrering av identitetstjänst från Experience Cloud
uuid: ee56b5de-fcf3-4cfb-9e53-762af7c4d2ff
translation-type: tm+mt
source-git-commit: a76eb7cc579ca859769e6caa256a3a0a3f66ca33
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Beslutspunkter för migrering av identitetstjänst från Experience Cloud

Innan du distribuerar Experience Cloud Identity Service bör du förstå hur den här tjänsten påverkar besöksspårning på flera domäner och eventuella problem om du samlar in data med olika metoder eller via JavaScript-filer.

Svar på frågorna i det här avsnittet hjälper dig att avgöra vilka ytterligare migreringsåtgärder du bör utföra.

## Har du en datainsamling i CNAME?

Många kunder kan migrera från en datainsamling med CNAME som en del av migreringen av ID-tjänsten.

<table id="table_13F7C1E3D64D4F86B0149C9D3B54AADD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Datainsamlingsmetod </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Med CNAME </p> </td> 
   <td colname="col2"> <p>Se nästa fråga för att bestämma om du ska migrera från en datainsamling CNAME. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Utan CNAME </p> </td> 
   <td colname="col2"> <p>Hoppa till <a href="../../reference/analytics-reference/migration-decisions.md#section-34dabde7780e4a339f134c0ca7768961" format="dita" scope="local"> Om du inte har någon datainsamling i CNAME, är datainsamlingsservern *.2o7.net eller *.sc.omtrdc.net?</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Har du flera domäner om du har en datainsamling i CNAME?

Om du har flera domäner som skickar data till *samma rapportserie* rekommenderar vi datainsamling med en CNAME. Detta hjälper er att spåra besökare över domäner. Om du samlar in data på en enda domän finns det ingen fördel med att underhålla en CNAME för datainsamling.

<table id="table_D132BCA243E54657AEC930559343FDD3"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Samlar in data från </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Flera domäner </p> </td> 
   <td colname="col2"> <p>Om du spårar besökare i flera domäner, och du också har en huvudstartwebbplats där kunderna kan identifieras innan de besöker andra domäner, bör du fortsätta använda din datainsamling CNAME. <!--See <a href="../../reference/analytics-reference/cname.md#concept-4df91f8a30ad4ec7a01eb943d579cc9d" format="dita" scope="local"> Data Collection CNAMES and Cross Domain Tracking</a> for a detailed explanation.--> </p> <p>Observera att du måste ange ytterligare två spårningsserverparametrar, <span class="codeph"> visitor.marketingCloudServer</span> och <span class="codeph"> visitor.marketingCloudServerSecure</span>, för att konfigurera en CNAME med ID-tjänsten. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>En enda domän </p> </td> 
   <td colname="col2"> <p>Att arbeta med en enda domän innebär att du kan migrera bort från en datainsamling med CNAME om du inte längre vill hantera den. Du behöver dock inte ändra om CNAME fungerar. </p> <p>Om du tar bort CNAME: </p> 
    <ul id="ul_12CDECEFC7BB41A18895B507CAA42315"> 
     <li id="li_32E2CD3E58454E20A642BADE507AE86E">Kontrollera att den nya spårningsservern är <a href="https://docs.adobe.com/content/help/en/analytics/technotes/rdc/regional-data-collection.html" format="https" scope="external"> RDC-kompatibel</a>. </li> 
     <li id="li_865BB6DAA3594EBBAB688E73C8343762">Gå från CNAME till en RDC-spårningsserver några månader innan du migrerar till Experience Cloud<span class="keyword"> ID-tjänsten </span>. </li> 
     <li id="li_284A015177554C848C8648DC5BBAA365"> <i>Använd </i> inte en  <span class="codeph"> *.2o7.</span> nettracking-server. </li> 
     <li id="li_B1ABF03DC46C42059F61542CDE0FE5A1">Kontakta <a href="https://helpx.adobe.com/marketing-cloud/contact-support.html" format="https" scope="external"> kundtjänst</a> för att konfigurera en migrering av besökare. Detta bidrar till att säkerställa ett konsekvent antal besökare. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Har du flera Analytics JavaScript-filer, eller spårar du Flash-program eller -videor?

Om du har flera Analytics JavaScript-filer, Flash-program eller -videor på webbplatsen som skickar data till *samma rapportserie*, bör du konfigurera en respitperiod så att besökarna identifieras av ett Analytics-ID när du distribuerar ID-tjänsten [!DNL Experience Cloud].

<table id="table_8A4EA063AF4345B69BC98537E2E702BA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Datainsamling med </th> 
   <th colname="col2" class="entry"> Nödvändiga åtgärder </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 
    <ul id="ul_910DD99E074E49C6907F86426EFA5BF2"> 
     <li id="li_4366CC8EB7A54A959568E3761ABBBF23">JavaScript-filer med flera analyser </li> 
     <li id="li_B8A8132019EA48088E4F37E36F153D76">Andra datainsamlingsmetoder </li> 
    </ul> </td> 
   <td colname="col2"> <p>Du bör konfigurera en respitperiod för besökar-ID så att du kan skicka besökar-ID-tjänsten till alla JavaScript-filer och andra datainsamlingsbibliotek. Se <a href="../../reference/analytics-reference/grace-period.md" format="dita" scope="local"> ID-tjänstens giltighetsperiod</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>En enda Analytics JavaScript-fil </p> </td> 
   <td colname="col2"> <p>Du kan uppdatera din enda JavaScript-fil så att besökar-ID-tjänsten används utan någon respitperiod. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Använder du datainsamlingsmetoder som inte stöds?

Du kan behöva uppdatera ditt sätt att spåra länkar eller migrera bort från Sliverlight.

<table id="table_A72AEB92F48345DD83F136B9989F4EF9"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Datainsamlingsmetod </th> 
   <th colname="col2" class="entry"> Nödvändiga åtgärder </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>JavaScript och/eller Flash </p> </td> 
   <td colname="col2"> <p>Ingen. ID-tjänsten <span class="keyword"> Experience Cloud</span> stöder dessa datainsamlingsmetoder. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Silverlight </p> </td> 
   <td colname="col2"> <p>Du måste migrera bort från Silverlight om besökarna kan få åtkomst till Silverlight-innehåll och andra avsnitt på webbplatsen som använder ID-tjänsten <span class="keyword"> Experience Cloud</span>. Silverlight stöds inte av ID-tjänsten. </p> <p> Om du spårar en Silverlight-baserad videospelare tillhandahåller leverantören förmodligen JavaScript-API:er som du kan använda i stället. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Hårdkodade bildtaggar </p> </td> 
   <td colname="col2"> <p>Uppdatera hårdkodade länkar för att använda JavaScript. </p> </td> 
  </tr> 
 </tbody> 
</table>

