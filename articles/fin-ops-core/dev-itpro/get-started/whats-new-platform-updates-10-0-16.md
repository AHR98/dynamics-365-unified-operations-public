---
# required metadata

title: Platform updates for version 10.0.16 of Finance and Operations apps (February 2021)
description: This topic lists the features that are included in the platform updates for version 10.0.16 of Finance and Operations apps.
author: sericks007
manager: AnnBe
ms.date: 11/13/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: Developer, IT Pro
# ms.devlang: 
ms.reviewer: sericks
ms.search.scope:  Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid:
ms.search.region: Global
# ms.search.industry: 
ms.author: sericks
ms.search.validFrom: 2020-10-31
ms.dyn365.ops.version: 10.0.16

---
# Platform updates for version 10.0.16 of Finance and Operations apps (February 2021)

[!include [banner](../includes/banner.md)]
[!include [banner](../includes/preview-banner.md)]

This topic lists the features that are included in the platform updates for version 10.0.16 of Finance and Operations apps. This version has a build number of 7.0.XXXX and is available on the following schedule:

- **Preview release:** November 2020
- **General availability (self-update):** January 2021
- **Auto-update:** February 2021

## Features included in this release

-  [User session management](../sysadmin/user-session-management.md)<br>- Administrators have the ability to set a maximum session timeout for individual users.  The range of the session can be from 1 hour to 2160 hours.  When this session length expires, the user is required to log-in with his or her credentials.

-  [Renamed 'Session idle timeout' to 'Session inactivity timeout'](../sysadmin/session-idle-timeout.md)(<br>- To differentiate the types of session timeouts between maximum user session and inactivity user session, a change in the name was implemented.

-  [Warning of deprecation of Visual Studio 2015](removed-deprecated-features-platform-updates.md#visual-studio-2015)<br>- Version 10.0.16 is the last version to support Visual Studio 2015.

## Additional resources

### Bug fixes

For information about the bug fixes that are included in this update, sign in to Microsoft Dynamics Lifecycle Services (LCS), and view the [KB article](https://fix.lcs.dynamics.com/Issue/).

### Dynamics 365: 2020 release wave 2 plan

Wondering about upcoming and recently released capabilities in any of our business apps or platform?

Check out the [Dynamics 365: 2020 release wave 2 plan](https://docs.microsoft.com/dynamics365-release-plan/2020wave2/). We've captured all the details, end to end, top to bottom, in a single document that you can use for planning.

### Removed and deprecated platform features

The [Removed or deprecated platform features](removed-deprecated-features-platform-updates.md) topic describes features that have been removed, or that are planned for removal in platform updates of Finance and Operations apps.

- A *removed* feature is no longer available in the product.
- A *deprecated* feature isn't in active development and might be removed in a future update.

A deprecation notice will be added in the [Removed or deprecated platform features](removed-deprecated-features-platform-updates.md) topic 12 months before the removal of any feature from the product.

For breaking changes that affect only compilation time, but that are binary-compatible with sandbox and production environments, the deprecation time will be less than 12 months. Typically, these changes are functional updates that must be made to the compiler.
