---
# required metadata

title: Enable quality and nonconformance management
description: This topic provides an overview of how to set up and configure quality and nonconformance management features in Dynamics 365 Supply Chain Management.
author: perlynne
manager: tfehr
ms.date: 03/23/2021
ms.topic: article
ms.prod:
ms.technology:

# optional metadata

ms.search.form: InventTestAssociationTable, InventTestGroup, InventTestItemQualityGroup, InventTestTable, InventTestVariable, InventTestVariableOutcome
# ROBOTS:
audience: Application User
# ms.devlang:
ms.reviewer: kamaybac
# ms.tgt_pltfrm:
ms.custom: 94003
ms.assetid: a1d9417b-268f-4334-8ab6-8499d6c3acf0
ms.search.region: Global
ms.search.industry: Distribution
ms.author: perlynne
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0

---

# Enable quality and nonconformance management

[!include [banner](../includes/banner.md)]

This topic provides an overview of how to set up and configure quality and nonconformance management features in Dynamics 365 Supply Chain Management.

## <a name="enable-qm"></a>Enable quality and nonconformance management

Do the following to enable quality management on your system:

1. Go to **Inventory management > Setup > Inventory and warehouse management parameters**.
1. Select the **Quality management** tab.
1. Set the **Use quality management option** to *Yes*.
1. In the **Hourly rate** field, enter an hourly labor rate in the local currency. The hourly rate is used to calculate costs for operations that are related to a nonconformance. The hourly rate and calculated costs provide reference information for a nonconformance. They don't interact with other functionality.
1. Select **Report setup**. Add new lines here for the various report types, and select the type of document to be used for each report.  
1. Close the page.
1. Close the page.

## Quality management configuration process

To start using the quality management features and generate quality orders, you must configure the system and prerequisites. The following list shows the steps that must be taken to configure quality management.

1. [Enable quality and nonconformance management](#enable-qm)
2. [Configure test instruments](quality-test-instruments.md) (Optional)
3. [Configure tests](quality-tests.md)
4. [Configure test variables and outcomes](quality-test-variables.md)
5. [Configure test groups](quality-test-groups.md)
6. [Configure quality groups and link to products](quality-groups.md) (Optional)
7. [Configure quality associations](quality-associations.md) (Optional)

Once the configuration is complete, you can start creating and processing quality orders. For more information about creating and working with quality orders, see [Quality orders](quality-orders.md).

## Nonconformance management configuration process

To start using the nonconformance management features and generate nonconformances, you must configure the system and pre-requisites. The following list shows the steps that must be taken to configure nonconformance management.

1. [Enable quality and nonconformance management](#enable-qm)
2. [Configure workers responsible for approving nonconformances](quality-responsible-workers.md)
3. [Configure problem types](quality-problem-types.md)
4. [Configure quarantine zones](quality-quarantine-zones.md)
5. [Configure diagnostic types](quality-diagnostic-types.md)
6. [Configure operations](quality-operations.md)
7. [Configure quality charges](quality-charges.md) (Optional)

Once the configuration is complete, you can start creating and processing nonconformances. For more information about creating and working with nonconformances, see [Create and process nonconformances](tasks/create-process-non-conformance.md).


## Additional resources

- [Quality management overview](quality-management-processes.md)
- [Nonconformance management](enable-nonconformance-management.md)
- [Quality management for warehouse processes](quality-management-for-warehouses-processes.md)


[!INCLUDE[footer-include](../../includes/footer-banner.md)]