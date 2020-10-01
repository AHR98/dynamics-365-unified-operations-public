---
# required metadata

title: Cloud and Edge
description: Cloud and Edge scale units for manufacturing and warehouse management workloads
author: cabeln
manager: 
ms.date: 11/03/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

ms.search.form: 
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: kamaybac
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid:
ms.search.region: global
ms.search.industry: SCM
ms.author: cabeln
ms.search.validFrom: 2020-09-23
ms.dyn365.ops.version: AX 10.0.15
---
 
# Cloud and Edge scale units for manufacturing and warehouse management workloads - public preview

This feature enables shop floor and warehouse execution workloads to be distributed between cloud and edge scale units, which can help improve performance, prevent service interruptions, and maximize up time.

Companies working with manufacturing and distribution must be able to execute key business processes 24/7, without interruption and at scale. But complications may arise due to issues ranging from basic connectivity (such as provider outages, Azure outages, unreliable connections, or network latency) to multiple business processes competing for the same system resources. Cloud and edge features enable companies to execute key mission-critical manufacturing and warehouse processes without interruption, even in situations such as these.

### Public preview information

The Cloud & Edge preview for Dynamics 365 Supply Chain Management is made available on the condition you agree to these [Supplemental Terms of Use for Microsoft Dynamics 365 Previews](https://go.microsoft.com/fwlink/?linkid=2105274).

> [!IMPORTANT]
> The preview for cloud and edge scale units will become available for existing customers of Dynamics 365 Supply Chain Management during October.
>
>You must be part of the Early Access Program (aka PEAP) for Finance & Operations to get access to the October preview release build 10.0.15 / PU 39 for deployment in your LCS environment. You can join the PEAP program via a membership in broader  [Dynamics Insider program](https://experience.dynamics.com/insider) and then by selecting the specific program "Finance & Operations: Preview early access program (PEAP).

> [!IMPORTANT]
> In order to sign up to the Cloud & Edge preview for Dynamics 365 Supply Chain Management your organization must already have a live Dynamics 365 Supply Chain Management cloud environment.
> The scale units capability are in public preview at the moment.
As the one signing up, your user account must be user in the specific tenant and also a project owner or an environment admin in LCS for an active Dynamics 365 LCS project in that tenant.
>
> When you  sign up for the preview, you will select the tenant and go through the sign up steps. As soon as a preview capacity can be allocated an email will be sent with provisioning details and the promotion codes for two environments (a cloud hub and a scale unit) for the respective LCS project. You will then be able to deploy the two environment as Tier 2 sandbox environments. Those are valid 60 days from creation date of the promo code.
>After confirmation to Microsoft, the one of the environments will be configured to function as cloud hub the other as a scale unit. You can then configure the scale units and deploy select warehouse management an manufacturing workloads using the [Scale Unit Manager portal](https://SUM.DYNAMICS.COM).
>
>Please note! Preview environments will be deleted automatically after 60 days or if they appear to not be utilized. After the preview environment has been deleted, you may sign up and queue for a new preview deployment.
>
>Navigate to the Scale Unit Manager portal to sign up for the preview [Scale Unit Manager portal](https://SUM.DYNAMICS.COM)

> [!WARNING]
> Please note that certain business functionality is not fully supported in the public preview when using workloads scale units. See more details in the sections that explain the functional workload details.

The preview will allow you receive one environment that will function as a cloud based hub of your supply chain management environment and one environment that will function as a cloud scale unit. For the preview both environment will be hosted in a data center in northern USA.
You will also have the possibility to configure an on-premise environment using LBD and configure this as an edge scale unit for the the cloud hub that you have received as part of the preview program.

## Scale units and dedicated workloads in public preview

:::image type="content" source="./media/cloud_edge-HeroDiagram.png" alt-text="Dynamics 365 with Scale Units":::

Scale units for supply chain management extend your central Dynamics 365 Supply Chain Management cloud hub environment with dedicated processing capacity. Scale units can run in the cloud or on the edge in your local facility premises. Scale units are always connected to the cloud hub environment and receive all information to run the dedicated processing for assigned workloads.

:::image type="content" source="media/cloud_edge-previewoptions.png" alt-text="Scale unit options with public preview ":::

With the public preview we offer participants to experience configurations of a cloud hub environment with selected workloads on a cloud scale unit which can be configured using the Scale Unit Manager portal. Preview participants who have access to a LBD (Local Business Data) on-premises environment can configure such as an edge scale unit.  

The preview features two kinds of workloads of which one of each may be assigned per scale unit. A workload is a defined set of business functionality that can be factored out and delegated to a scale unit. As of today two types of workloads are supported:

- Manufacturing execution
- Warehouse management

### Dedicated manufacturing workload capabilities in a scale unit

Within manufacturing execution, cloud and edge scale units deliver the following capabilities, even when edge units aren't connected to the cloud:

- Enable machine operators and shop floor supervisors to access the operational production plan.
- Enable machine operators to keep the plan current by executing discrete and process manufacturing jobs.
- Enable the shop floor supervisor to adjust the operational plan.
- Enable workers to access time and attendance for clock-in and clock-out on the edge to ensure correct worker pay calculation.

Review the [manufacturing scale unit workload details](cloud_edge-workload-manufacturing.md) for more information.

### Dedicated warehouse management workload capabilities in a scale unit

For warehouse execution, cloud and edge scale units deliver the following capabilities, even when edge units aren't connected to the cloud:

- Enable selected wave methods processing, for sales orders and demand replenishment.
- Enable warehouse workers to execute sales and demand replenishment warehouse work using the warehouse app.
- Enable warehouse workers to perform inquiries into on-hand inventory using the warehouse app.
- Enable warehouse workers to create and execute inventory movements using the warehouse app.
- Enable warehouse worker to register purchase orders and conduct put away using the warehouse app.

Review the [warehouse scale unit workload details](cloud_edge-workload-warehousing.md) for more information.

## Onboarding to using scale units for your Dynamics 365  Supply Chain Management environment

### The deployment of the preview for cloud and edge scale units

The following diagram shows the sign-up and provisioning flow for the public preview of cloud and edge scale units.
:::image type="content" source="media/cloud_edge-previewsignup.png" alt-text="Diagram of the preview sign-up steps":::

### Selecting your LCS project tenant and the detailed preview process

In the public preview the [Scale Unit Manager portal](https://SUM.DYNAMICS.COM) shows the list of Tenants that your account is part of and you are and owner or environment admin in the in a LCS project.
You will also see the sign-up status for each tenant.

:::image type="content" source="media/cloud_edge-Signup1.png" alt-text="Screen shot showing the 'Sign up now' for a tenant.":::

Click on the Sign up now! button in order to submit your LCS tenant to participate in the preview. You need to accept the terms and supply your business email address for further communication in regards to the preview signup process.
:::image type="content" source="media/cloud_edge-Signup2.png" alt-text="Screen shot showing the 'Sign up now' for a tenant.":::  

Microsoft will review your request and inform you about the next steps.  

Once you have been granted access to the preview program you will receive two promo codes for your LCS project. You should now deploy two environments in LCS with these promo codes. The environments should be for the PEAP build 10.0.15. Once completed you should reply in email such that we can commence the final step to enable one of those environments to become the Cloud hub, the other a cloud scale unit in your preview deployment. We will let you know once this step is completed.

At this point you can start configuring scale units and workloads in your preview environment using the scale unit manager portal.

### Managing cloud scale units and workloads
Enter the scale unit manager portal and select the navigation item 

### Creating an edge scale unit for preview using your custom on-premises hardware appliance
  
In the public preview you can create on-premises edge scale units on your custom hardware using the Local Business Data environments.
Please find more details on [on-premises scale units in preview here](cloud_edge-EdgeScaleUnitsUsingLBD.md).
