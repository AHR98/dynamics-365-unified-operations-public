---
# required metadata

title: Site selector module
description: This topic covers the site selector module and describes how to add it to site pages in Microsoft Dynamics 365 Commerce.
author:  anupamar-ms
manager: annbe
ms.date: 09/01/2020
ms.topic: article
ms.prod:
ms.service: dynamics-365-commerce
ms.technology:

# optional metadata
# ms.search.form:
# ROBOTS:
audience: Application User
# ms.devlang:
ms.reviewer: v-chgri
ms.search.scope: Retail, Core, Operations
# ms.tgt\_pltfrm:
ms.custom:
ms.assetid:
ms.search.region: Global
ms.search.industry:
ms.author: anupamar
ms.search.validFrom: 2020-02-10
ms.dyn365.ops.version: Release 10.0.13

---

# Site selector module

[!include [banner](includes/banner.md)]

This topic covers the site selector module and describes how to add it to site pages in Microsoft Dynamics 365 Commerce.

## Overview

When a business has different sites across markets, regions, and locales, site users need an easy way to switch between sites and to choose their preferred shopping site. To accomodate this scenario, the site selector module allows a user to browse across multiple sites.

The site selector module must be configured with the list of sites (market or region or locales) that site users can browse. 

> [!NOTE]
> The site selector module is available in the Dynamics 365 Commerce 10.0.14 release.

The following example image shows a site selector module featured on the header of a site page.
![Example of a site selector module on the header of a site page](./media/ecommerce-sitepicker.PNG)

## Site selector module properties

| Property name             | Value                 | Description |
|---------------------------|-----------------------|-------------|
| Heading | Text | The heading for the module. |
| Site options | Name, Image, URL | This property specifies a name, a link to the site home page, and an optional image to be displayed for each site to be included in the module. The image can be a flag or some represention of a market, region, locale.|

## Add a site selector module to a page

The site selector module can be added to the [Header module](author-header-module.md) under the site selector slot. Once added, you can define the module heading and site options. 

## Additional resources

[Module library overview](starter-kit-overview.md)

[Header module](author-header-module.md)

[Breadcrumb module](add-breadcrumb.md)

[Navigation menu module](nav-menu-module.md)
