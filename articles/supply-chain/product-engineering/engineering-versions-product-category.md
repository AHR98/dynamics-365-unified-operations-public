---
# required metadata

title: Engineering versions and engineering product category
description: The engineering version concept ensures that different states of a product and its data are kept current and clear and can be visualized in the system
author: t-benebo
manager: tfehr
ms.date: 07/31/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form:  [Operations AOT form name to tie this topic to]
audience: Application User
# ms.devlang: 
ms.reviewer: kamaybac
ms.search.scope:  Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: [used by loc for topics migrated from the wiki]
ms.search.region: Global
# ms.search.industry: [leave blank for most, retail, public sector]
ms.author: benebotg
ms.search.validFrom: 2020-07-31
ms.dyn365.ops.version: Release 10.0.13
---

# Engineering versions and engineering product categories

[!include [banner](../includes/banner.md)]

Engineering products evolve during their product lifecycle. There can be many reasons for this. For example, changes might be introduced to: improve product serviceability, change a component because the supplier no longer offers it, response to new insights, or fix mistakes made in the initial design. There are many reasons why such changes should be stored as part of an ongoing product without overriding previous data. For example:

- You want to keep track of the product as it was manufactured and delivered to your customers in previous lifecycle states.
- You need a lead time before approving and applying the changes.
- You want to have a timestamp on each change and be able to deliver previously manufactured products, separately from each other.

*Engineering versions* ensure that the various states of the product and its data are kept current and clear, and can be visualized in the system. This concept lets you maintain consistency, lock down the bill of material for production, eliminate variability, and easily identify changes.

Generally, the *form-fit-function* rule is applied to decide whether a change requires a new product, a new version, or an update to an existing version. Each defines a specific aspect of a part to help engineers match parts to needs. The form-fit-function rule increases design change flexibility by allowing changes to a part with minimal documentation and design cost as long as the fit, form and function of the product are maintained.

- **Fit** refers to the ability of the part or feature to connect to, mate with, or join to another feature or part within an assembly. The "fit" allows the part to meet the required assembly tolerances to be useful.
- **Form** refers to such characteristics as external dimensions, weight, size, and visual appearance of a part or assembly. This is the element that is most affected by an engineer's aesthetic choices, including enclosure, chassis, and control panel, which become the outward "face" of the product.
- **Function** is a criterion that is met when the part performs its stated purpose effectively and reliably. In an electronics product, for example, function can depend on the solid-state components used, the software or firmware, and quite often on the features of the selected enclosure. Poorly placed or sized ports and misleading or missing labeling are two of the most common ways in which an enclosure can fail the function criterion.

## Engineering versions

When you use engineering products, each product will have at least one engineering version. The initial engineer version is created automatically when you create an engineering product. Each engineering version stores the engineering-relevant data that is specific for that version, including:

- The version number and previous version number (if applicable).
- Effective-from and effective-to dates.
- The product version active status, which tells whether the version can be released and used in transactions (see also [Product readiness](product-readiness.md)).
- The engineering organization that created and owns the product (see also [Engineering organization and data ownership rules](engineering-org-data-ownership-rules.md)).
- Related engineering documents. <!-- KFM: what are these? -->
- The engineering attributes (see also [Engineering attributes and engineering attribute search](engineering-attributes-and-search.md)).
- The engineering bill(s) of materials
- The engineering route(s)

You can choose to update this data on an existing version or create a new version using an **engineering change order** (see also [Engineering change management](engineering-change-management.md)). If you create a new version of the product, the system copies all engineering relevant data to then new version, and then you can modify the data for the new version. This lets you can track specific data for each consecutive version. To compare the differences between consecutive engineering versions, inspect the engineering change order, which includes change types that indicate all changes.

<!-- KFM: We should describe how to make an engineering version and what the settings are. -->

## Track versions in transactions

