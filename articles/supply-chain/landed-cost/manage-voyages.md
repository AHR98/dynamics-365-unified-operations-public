---
# required metadata

title: Manage voyages
description: A voyage typically represents a vessel but, depending on your own practices and procedures, it could be a vendor, a purchase order, or some other item that makes sense for your organization.
author: RichardLuan
manager: tfehr
ms.date: 12/14/2020
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
ms.author: riluan
ms.search.validFrom: 2020-12-14
ms.dyn365.ops.version: Release 10.0.17
---

# Manage voyages

[!include [banner](../includes/banner.md)]

A voyage typically represents a vessel but, depending on your own practices and procedures, it could be a vendor, a purchase order, or some other item that makes sense for your organization.

The **All voyages** page provides voyage details, delivery, costing, and item/purchase-order/transfer-order information. To open the **All voyages** page, go to **Landed cost \> Voyages \> All voyages**. This page shows a list of current voyages and provides Action Pane actions to create, delete, and work with listed voyages. Select any listed voyage to see its details.

> [!NOTE]
> Shipping containers and folios link to a voyage. Purchase lines link to a shipping container or, should shipping containers and folios be switched off, they can be linked directly to a voyage. In addition, costs entered here are apportioned to all attached purchase lines.

## Action Pane commands

The Action Pane of the **Voyages** page provides actions for working with a selected voyage. Except where noted, all actions and tabs are available both for the the list view of the **All voyages** page and for the detailed view of a single selected voyage.

### Actions directly on the Action Pane

The Action Pane includes both tabs, which open to show a collection of related actions, and buttons, each of which executes a single action. The following table describes the buttons that are directly on the Action Pane.

| **Action** | **Description** |
| --- | --- |
| **New** | Creates a new voyage. <!-- KFM: Link to scenario --> |
| **Delete** | Deletes the current voyage. Only voyages that have a **Voyage status** of *Confirmed* can be deleted. Once a voyage leaves port and processes goods in transit, it can no longer be deleted. |
| **Voyage editor** | Opens the **Voyage editor**, where you can add or remove purchase lines for the voyage, create new containers, and modify details regarding the voyage itself. |
| **Voyage costs** | Opens the **Voyage costs** page, where you can view and add voyage costs to all goods within the voyage. When voyage costs are manually added to the voyage, they are automatically added to the costs inquiry screen and apportioned across to each good according to the method specified in the **Voyage costs** page. |

### The Voyage tab of the Action Pane

The following table describes the actions available on the **Voyage** tab of the Action Pane. This tab is only available when you are working with the list view of the **All voyages** page.

| **Action** | **Description** |
| --- | --- |
| **Shipping container** | Opens a page that shows all of the shipping containers associated with the selected voyage. There could be one or many containers. |
| **Folio** | Opens a page that shows all of the folios associated with the selected voyage. There could be one or many folios. |

### The Manage tab of the Action Pane

The following table describes the actions available on the **Manage** tab of the Action Pane.

