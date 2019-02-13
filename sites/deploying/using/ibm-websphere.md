---
title: IBM Websphere Commerce
seo-title: IBM Websphere Commerce
description: null
seo-description: Integrating AEM with IBM Websphere Commerce
uuid: e2aa19e2-4e75-4c27-8131-6ffe6c27a055
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: a63c15b6-47e6-4aec-8f52-ee102c1cbcc8
disttype: dist5
gnavtheme: light
isreadyforlocalization: false
pagetitle: Deploying eCommerce with IBM Websphere Commerce
index: y
internal: n
snippet: y
---

# IBM Websphere Commerce{#ibm-websphere-commerce}

Deploying the necessary eCommerce packages will provide the full functionality of the eCommerce framework, together with a reference implementation of eCommerce functionality as provided with a IBM Websphere Commerce implementation (including a demonstration catalog).

This is available under the English (US) branch ( `/content/geometrixx-outdoors/en_US`) of the Geometrixx Outdoors site.

>[!NOTE]
>
>To run the Geometrixx Outdoors store with WebSphere Commerce, [the Geometrixx Outdoors products and catalog data must be loaded into WebSphere Commerce](../../deploying/using/setup.md).

### Technical Requirements {#technical-requirements}

The IBM Websphere extension of the eCommerce Integration Framework has been made to support Websphere Commerce version 7 Feature Pack 8.

>[!NOTE]
>
>You will need Java 7.

### Packages Needed for eCommerce with Websphere Commerce {#packages-needed-for-ecommerce-with-websphere-commerce}

To install eCommerce functionality you need:

* Your Websphere Commerce server.
* AEM eCommerce framework:

    * this is part of a standard AEM installation  
    * CQ Geometrixx Outdoors demo store (needs seperate package, as Geometrixx demos are not part of AEM 6.3 any more)

* AEM Websphere Commerce content packages, available through your [Daycare](http://daycare.day.com/home.html) account: ``

    * `cq-geometrixx-all-pkg-5.10.68  
      `
    * `cq-6.3.0-featurepack-6709`
    * a reference implementation to illustrate use of Websphere Commerce ( `geometrixx-outdoors/en_US`)

### Installation of eCommerce with Websphere Commerce {#installation-of-ecommerce-with-websphere-commerce}

To install AEM with a Websphere Commerce integration configuration (using the demonstration catalog, Geometrixx Outdoors), the basic steps are:

1. [Install AEM](../../deploying/using/deploy.md).
1. Install the demonstration content packages using the [package manager](../../administering/using/package-manager.md):

    1. `cq-geometrixx-all-pkg  
       `
    1. `cq-6.3.0-featurepack-6709`

1. [Author](../../authoring/using/page-authoring.md) any supplementary pages that you need in AEM.

>[!NOTE]
>
>To download the packages, navigate to [Package Share](../../administering/using/package-manager.md#main-pars-title-3).

AEM needs to be configured to connect to the WebSphere Commerce server instance, which is our demo WebSphere Commerce Server running the Geometrixx Outdoors eSite.

1. Navigate to [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Click **Adobe CQ Commerce - IBM WebSphere Commerce REST API client**.
1. Enter the **Websphere Commerce server host / ip **as required.
1. Click **Save**.

>[!CAUTION]
>
>Use of the Websphere Commerce server requires a separate license.
