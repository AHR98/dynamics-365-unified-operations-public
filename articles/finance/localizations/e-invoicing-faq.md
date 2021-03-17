---
# required metadata

title: Electronic invoicing add-in FAQ
description: This topic provides information about frequently asked questions regarding the Electronic invoicing add-in.
author: gionoder
manager: AnnBe
ms.date: 03/17/2021
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 

# optional metadata

ms.search.form: 
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: kfend
# ms.tgt_pltfrm: 
ms.custom: 97423
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: janeaug
ms.search.validFrom: 2020-07-08
ms.dyn365.ops.version: AX 10.0.17

---

# Electronic invoicing add-in FAQ

[!include [banner](../includes/banner.md)]

This topic provides answers to frequently asked questions about the Electronic invoicing add-in. The Electronic invoicing add-in extends the electronic invoicing capabilities that exist in Dynamics 365 Finance, Dynamics 365 Supply Chain Management, and Dynamics 365 Project Operations. 

## What is important about electronic invoicing and why should it matter to my organization?

Operational complexity and risk continue to intensify as organizations grow globally and expand their footprints across regions. Maintaining compliance and adapting to frequently changing regulations is a growing challenge and is of particular importance when it comes to invoicing. Invoicing has traditionally been expensive and prone to errors as companies rely on paper documents and manually intensive processes.  

Organizations have begun to move away from paper invoices to reduce cost and speed up the end-to-end process. Governments are increasingly turning to electronic invoicing as a key component of tax digitalization. By requiring organizations to digitally submit real-time tax information to tax authorities, governments can minimize tax evasion and manipulation, and reduce fraud. 

The world is shifting to paperless document processing and without implementing electronic invoicing, customers may risk compliance issues, unnecessary costs, and lag behind competitors. 

## Doesn't Finance, Supply Chain Management, and Project Operations already include electronic invoicing functionality? What value does the add-in bring to me as a customer? 

The Electronic invoicing add-in extends the electronic invoicing capabilities that exist in Finance, Supply Chain Management, and Project Operations. The add-in also simplifies adherence to the newest electronic invoicing standards and provides coherent experiences for different geographies in electronic invoice processing and exchange. Electronic invoicing's capabilities unlock an array of benefits including: 

   - Faster and easier adoption to country/region specific requirements.
   - Standardization of e-invoicing solution implementations. 
   - Enhanced e-invoice processing traceability.  
   - Easier maintenance to comply with changing legal requirements and local business practices. 
   - Simplified solution packaging.
   - Scaling capabilities for a large volume of submitted documents that results in faster turnaround.
   - Ability to share your solutions with other companies.

## Does the Electronic invoicing add-in support the on-premises installations of Finance, Supply Chain Management, and Project Operations? 

The current platform doesn't allow the use the on-premises version and there are no plans to support it in the future.

## Does the Electronic invoicing add-in interface with the vendor import automation feature?

No. There are plans for this interface, but there is no planned timeline. When planned, the dates will be announced in the [Release plans](https://docs.microsoft.com/dynamics365/release-plans/).

## How does the Electronic invoicing add-in handle file attachments into the electronic invoice? Is a SharePoint server needed when embedding PDF files into the XML file?

The files attached to the electronic invoice are handled as embedded binary data in an XML element. A SharePoint server isn't needed to embed PDF files, but the attachment must be stored in the Finance, Supply Chain Management, and Project Operations document management system.

## Is the Electronic invoicing add-in available according to the regulations of my country/region?

The Electronic invoicing add-in is a microservice platform that will be globally available.

Microsoft plans to publish the electronic invoice formats and integrations for the countries that are functionally localized by Microsoft. For more information, see [Availability of electronic invoicing features](e-invoicing-configuration-rcs.md#availability-of-electronic-invoicing-features).

If the electronic invoicing format for your country/region isn't listed, the platform aims to support this scenario in the future. You can still benefit from the configuration capabilities the Electronic invoicing add-in has, and configure the electronic invoicing format by yourself, or you can work with a partner/ISV to configure those for your organization.

## Is Dynamics 365 for Regulatory Services a new module like Human Resources or Project Operations that is linked to Finance or Supply Chain Management? Are there extra costs for that?

The Dynamics 365 for Regulatory Services (RCS) is a cloud service for configuring Globalization resources. RCS is free for all Finance, Supply Chain Management, and Project Operations license holders.

For RCS sign-up, go to <https://marketing.configure.global.dynamics.com/>.

For more information, see [Regulatory Configuration Services (RCS) - Globalization features](rcs-globalization-feature.md).

## Do I need to sign up to get the Electronic invoicing add-in, or just turn it on in Feature Management?

If you are have a license for Finance, Supply Chain Management, and Project Operations, see [Get started with Electronic invoicing add-on service administration](e-invoicing-get-started-service-administration.md) to sign up for the Electronic invoicing add-in.

## Does the Electronic invoicing add-in work with Tier 1 virtual machines? What is the minimal required environment?

Integration with Electronic invoicing add-in requires at least a Tier 2 virtual machine to host Finance or Supply Chain Management. For more information about environment planning, see [Environment planning](../../fin-ops-core/fin-ops/imp-lifecycle/environment-planning.md).

## Does the Electronic invoicing add-in have a test mode for testing invoice submission?

This can be achieved by configuration. To test invoice submission, you can connect to Finance or Supply Chain Management from a User Acceptance Test (UAT) environment and submit the test invoices. The Electronic invoicing add-in supports configuring test digital certificates, and in the case of e-invoices requiring digital approval, the setup of a URL from test web services published by the tax authorities.

## Is there any documentation about the out-of-box country-specific Electronic invoicing add-in features?

Yes. For information about the availability of Electronic invoicing add-in features and the formats they support, see [Availability of electronic invoicing features](e-invoicing-configuration-rcs#availability-of-electronic-invoicing-features.md).

> [!NOTE] 
> If you didn't find the answer you are looking for, email your question to the Product Development Team at <D365EInvoicePreview@microsoft.com>. We will either contact you or improve the coverage of this FAQ.