| **Action** | **Description** |
| --- | --- |
| **Documents received** | Updates the voyage to set **Documents received** to *Yes*. This can lock the item and/or purchase line for further updates. |
| **In transit** | Updates the **Voyage status** to the in-transit status established in the **[Landed cost parameters](landed-cost-parameters.md)**. There is no further logic on this process. A voyage can also be automatically updated to the in-transit status based on settings on the **[Tracking control center](delivery-information-setup.md)**.
| **Ready for costing** | Updates the **Voyage status** to the costed status established in the **[Landed cost parameters](landed-cost-parameters.md)**. A voyage can be costed when all the invoices have been processed (both stock invoices and voyage cost invoices) and the goods have been received. If the estimated costs associated with a voyage have not been costed, an error will occur when attempting to process the costing of a voyage. |
| **Costed** | Cleans up any costing irregularities once an invoice exists for all purchase orders and voyage costs. On selecting this action, the **Voyage update - Costed** dialog box opens, where you can choose whether to post on the standard financial date, or to instead specify a posting date, and then run the action. You can rerun this any number of times, without limit. You can also use the **Voyage update - Costed** dialog box to establish a schedule to run this action as a periodic task (batch job). We recommend using this function regularly by setting it up as a batch job. |
| **Post receipts list** | Posts a receipts list for all purchase order lines within the voyage. If multi-company voyages are used, a new receipts list posting form will open per company and must be processed within each legal entity. |
| **Post product receipt** | Posts a product receipt for all purchase order lines within the voyage. The product receipt process for the purchase order lines associated with a voyage will be used *only* if the goods will *not* be going through the goods-in-transit process. If the goods are to go through the goods-in-transit process, the system will error out when attempting to post the product receipt for a purchase order line. If multi-company voyages are used, a new delivery note posting form will open per company. |
| **Post invoice** | Posts an invoice for all purchase order lines within the voyage. If the goods on the voyage are to go through goods-in-transit processing, the purchase order lines will be invoiced before the receiving process is done. Invoicing the original purchase order will create the goods in transit orders associated with the original purchase order lines, which can then be received by the warehouse. If multi-company shipments are used, a new invoice posting form will open per company. |
| **Ship transfer order** | Posts a transfer order voyage for all transfer order lines within the voyage. Only transfer orders will be available for update when this option is selected. |
| **Receive transfer order** | Posts a transfer order receipt for all transfer order lines within the voyage |
| **Receive goods in transit** | Receives all order lines that are in transit within the voyage. This is one of three available options for receiving goods in transit on a voyage (the others are to use the **Create arrival journal** action described later in the table, or to use the warehouse app). This is the most simple option and will process the goods-in-transit goods out of the goods-in-transit warehouse and into the final destination warehouse. If you would like greater control over the process, use the arrival journal or a mobile device to process the receipt of goods. |
| **Find auto costs** | Finds relevant voyage costs. If these have already been found or updated, the system will show the message "Un-invoiced cost lines exist. Do you want to overwrite them?" This will find any costs that were not associated with the voyage at the time of creation. Voyage costs that are attached to a voyage and invoiced will not be overwritten. |
| **Create arrival journal** | Opens the **Create arrival journal** dialog box, which lets you create an arrival journal that specifies a location. The dialog box provides the following options:<ul><li>**Create from goods in transit** or **Create from transfer order**: The label for this option changes depending on whether you are using the goods-in-transit process. Set this option to *Yes* to open an arrival journal form that lets you process a standard arrival journal for the goods in transit associated with the voyage. If the item has already been received into the final destination warehouse, it will not be added to the arrival journal lines. </li><li>**Initialize quantity**: Initializes the quantity that will be received based on the the quantities of goods specified on the voyage line. If the voyage line has been partially received, this will be the remaining quantity. (We recommend that you enable this option.)</li><li>**Create from order lines**: The value is taken from the order lines.</li></ul><p>This is one of three available options for receiving goods on a voyage (the others are to use the **Receive goods in transit** action described previously in the table, or to use the warehouse app). |
| **Accrue costs** | It is possible to accrue costs where a cost type has a ledger account specified for the debit. This is normally used when the stock is in transit or goods have been received and invoiced. |
| **Aggregate costs** | Moves costs from the shipping container level to the voyage level. For example, you might typically use this in a shared services/shipping scenario where multiple entities are sharing a shipping container/carton space. Assume the voyage has a 40' shipping container and a 20' shipping container, and the apportionment method is by volume. The goods/entities that are sharing or using the space in the 20' shipping container may be being penalized. To fairly distribute the costs, some organizations may want to transfer the costs to the voyage and distribute based on the voyage level apportionment method. |
| **Change journey template** | Opens a dialog box that lets you change the journey template. After you change the template, the voyage voyage costs will be deleted, so you may need to run the **Find auto costs** action (described previously in this table) or to manually add costs once again. |

### The General tab of the Action Pane

The following table describes the actions available on the **General** tab of the Action Pane.

