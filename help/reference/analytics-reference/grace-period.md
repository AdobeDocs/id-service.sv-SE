---
description: Om du har flera JavaScript-filer som skickar data till samma rapportsvit, eller om du använder andra tekniker på webbplatsen, till exempel Flash-videomätning, rekommenderar vi att du konfigurerar en respitperiod.
keywords: ID Service
seo-description: Om du har flera JavaScript-filer som skickar data till samma rapportsvit, eller om du använder andra tekniker på webbplatsen, till exempel Flash-videomätning, rekommenderar vi att du konfigurerar en respitperiod.
seo-title: Giltighetsperioden för ID-tjänsten
title: Giltighetsperioden för ID-tjänsten
uuid: 10a7db7d-de32-4379-914f-edaf929efa32
translation-type: tm+mt
source-git-commit: bc5c81455023e22e64877bb861dfe141e158599c

---


# Giltighetsperioden för ID-tjänsten {#the-id-service-grace-period}

Om du har flera JavaScript-filer som skickar data till samma rapportsvit, eller om du använder andra tekniker på webbplatsen, till exempel Flash-videomätning, rekommenderar vi att du konfigurerar en respitperiod.

När du har distribuerat [!DNL Experience Cloud] ID-tjänsten får nya besökare inte längre något besökar-ID för Analytics från din datainsamlingsserver. Om delar av din webbplats ännu inte har implementerat [!DNL Experience Cloud] ID-tjänsten identifieras inte Experience Cloud ID:t när besökare bläddrar till de här avsnitten och besökarna tilldelas ett äldre besökar-ID för Analytics. Detta kan skapa dubblerade besöksantal och felaktig attribuering.

Om supportavsnittet på webbplatsen till exempel hanteras i ett separat CMS-system kan du ha en annan Analytics JavaScript-fil för det här avsnittet. Om du distribuerar besökar-ID:t på huvudwebbplatsen innan du distribuerar besökar-ID:t till supportwebbplatsen får nya besökare ett äldre Analytics-ID när de besöker supportavsnittet, och besök som sträcker sig över båda webbplatsavsnitten rapporteras som olika besök.

Distribuering av [!DNL Experience Cloud] ID-tjänsten på webbplatser som använder flera JavaScript-filer eller andra tekniker (till exempel Flash) kan orsaka samordningsproblem eftersom du samtidigt måste aktivera ID-tjänsten på alla delar av platsen. Genom att konfigurera en respitperiod kan nya besökare fortsätta att ta emot ett besökar-ID för Analytics från [!DNL Experience Cloud] ID-tjänsten, så att besökare kan identifieras konsekvent på avsnitt på webbplatsen som inte har uppgraderats för att använda ID-tjänsten.

>[!NOTE]
>
>Stöd för respitperiod kräver version 1.3 eller senare av [!DNL Experience Cloud] ID-tjänsten.

## Behöver jag en frist? {#section-fd34c7ff697348a39f49258b7d39eb42}

Om du har en enda Analytics JavaScript-fil och inte använder några andra AppMeasurement-bibliotek behöver du ingen respitperiod. Du kan göra uppdateringen i den enskilda JavaScript-filen så identifieras nya besökare konsekvent med hjälp av marknadsföringsmolnet-ID:t under besöket.

Om du har flera JavaScript-filer som skickar data till *samma rapportserie*, eller om du använder andra tekniker på webbplatsen, till exempel Flash-videomätning, rekommenderar vi att du konfigurerar en respitperiod.

## Hur kan jag aktivera en respitperiod? {#section-512d5cd8570e483cbdd8b04457a16ced}

Kontakta [kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html).