When you use engineering change management, your product master data will always include one or more engineering versions. In your setup of engineering products, you can choose whether or not the engineering version is also part of *logistical transactions* (see [Engineering product category](#product-category) for details). If the logistical impact is relevant, it differs per product and per company. Sometimes, only the latest version of a product are used and when you introduce a new version, the previous version can't be used anymore. In other cases, the version is needed in logistical transactions to overcome the following challenges:

- Logistics <!-- KFM: Logistics what? Department, manager, personnel? --> needs to ship two pieces of a product to a customer. Do you allow or  desire to ship two different versions?
- If it later turns out that a problem occurs specifically related to a change, it may be beneficial to pinpoint exactly which version was shipped with each order.
- Companies typically want to ship old versions first to phase them out of inventory. This can often be managed by determining the effectivity <!-- KFM: What do you mean by "effectivity"? --> of the new version in relation to predictions of when stock of the old version will be depleted, especially with low-volume products. But sometimes this is not possible, or the uncertainty in stock level prediction is considered too high.

The choice of whether or not to make versions visible in inventory depends on factors such as those mentioned, plus company practice and other considerations specific to each company. You can set this option on the *engineering product category*, and this will be applicable for all products created from the engineering product category for all companies the product is released to.

For products set up with logistical impact, the engineering version must be specified on each transaction. The system will propose the *latest active version*, but you can choose a different version among the various active versions available for the company. For products set up without logistical impact, the engineering version isn't specified on the transactions, but the latest active version is used by the system. For example, when creating the *production bill of material* and running *master planning* <!-- KFM: What is this an example of? -->.

<a name="product-category"></a>

## Engineering product category

Set up engineering product categories in the engineering product hierarchy to ensure engineering products will behave as required. Each engineering product category establishes the (default) behavior of the engineering products that are created based on that category. Once you've create an engineering product, you can't change its engineering product category; you are also prevented from changing any of the following:

- Engineering company
- Product type <!-- KFM: Same as engineering product category? -->
- Product subtype
- Product dimension group
- Configuration technology
- Version number rule

Other settings may inherit default values set up on the engineering product category, but those can be changed according to the system rules.

To work with engineering product categories, go to **Project Oaktree > Setup > Engineering product category details**. Then do one of the following:

- To create a new category, select **New** from the Action Pane and then make settings as described in the following subsections.
- To edit an existing category, select it from the list pane, select **Edit** on the Action Pane, and then make settings as described in the following subsections.
- To delete an existing category, select it from the list pane and then select **Delete** on the Action Pane.

### Settings in the header

Make the following settings in the header of an engineering product category:

| Setting | Description |
| --- | --- |
| **Name** | Enter a name for the engineering product category. |
| **Engineering organization** | Select the engineering organization where products of this engineering product category can be created and will be maintained. |

### The Details FastTab

Make the following settings in the **Details** FastTab of an engineering product category:

| Setting | Description |
| --- | --- |
| **Product subtype** | This setting controls whether engineering versions will have impact on logistical transactions. <!-- KFM: Is there more to say here? Seems like there may be more to this other than its affect on logistics. --> Choose one of the following:<ul><li>**Product** - If there is no **Product dimension group** selected, then there is no logistical impact.</li><li>**Product master** - If the selected **Product dimension group** has the version dimension active, there will be logistical impact on each engineering version. If the selected **Product dimension group** doesn't have the version dimension active, there is no logistical impact (each individual variant will have an engineering version, but no impact on transactions). |
| **Product dimension group** | <!-- KFM: We should describe more about what the **Product dimension group** setting does. Seems like there is more to this other than its affect on logistics --> |
| **Product lifecycle state at creation** | Set up the default product lifecycle state at creation of a new engineering product. For more information see [Product lifecycle state and transactions](product-lifecycle-state-transactions.md). |
| **Version number rule** | Select the version number rule that applies to this engineering product category. The rules can be setup as:<ul><li>**Manual** - You choose the version number for each new version.</li><li>**Automatic**: The system sets the version number based on a format that you define. When setting up the format, use # to position a number and any other character to position a constant value. For example, if you defined the format as "V-##", the first version will be 'V-01', the second version 'V-02', and so on.</li><li>**List**: the system takes the next number from a predefined list of custom values defined by you.</li><ul><!-- KFM: We should have a separate topic or section that describes how to create version number rules of all types. Then link there from here. --> |
| **Enforce effectivity** | Choose whether the effectivity dates of engineering versions must be contiguous, or whether to allow gaps and overlaps. This setting affects the way you can use the **Effective from** and **Effective to** settings for each engineering version where this category applies. Choose one of the following:<ul><li>**Yes** - Each version must specify an **Effective from** value, and neither overlaps nor gaps are allowed between versions. The date range for each engineering version connects directly to the previous and next engineering versions (if they exist). In this scenario, the newest version is always used, and older versions aren't used anymore.</li><li>**No** - There are no restrictions on the effectivity date fields for engineering versions, and both overlaps and gaps are allowed. In this scenario, multiple versions can be active at the same time and you can choose to work with any active version.</li></ul><p>This setting also affects  bills of materials and routes connected to a product version. For details, see [Connect bills of materials and routes to engineering versions](#boms-routes).</p> |
| **Use number rule&nbsp;nomenclature** | Set this to **Yes** to enable rules for defining product number using the engineering attributes. Select the **Edit** button to create and/or modify the rules. <!-- KFM: What does it mean to "use the engineering attributes"? What if we set No? We should describe how to use the settings that open when selected Edit. --> |
| **Use name rule&nbsp;nomenclature** | Set this to **Yes** to enable rules for defining the name using the engineering attributes. Select the **Edit** button to create and/or modify the rules. <!-- KFM: Same notes as above. -->  |
| **Use description rule&nbsp;nomenclature** | Set this to **Yes** to enable rules for defining the description using the engineering attributes. Select the **Edit** button to create and/or modify the rules. <!-- KFM: Same notes as above. -->   |

### The Attributes FastTab

Use the grid on the **Attributes** FastTab to set up the engineering attributes that apply to products belonging to this category.

For details about how to create engineering attributes, see [Engineering attributes and engineering attribute search](engineering-attributes-and-search.md).

Use buttons in the **Attributes** FastTab toolbar to add, remove, and arrange attributes in the grid. <!-- KFM: what does "Update existing products" do? What affect does the order have?  --> 

For each row that you add to the grid, make the following settings:

| Setting | Description |
| --- | --- |
| **Name** | Select the attribute to add. |
| **Value** | <!-- KFM: What does this do?  -->  |
| **Mandatory** | <!-- KFM: What does this do?  -->  |
| **Batch attribute** | <!-- KFM: What does this do?  -->  |
| **Inheritance attribute** | <!-- KFM: What does this do?  -->  |

### The Readiness policy FastTab

Use the **Product readiness policy** drop-down list to select the readiness policy that applies to products belonging to this category. For more information, see [Product readiness](product-readiness.md).

### The Release policy FastTab

Use the **Product release policy** drop-down list to select the release policy that applies to products belonging to this category. For more information, see [Release product structure](release-product-structure.md).

<!-- KFM: When I tried to create an engineering product category, I got the error "Your organization does not have an Engineering category hierarchy. Please go to Product Information Management to create an engineering product hierarchy." Maybe we should mention this and explain what to do about it. I was simply blocked and could not continue. -->

<a name="boms-routes"></a>

## Connect bills of materials and routes to engineering versions

The choice you make on the **Enforce effectivity** setting is also important with regards to the connection of bills of materials and routes to each engineering version. You can only activate multiple bills of materials or routes per product provided there is a difference in the following <!-- KFM: All of the following, or any of the following?  -->:

- Product dimension
- Quantity
- Site
- Effectivity dates

Engineering bills of materials and routes are created from the engineering version where they apply, and can be recognized by the **Engineering controlled** check mark<!-- KFM: Where is this check mark? How do I create these from the engineering version? We should maybe give a procedure for this. -->. When working with engineering bills of materials and routes, you won't normally design them using different quantities, nor will you design different bills of material per site. Also, for engineering bills of materials and routes, the effectivity dates are always taken from the engineering version, so an engineering version, its bill of materials, and its route will all have the same effectivity dates.

For products where you are using the *version* product dimension (with logistical impact on the transactions), the version is also added to the bill of material and routes. This helps to differentiate between the bill of materials and routes of consecutive versions, regardless of the **Enforce effectivity** setting.

For products where you aren't using the *version* product dimension  (no logistical impact on the transactions), the version isn't added to bills of materials or routes. This will result in there being no difference between the bills of materials and routes of consecutive versions. In this case, we highly recommend that you set **Enforce effectivity** to *Yes*; this prevents overlap of engineering versions and makes it possible to activate the bill of material and route of a newer version without needing to deactivate them for the previous version first. If you do set **Enforce effectivity** to *Yes* in this case, you will need to manually deactivate bills of materials and routes of older versions before you can activate the latest version.
