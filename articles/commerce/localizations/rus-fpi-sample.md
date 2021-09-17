---
# required metadata

title: Fiscal printer integration sample for Russia
description: This topic provides an overview of the fiscal integration sample for Russia in Microsoft Dynamics 365 Commerce.
author: EvgenyPopovMBS
manager: annbe
ms.date: 09/21/2021
ms.topic: article
ms.prod: 
ms.technology: 

# optional metadata

ms.search.form: RetailFunctionalityProfile, RetailFormLayout, RetailParameters
audience: Application User
# ms.devlang: 
ms.reviewer: v-chgri
# ms.tgt_pltfrm: 
# ms.custom: 
ms.search.region: Russia
ms.search.industry: Retail
ms.author: epopov
ms.search.validFrom: 2021-8-2
ms.dyn365.ops.version: 10.0.21

---
# Fiscal printer integration sample for Russia

[!include [banner](../includes/banner.md)]

This topic provides an overview of the fiscal integration sample for Russia in Microsoft Dynamics 365 Commerce.

The Dynamics 365 Commerce functionality for Russia includes a sample integration of the point of sale (POS) with a fiscal printer. The sample extends the [fiscal integration functionality](fiscal-integration-for-retail-channel.md) and supports the application programming interface (API) of fiscal printers from [ATOL](http://integration.atol.ru/). The sample enables communication with a fiscal printer that is connected via a communication (COM) port by using a native software driver. The sample is provided in the form of source code and is part of the Retail software development kit (SDK).

Microsoft doesn't release any hardware, software, or documentation from ATOL. For information about how to obatin and operate the fiscal printer, contact [ATOL](https://www.atol.ru/).

> [!NOTE]
> This sample code is intended to be used with certain cash register software from ATOL, a third party. You are responsible for your use of ATOL services, and any use is subject to a separate [end user agreement](http://integration.atol.ru/eula/) between you and ATOL. You understand that the data handling, compliance and security standards of ATOL may
not be the same as Microsoft Dynamics 365 Commerce. Your privacy is important to us. To learn more, read our [Privacy statement](https://go.microsoft.com/fwlink/?LinkId=521839).

For more information on Commerce features available to customers in Russia, see [Commerce localization for Russia](rus-commerce-localization.md).

## Scenarios

The following scenarios are covered by the fiscal printer integration sample for Russia:

### Sales scenarios

- Print a fiscal receipt for cash-and-carry sales and returns.
- Capture a response from the fiscal printer and store it in the channel database.
- Taxes:
    - Map tax rates to the fiscal printer's tax types.
    - Transfer mapped tax data to the fiscal printer.
- Payments:
    - Map the store's payment methods to the fiscal printer's payment types.
    - Print payments on a fiscal receipt.
    - Print change information.
- Print line discount information.
- Send the customer information that is specified for a sales transaction with a fiscal receipt. An example of this information is the customer's email address. For more information, see [Customer information management for Russia](rus-customer-information.md).

### Daily reports

- Fiscal X and fiscal Z reports.

### Error handling

- Retry fiscal registration if possible for situations where the fiscal printer isn't connected, isn't ready, or isn't responding, the printer is out of paper, or there is a paper jam.
- Postpone fiscal registration.
- Skip fiscal registration, or mark the transaction as registered, and include info codes to capture the reason for the failure and additional information.
- Check the availability of the fiscal printer before a new sales transaction is opened or a sales transaction is finalized.

## Limitations of the sample

- The fiscal printer only supports scenarios where sales tax is included in the price. Therefore, the **Price include sales tax** option must be set to **Yes** for both stores and customers.
- Printing of fiscal receipts for customer order operations (for example deposit, pick up, or ship) is not currently supported. Support of customer order operations may be added in later versions.
- Printing of fiscal receipts for petty cash operations (for example tender declaration, float entry, or tender removal) is not currently supported. Support of petty cash operations may be added in later versions.
- Daily reports (fiscal X and fiscal Z) are printed by using the fiscal printer's embedded format.
- The fiscal printer doesn't support mixed transactions. The **Prohibit mixing sales and returns in one receipt** option should be set to **Yes** in POS functionality profiles.

## Default data mapping

The following default data mapping is included in the fiscal document provider configuration that is provided as part of the fiscal integration sample.

- Payment method mapping:
	```json
	{
		"PaymentMethods": [
			{"StorePaymentMethod":"1", "AtolPaymentType":0},
			{"StorePaymentMethod":"2", "AtolPaymentType":4},
			{"StorePaymentMethod":"3", "AtolPaymentType":1},
			{"StorePaymentMethod":"4", "AtolPaymentType":3},
			{"StorePaymentMethod":"5", "AtolPaymentType":0},
			{"StorePaymentMethod":"6", "AtolPaymentType":0},
			{"StorePaymentMethod":"7", "AtolPaymentType":4},
			{"StorePaymentMethod":"8", "AtolPaymentType":4},
			{"StorePaymentMethod":"10", "AtolPaymentType":4},
			{"StorePaymentMethod":"11", "AtolPaymentType":4}
		]
	}    
	```

	The default payment method mapping is based on the store payment method configuration in demo data. You may need to modify the mapping in the connector functional profile according to the settings of payment methods for your stores. For more information on payment types supported by ATOL fiscal printers, see the [ATOL integration documentation](http://integration.atol.ru/) .

## Set up fiscal integration for Russia

For more information on general Commerce settings for Russia, see [Set up Commerce localization for Russia](rus-commerce-setup.md).

To set up fiscal integration for Russia, complete the fiscal registration setup steps that are described in [Set up the fiscal integration for Commerce channels](./setting-up-fiscal-integration-for-retail-channel.md):

1. [Set up a fiscal registration process](./setting-up-fiscal-integration-for-retail-channel.md#set-up-a-fiscal-registration-process). Be sure to note the settings of the fiscal registration process that are [specific to Russia](#configure-the-fiscal-registration-process).
1. [Set error handling settings](./setting-up-fiscal-integration-for-retail-channel.md#set-error-handling-settings).
1. [Set up fiscal X/Z reports from the POS](setting-up-fiscal-integration-for-retail-channel.md#set-up-fiscal-xz-reports-from-the-pos).
1. [Enable manual execution of postponed fiscal registration](./setting-up-fiscal-integration-for-retail-channel.md#enable-manual-execution-of-postponed-fiscal-registration).
1. [Set up the functionality for management of customer information in POS](rus-customer-information.md#setup)
1. [Configure channel components](#configure-channel-components).

### Configure the fiscal registration process

To enable the fiscal registration process for Russia in Commerce headquarters, follow these steps.

1. Download configuration files for the fiscal document provider and the fiscal connector from the Commerce SDK:
    1. Open the [Dynamics 365 Commerce Solutions](https://github.com/microsoft/Dynamics365Commerce.Solutions/) repository.
    1. Open the last available release branch (for example, **[release/9.31](https://github.com/microsoft/Dynamics365Commerce.Solutions/tree/release/9.31)**).
    1. Open **src \> FiscalIntegration \> AtolFiscalPrinterSample**.
    1. Download the fiscal connector configuration file at **HardwareStation \> Connector.AtolSample \> ConfigurationTemplate \> ConnectorAtolSample.xml** (for example, [the file for release/9.31](https://github.com/microsoft/Dynamics365Commerce.Solutions/blob/release/9.31/src/FiscalIntegration/AtolFiscalPrinterSample/HardwareStation/Connector.AtolSample/ConfigurationTemplate/ConnectorAtolSample.xml)).
    1. Download the fiscal document provider configuration file at **CommerceRuntime \> DocumentProvider.AtolSample \> ConfigurationTemplate \> DocumentProviderAtolSample.xml** (for example, [the file for release/9.31](https://github.com/microsoft/Dynamics365Commerce.Solutions/blob/release/9.31/src/FiscalIntegration/AtolFiscalPrinterSample/CommerceRuntime/DocumentProvider.AtolSample/ConfigurationTemplate/DocumentProviderAtolSample.xml)).
1. Go to **Retail and Commerce \> Headquarters setup \> Parameters \> Shared parameters**. On the **General** tab, set the **Enable fiscal integration** option to **Yes**.
1. Go to **Retail and Commerce \> Channel setup \> Fiscal integration \> Fiscal connectors**, and load the fiscal connector configuration file that you downloaded earlier.
1. Go to **Retail and Commerce \> Channel setup \> Fiscal integration \> Fiscal document providers**, and load the fiscal document provider configuration file that you downloaded earlier.
1. Go to **Retail and Commerce \> Channel setup \> Fiscal integration \> Connector functional profiles**. Create a new connector functional profile, and select the document provider and the connector that you loaded earlier. Update the data mapping settings as required.
1. Go to **Retail and Commerce \> Channel setup \> Fiscal integration \> Connector technical profiles**. Create a new connector technical profile, and select the connector that you loaded earlier. Set the connector type to **Internal**. Update the other connection settings as required.
1. Go to **Retail and Commerce \> Channel setup \> Fiscal integration \> Fiscal connector groups**, and create a new fiscal connector group for the connector functional profile that you created earlier.
1. Go to **Retail and Commerce \> Channel setup \> Fiscal integration \> Fiscal registration processes**. Create a new fiscal registration process, create a fiscal registration process step, and select the fiscal connector group that you created earlier.
1. Go to **Retail and Commerce \> Channel setup \> POS setup \> POS profiles \> Functionality profiles**. Open the functionality profile that is linked to the store where the registration process should be activated. On the **Fiscal registration process** FastTab, select the registration process that was created earlier.
1. Go to **Retail and Commerce \> Channel setup \> POS setup \> POS profiles \> Hardware profiles**. Open the hardware profile that is linked to the Commerce Hardware Station that the fiscal printer will be connected to. On the **Fiscal peripherals** FastTab, select the connector technical profile.
1. Go to **Retail and Commerce \> Retail and Commerce IT \> Distribution schedule**. Open the distribution schedule, and select jobs **1070** and **1090** to transfer data to the channel database.

### Configure channel components

The fiscal printer integration sample for Russia is part of the Retail SDK. The sample is located in the **src \> FiscalIntegration \> AtolFiscalPrinterSample** folder of the [Dynamics 365 Commerce Solutions](https://github.com/microsoft/Dynamics365Commerce.Solutions/) repository (for example, [the sample in release/9.31](https://github.com/microsoft/Dynamics365Commerce.Solutions/tree/release/9.31/src/FiscalIntegration/AtolFiscalPrinterSample)). The sample [consists](fiscal-integration-for-retail-channel.md#fiscal-registration-process-and-fiscal-integration-samples-for-fiscal-devices) of a fiscal document provider, which is an extension of Commerce Runtime (CRT), and a fiscal connector, which is an extension of Commerce Hardware Station. For more information about how to use the Retail SDK, see [Retail SDK architecture](../dev-itpro/retail-sdk/retail-sdk-overview.md) and [Set up a build pipeline for the independent-packaging SDK](../dev-itpro/build-pipeline.md).

> [!WARNING]
> Due to limitations of the [new independent packaging and extension model](../dev-itpro/build-pipeline.md), it is currently not possible to use it for this fiscal integration sample. You need to use the previous version of the Retail SDK on a developer virtual machine (VM) in Microsoft Dynamics Lifecycle Services (LCS). Next sections describe how to enable the sample using the previous version of the Retail SDK.

#### Copy sample files to Retail SDK

1. For the auxiliary files:
	1. Copy the **repo.props** file from **Dynamics365Commerce.Solutions** to the **RetailSDK\\src\\SampleExtensions** folder.
	1. Copy the **CustomizationPackage.props** file from **Dynamics365Commerce.Solutions\\src\\FiscalIntegration\\AtolFiscalPrinterSample** to the **RetailSDK\\src\\SampleExtensions** folder.
	1. Open the **CustomizationPackage.props** file and replace the following line:
		
		``` xml
		<Import Project="..\..\..\repo.props" />
		``` 
		
		with the following line:
		
		``` xml
		<Import Project="repo.props" />
		``` 
    
1. For the Commerce runtime extension files:
	1. Copy the **DocumentProvider.AtolSample** folder from **Dynamics365Commerce.Solutions\\src\\FiscalIntegration\\AtolFiscalPrinterSample\\CommerceRuntime** to the **RetailSDK\\src\\SampleExtensions\\CommerceRuntime** folder.
1. For the Hardware Station extension files:
	1. Copy the **Connector.AtolSample** folder from **Dynamics365Commerce.Solutions\\src\\FiscalIntegration\\AtolFiscalPrinterSample\\HardwareStation** to the **RetailSDK\\src\\SampleExtensions\\HardwareStation** folder.

#### Include extension projects to solutions

1. For the Commerce runtime solution:
	1. Find the **RetailSDK\\src\\SampleExtensions\\CommerceRuntime\\CommerceRuntimeSamples.sln** solution and open it.
	1. Add the **DocumentProvider.AtolSample.csproj** project located in the **RetailSDK\\src\\SampleExtensions\\CommerceRuntime\\DocumentProvider.AtolSample** folder.
1. For the Hardware Station solution:
	1. Find the **RetailSDK\\src\\SampleExtensions\\HardwareStation\\HardwareStationSamples.sln** and open it.
	1. Add the **Connector.AtolSample.csproj** project located in the **RetailSDK\\src\\SampleExtensions\\HardwareStation\\Connector.AtolSample** folder.

#### Adjust extension projects

1. For the Commerce runtime extension project:
	1. Find the **RetailSDK\\src\\SampleExtensions\\CommerceRuntime\\DocumentProvider.AtolSample\\DocumentProvider.AtolSample.csproj** file and open it as a text file.
	1. Add the following lines to the top of the **Project** section:
		``` xml
		<Import Project="..\..\..\BuildTools\Microsoft.Dynamics.RetailSdk.Build.props" />
		<Import Project="..\..\..\BuildTools\Common.props" />
		<Import Project="..\..\..\BuildTools\Microsoft.Dynamics.RetailSdk.Build.settings" />
		```
	1. Add the following lines to the bottom of the **Project** section:
		``` xml
		<Import Project="..\..\..\BuildTools\Microsoft.Dynamics.RetailSdk.Build.targets" />
		```

1. For the Hardware Station extension project:
	1. Find the **RetailSDK\\src\\SampleExtensions\\HardwareStation\\Connector.AtolSample\\Connector.AtolSample.csproj** file and open it as text file.
	1. Add the following lines to the top of the **Project** section:
		``` xml
		<Import Project="..\..\..\BuildTools\Microsoft.Dynamics.RetailSdk.Build.props" />
		<Import Project="..\..\..\BuildTools\Common.props" />
		<Import Project="..\..\..\BuildTools\Microsoft.Dynamics.RetailSdk.Build.settings" />
		```
	1. Add the following lines to the bottom of the **Project** section:
		``` xml
		<Import Project="..\..\..\BuildTools\Microsoft.Dynamics.RetailSdk.Build.targets" />
		```

#### Build extension projects

1. For the Commerce runtime extension components:
	1. Open the **CommerceRuntimeSamples.sln** solution under **RetailSDK\\src\\SampleExtensions\\CommerceRuntime**.
	1. Find the **DocumentProvider.AtolSample** project, and build it.
	1. Find the **Contoso.CommerceRuntime.DocumentProvider.AtolSample.dll** assembly file in the **DocumentProvider.AtolSample\\bin\\Debug** folder.
	1. Copy the assembly file to the CRT extension folder:
		- **Commerce Scale Unit:**  Copy the assembly to the  **\\bin\\ext**  folder under the Microsoft Internet Information Services (IIS) Commerce Scale Unit site location.
		- **Local CRT on Modern POS:**  Copy the assembly to the  **\\ext**  folder under the local CRT client broker location.
	1. Find the extension configuration file for CRT:
		- **Commerce Scale Unit:**  The file is named  **commerceruntime.ext.config**, and it's in the bin\ext folder under the IIS Commerce Scale Unit site location.
		- **Local CRT on Modern POS:**  The file is named  **CommerceRuntime.MPOSOffline.Ext.config**, and it's under the local CRT client broker location.
	1.  Register the CRT change in the extensions configuration file. Add  **source="assembly" value="Contoso.CommerceRuntime.DocumentProvider.AtolSample"**.
	1.  Restart the Commerce Scale Unit:
		- **Commerce Scale Unit:**  Restart the Commerce Scale Unit site from IIS Manager.
		- **Client broker:** End the **dllhost.exe** process in Task Manager, and then restart Modern POS.

1. For the Hardware Station extension components:
	1. Open the **HardwareStationSamples.sln** solution under **RetailSDK\\src\\SampleExtensions\\HardwareStation**.
	1. Find the **Connector.AtolSample** project, and build it.
	1. Find the **Contoso.HardwareStation.Connector.AtolSample.dll** assembly file in the **Connector.AtolSample\\bin\\Debug** folder.
	1. Copy the assembly file to a deployed Hardware Station machine:
		- **Remote Hardware station:** Copy the files to the **bin** folder under the IIS Hardware Station site location.
		- **Local Hardware station:** Copy the files to the Modern POS client broker location.
	1. Find the extension configuration file for Hardware Station. The file is named  **HardwareStation.Extension.config**:
		- **Remote Hardware station:** The file is located under the IIS Hardware Station site location.
		- **Local Hardware station:** The file is located under the Modern POS client broker location.
	1. Add the following section to the  **composition**  section of the config file.

		```xml
		<add source="assembly" value="Contoso.Commerce.HardwareStation.Extension.EpsonFP90IIIFiscalDeviceSample" />
		```
	
	1.  Restart the Hardware Station service:
		- **Remote Hardware station:** Restart the Hardware Station site from IIS Manager.
		- **Local Hardware station:** End the **dllhost.exe** process in Task Manager, and then restart Modern POS.

#### Install fiscal printer driver

Install the driver of the fiscal printer to the Hardware Station machine. See the manufacturer's documentation for detailed guidelines.

> [!NOTE]
> If you are using a 64-bit driver, set the **Enable 32-bit Applications** parameter to **False** for the Hardware Station application pool in IIS Manager. Otherwise, if you are using a 32-bit driver, set the **Enable 32-bit Applications** parameter to **True**.

#### Production environment

Follow these additional steps to create deployable packages that contain Commerce components, and to apply those packages in a production environment.

1. Make the following changes in the package configuration files under the **RetailSdk\\Assets** folder:

    - In the **commerceruntime.ext.config** and **CommerceRuntime.MPOSOffline.Ext.config** configuration files, add the following lines to the **composition** section.

        ``` xml
        <add source="assembly" value="Contoso.CommerceRuntime.DocumentProvider.AtolSample" />
        ```

    - In the **HardwareStation.Extension.config** configuration file, add the following line to the **composition** section.

        ``` xml
        <add source="assembly" value="Contoso.HardwareStation.Connector.AtolSample" />
        ```

1. Make the following changes in the **BuildTools\\Customization.settings** package customization configuration file:

    - Add the following lines to include the CRT extensions in the deployable packages.

        ``` xml
        <ISV_CommerceRuntime_CustomizableFile Include="$(SdkReferencesPath)\Contoso.CommerceRuntime.DocumentProvider.AtolSample.dll" />
        ```

    - Add the following line to include the Hardware Station extension in the deployable packages.

        ``` xml
        <ISV_HardwareStation_CustomizableFile Include="$(SdkReferencesPath)\Contoso.HardwareStation.Connector.AtolSample.dll" />
        ```

1. Start the MSBuild Command Prompt for Visual Studio utility, and run **msbuild** under the Retail SDK folder to create deployable packages.
1. Apply the packages via Microsoft Dynamics Lifecycle Services (LCS) or manually. For more information, see [Create deployable packages](../dev-itpro/retail-sdk/retail-sdk-packaging.md).

## Additional resources

[Overview of fiscal integration for Commerce channels](fiscal-integration-for-retail-channel.md)

[Commerce localization for Russia](rus-commerce-localization.md)

[Customer information management for Russia](rus-customer-information.md)

[Set up Commerce localization for Russia](rus-commerce-setup.md)

[Set up the fiscal integration for Commerce channels](./setting-up-fiscal-integration-for-retail-channel.md)

[Retail SDK architecture](../dev-itpro/retail-sdk/retail-sdk-overview.md)

[Set up a build pipeline for the independent-packaging SDK](../dev-itpro/build-pipeline.md)

[Create deployable packages](../dev-itpro/retail-sdk/retail-sdk-packaging.md)