| **Action** | **Description** |
| --- | --- |
| **Receipts list** | Opens a list of product receipts for all purchase order lines within the voyage. If multi-company voyages are used, a new receipts list will open for each company. If no product receipts lists have been processed, this action is grayed out. |
| **Product receipt** | Opens the product receipt record (where used) for the purchase order lines associated with the voyage. This action is greyed out if no product receipts have been posted. The product receipt process won't be used if you are using goods in transit processing. |
| **Item arrival** | Opens the item arrival journal (where used). |
| **Tracking** | Opens the **Inbound tracking** page. From here, you can update the expected arrival date of goods within a shipping container and voyage and subsequently update the expected delivery dates of purchase order lines. |
| **Costs inquiry** | Opens the **Costs inquiry** page, which shows all the costs of a voyage.<p>Select **View** on the Action Pane to adjust the view. You can choose to view any of the levels, plus the item and cost type code.<p>Only those cost type codes that directly relate to inventory transactions will show the **Costs inquiry** page. Removing these will adjust the inquiry form by grouping costs together, which can be useful if are using using sizes and colors.<p>The **Costs inquiry** page only shows cost type codes where the **Debit** is set to *Item*. |
| **Goods in transit orders** | Opens the **Goods in Transit orders** page, displaying the goods in transit records for the selected voyage only. |

## The Lines view

To open the **Lines** view, open a voyage and then select the **Lines** tab at the top-right part of the voyage heading.

### The voyage header FastTab

This FastTab contains basic information that describes the voyage. Many of the settings here are repeated on the **Header** view, as described in the next section.

### The Voyage lines FastTab

The **Voyage lines** FastTab relates to the voyage details and costing information that applies at a voyage level. Here, the shipping containers, folios, and items attached to the voyage are visible and available for review. The price and quantity of the items on the voyage are also visible here. You can view any listed shipping container or folio by selecting the relevant link.

### The Line details FastTab

The **Line details** FastTab provides more information about the line currently selected in the **Voyage lines** FastTab. Note that this FastTab includes details about the **Position** each line occupies in the container, and its **Declared quantity**.

## The Header view

To open the **Header** view, open a voyage and then select the **Header** tab at the top-right part of the voyage heading.

### The General FastTab of the Header view

The following table describes the settings available on the **General** FastTab of the **Header** view of a voyage.

| **Setting** | **Description** |
| --- | --- |
| **Voyage** | Enter the voyage or flight number |
| **Booking reference** | If your shipper or shipping enter provides a reference number (their internal reference) to identify the voyage, enter it here. |
| **Vessel** | The vessel is selected or entered in this field. Even though it is a drop-down field it allows free text within it. If the vessel is not listed in the drop-down and the user must enter free text for the vessel ID, it does not update the main table for future selection. |
| **External voyage ID** | Enter the publicly available ID for the voyage (such as a flight number). |
| **Master air waybill/Bill of lading** | Enter the master air waybill or bill of lading number. You can specify this when shipping by air. |
| **House air waybill/Bill of lading** | Enter the house air waybill or bill of lading to be specified against the shipping container. |
| **Rental** | Select this check box to indicate the container is a rental, which must be returned. |
| **Description** | Enter a description of the voyage to make it easier to recognize. |
| **Voyage status** | Shows the status of the voyage. Values include *Created*, *In transit*, *Documents received*, and *Costed*. This field isn't calculated based on logic and is only updated via the posting action. The *Costed* value means that an invoice for the stock and all voyage costs have been received. Without an invoice, a voyage can't get the status *Costed*. |
| **Purchase order status** | Shows the highest status of that all the purchase orders associated with this voyage have achieved. |
| **Documents received** | Indicates whether your company has received all the documents associated with this voyage. You can change this value by opening the **Manage** tab on the Action Pane and the, from the **Voyage update** group, select **Documents received**. |
| **Shipping company** | Select the shipping company for this voyage, this can be used to determine auto-costs |
| **Name** | Shows the name of the company selected in the **Shipping company**     field. |
| **Measurement** | This allows for a measurement to be specified within auto cost. This is often used by organizations that do not know the individual volume/weight of the goods but they require a more accurate apportionment than amount or quantity. The freight forwarder will supply them with the weight or cubic measurement, which they place at either an item level or purchase order level. It can be automatically updated if the parameter is selected or manually input. |
| **Measurement unit** | The unit of measure tht applies to the number in the **Measurement** field |
| **Number of pallets** | Specify the number of pallets on the voyage line. This is automatically updated if the **Automatically update number of cartons** parameter is set to *Yes* on the **General** tab of the **Landed cost parameters** page. |

### The Delivery FastTab of the Header view

The following table describes the settings available on the **Delivery** FastTab of the **Header** view of a voyage.

| **Setting** | **Description** |
| --- | --- |
| **Created date and time** | The date and time that the voyage record was created. |
| **Ex-factory date** | This date selects the earliest ex-factory date from the purchase orders that are linked to the voyage. The **Ex-factory date** field is available from the purchase order header and is updated using the tracking control feature. |
| **Ship date** | The estimated date that the plane or vessel leaves the point of origin. |
| **Departure date** | The departure date is usually the date the plane or vessel actually leaves the overseas port. The **Ship date** and **Departure date** do not have to be the same. This date is informational only and is not used to estimate the expected delivery date. The tracking control feature is used to estimate the expected delivery date and this field can be set up to be populated automatically by the tracking control feature. |
| **In to store date** | This date selects the earliest date that the goods from the purchase orders that are linked to the voyage will be available for sale. |
| **Estimated delivery date** | This is usually the date that the goods are due to arrive in the warehouse. This date is informational only and is not used in master planning for goods. The expected delivery date on the purchase order line is used for master planning for goods on a voyage and is updated using the tracking control feature. This field can be set up to be populated by the tracking control feature. |
| **Actual delivery date** | The earliest delivery date based on the goods that are linked to the voyage. |
| **ETA at shipping port** | Enter the date that you expect the voyage will arrive at the shipping port (as provided by your shipping agent). |
| **Original documents received** | Enter the date original documents were received. |
| **Broker advised** | Enter the date broker was advised. |
| **Original bill of lading sent** | Enter the date that the original bill of lading was sent. |
| **Goods released** | Enter the date goods were released from customs. |
| **Customer appointment** | Enter the customer appointment date, which is the date that you expect your customer to take ownership of the goods. |
| **Delivered at warehouse** | Enter the date goods were delivered to the warehouse. |
| **Verification date** | Enter the verification date. |
| **Delivery instructions** | Enter the date that the delivery instructions were received. |
| **Mode of delivery** | This field serves two purposes. It provides information regarding the method by which the voyage is delivered and the cost selection of auto costs associated with that delivery method. |
| **From port** | The shipping port the voyage departs from. |
| **To port** | The shipping port the voyage arrives at. It is possible for the shipping containers to have different ports because the ship may stop at multiple ports. By verifying the **To port** at the shipping container level, it will provide an accurate port detail for each shipping container on a voyage. The auto cost associated with the freight is determined based on the combination of the shipping container type, the **To port** and the **From port**. |
| **Local forwarder** | This is for informational purposes. The local forwarder should be selectable from the vendor table. |
| **Local transport date** | Stores the date the local transport is booked for. This can assist the warehouse in their planning. |
| **Local transport time** | Stores the time slot the local transport is booked for. This can assist the warehouse in their planning. |
| **Journey template** | The journey template specified for the voyage. The journey template is used to populate the to and from port of the shipping container and voyage, which then assists with identifying the auto costs associated with the voyage. |

### The Other FastTab of the Header view

The following table describes the settings available on the **Other** FastTab of the **Header** view of a voyage.

| **Setting** | **Description** |
| --- | --- |
| **Remarks** | Enter additional information relating to the voyage. |
| **Valuation date** | Select the earliest ex-factory date for the purchase orders that are linked to the voyage. |
| **Pending voyage** | <!-- KFM: Description needed --> |
| **Renaming shipping containers** | For voyages with more than one container, this shows how many containers have yet to be received. |

## Voyage update periodic tasks

The Landed cost module includes several voyage-related periodic tasks that can bulk update any of several different aspects of voyages. You can run or schedule them by expanding **Landed cost > Periodic tasks > Voyage updates** in the side navigator and then selecting the type of task. The tasks are:

- **Documents received** - Lets you set the documents received status to several voyages at the same time. Use the **Filter** settings to define the set of voyages you want to update.
- **In transit** - Lets you set the in-transit status to several voyages at the same time. Use the **Filter** settings to define the set of voyages you want to update.
- **Ready for costing** - Lets you update all voyages that are ready to be costed, but have not yet been so. You would typically set this task to run on a regular schedule.
- **Costed**  - Lets you sets all qualifying voyages to the costed status, provided they have been costed and not yet updated on the voyage. You would typically set this task to run on a regular schedule.

