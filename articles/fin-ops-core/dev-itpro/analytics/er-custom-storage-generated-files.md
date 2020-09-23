---
# required metadata

title: Specify a custom storage location for generated documents
description: This topic explains how to extend the list of storage locations for documents that Electronic reporting (ER) formats generate.
author: NickSelin
manager: AnnBe
ms.date: 07/30/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 

# optional metadata

# ms.search.form: ERFormatDestinationTable, ERParameters
# ROBOTS: 
audience: Application User, Developer, IT Pro
# ms.devlang: 
ms.reviewer: kfend
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: 
# ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: nselin
ms.search.validFrom: 2019-3-31
ms.dyn365.ops.version: 10.0

---

# Delegate the creation of an ER destination to implement a custom destination

[!include[banner](../includes/banner.md)]

The application programming interface (API) of the Electronic reporting (ER) framework lets you extend the list of storage locations for documents that ER formats generate. This topic includes an overview of the main tasks that you must complete to add a custom storage location by delegating the creation of an ER destination to the default destination factory and implementing a custom class with own destination logic.

## Prerequisites

You must deploy a topology that supports continuous build. (For more information, see [Deploy topologies that support continuous build and test automation](https://docs.microsoft.com/dynamics365/unified-operations/dev-itpro/perf-test/continuous-build-test-automation)) You must have access to this topology for one of the following roles:

- Electronic reporting developer
- Electronic reporting functional consultant
- System administrator

You must also have access to the development environment for this topology.

All the tasks can be done in the **USMF** company.

## Import the Fixed asset roll forward ER format configuration

In the current topology, [import](er-download-configurations-global-repo.md) the **Fixed asset roll forward** ER format configuration into this topology to generate documents that you plan to add a custom storage location for.

![Configuration repository page]( ./media/er-custom-storage-generated-files-import-format.png)

## Run the Fixed asset roll forward report

1.  Go to **Fixed assets \> Inquiries and reports \> Transaction reports \> Fixed asset roll forward**.
2.  In the **From date** field, enter 1/1/2017.
3.  In the **To date** field, enter 1/31/2017.
4.  In the **Currency field**, select **Accounting currency**.
5.  In the **Format mapping** field, select **Fixed asset roll forward**.
6.  Select **OK**.

![Runtime dialog page of the Fixed asset roll forward report](./media/er-custom-storage-generated-files-runtime-dialog.png)

Review a generated outbound document in Excel format that is made available for download by using web browser. This is the [default
behavior](electronic-reporting-destinations.md#default-behavior) of an ER format having no configured [destinations](electronic-reporting-destinations.md) and executing in interactive mode.

## Review source code

Review the code of the `generateReportByGER()` method of the `AssetRollForwardService` class. Notice that the `Run()` method is used to call the ER framework and generate the fixed asset roll-forward report.

```xpp
class AssetRollForwardService extends SysOperationServiceBase
{
    public const str ERFormatModelName = 'Fixed assets';
    public const str ERModelDataSourceName = 'model';
    public const str DefaultExportedFileName = 'AssetRollForward';

    /// <summary>
    /// Generates report by general electronic reporting
    /// </summary>
    /// <param name = "_contract">The Asset Period Statement contract</param>
    public void generateReportByGER(AssetRollForwardContract _contract)
    {
        ERFormatMappingId   formatMappingId;
        AssetRollForwardDP  dataProvider;
        AssetRollForwardTmp assetRollForwardTmp;
        Query               query;

        query = new Query(SysOperationHelper::base64Decode(_contract.parmQuery()));
        dataProvider = AssetRollForwardDP::construct();
        formatMappingId = _contract.parmFormatMapping();
        assetRollForwardTmp = dataProvider.getAssetRollForwardTmp(_contract, query);

        if (assetRollForwardTmp)
        {
            try
            {
                ERIModelDefinitionParamsAction parameters = new ERModelDefinitionParamsUIActionComposite()
                    .add(new ERModelDefinitionDatabaseContext().addTemporaryTable(assetRollForwardTmp))
                    .add(new ERModelDefinitionObjectParameterAction(ERModelDataSourceName, 'MyParameters', _contract, true));

                // Call ER to generate the report.
                ERObjectsFactory::createFormatMappingRunByFormatMappingId(formatMappingId, DefaultExportedFileName)
                    .withParameter(parameters)
                    .withFileDestination(_contract.getFileDestination())
                    .run();
            }
            catch
            {
                // An error occurred while exporting data.
                error("@SYP4861341");
            }
        }
        else
        {
            // There is no data available.
            info("@SYS300117");
        }
    }
}
```

## Modify source code

1.  Add a new class to your Microsoft Visual Studio project (`AssetRollForwardDestination` in this example) and write code
    to implement your custom destination for generated fixed asset roll forward reports.
    1.  `new()` method is designed to get the original ER destination object as well as the application logic driven parameter to specify the custom location for storing generated reports. In this example it is the name of a folder of the local file system of the server that runs the Application Object Server (AOS) service.
    2.  `saveFile()` method is designed to save a generated document to a folder of the local file system of the server that runs the Application Object Server (AOS) service.

```xpp
using Microsoft.Dynamics365.LocalizationFramework;

/// <summary>
/// Destination class for <c>AssetRollForwardDestinationFactory</c> that stores a generated report.
/// </summary>
public class AssetRollForwardDestination implements ERIFileDestination
{
    private ERIFileDestination originDestination;
    private str TargetFolder;

    /// <summary>
    /// Creates a stream for new file.
    /// </summary>
    /// <param name = "_fileName">Name of a new file.</param>
    /// <returns>Stream for new file.</returns>
    public System.IO.Stream newFileStream(System.String _fileName)
    {
        return originDestination.newFileStream(_fileName);
    }

    /// <summary>
    /// Saves file in destination.
    /// </summary>
    /// <param name = "_stream">A stream to save.</param>
    /// <param name = "_fileName">A file name.</param>
    /// <returns>Saved stream.</returns>
    public System.IO.Stream saveFile(System.IO.Stream _stream, System.String _fileName)
    {
        _stream.Seek(0, System.IO.SeekOrigin::Begin);
        using (var localStream = System.IO.File::OpenWrite(TargetFolder + _fileName))
        {
            _stream.CopyTo(localStream);
        }
        return _stream;
    }

    /// <summary>
    /// Constructs destination for fixed asset roll forward report.
    /// </summary>
    /// <param name = "_originDestination">The original destination.</param>
    /// <param name = "_TargetFoder">The folder to store a report that's being created.</param>
    /// <returns>The fixed asset roll forward destination.</returns>
    public static AssetRollForwardDestination construct(ERIFileDestination _originDestination, str _TargetFoder)
    {
        return new AssetRollForwardDestination(_originDestination, _TargetFoder);
    }

    protected void new(ERIFileDestination _originDestination, str _TargetFoder)
    {
        originDestination = _originDestination;
        TargetFolder = _TargetFoder;
    }
}
```  

2.  Add a new class to your Microsoft Visual Studio project (`AssetRollForwardDestinationFactory` in this example) and write code to set
    up a custom destination factory to delegate the creation of a destination to the default destination factory and wraps a file destination up with your own destination.

```xpp
using Microsoft.Dynamics365.LocalizationFramework;
using Microsoft.Dynamics365.LocalizationFramework.Format.FileGeneration;

/// <summary>
/// Destination factory for using <c>AssetRollForwardDestinationFactory</c>.
/// </summary>
public class AssetRollForwardDestinationFactory implements ERIFileDestinationFactory, ERIFileDestinationFactoryPostProcessor
{
    private ERIFileDestinationFactory originDestinationFactory;
    private str TargetFolder;

    /// <summary>
    /// Creates file destination for print management.
    /// </summary>
    /// <param name = "_fileDestination">A default file destination.</param>
    /// <param name = "_identification">An identification strategy.</param>
    /// <param name = "_rootContext">A root context.</param>
    /// <param name = "_root">A root element.</param>
    /// <returns>A file destination.</returns>
    public ERIDataDrivenFileDestination createPrintMgmtDestination(
        ERIFileDestination _fileDestination,
        ERIObjectIdentificationStrategy _identification,
        ERTextFormatDataContext _rootContext,
        ERTextFormatIFileComponent _root)
    {
        ERIDataDrivenFileDestination dataDrivenDestination = originDestinationFactory.createPrintMgmtDestination(
            _fileDestination,
            _identification,
            _rootContext,
            _root);

        IFileDestinationHost fileDestinationHost = dataDrivenDestination as IFileDestinationHost;
        if (fileDestinationHost)
        {
            fileDestinationHost.FileDestination = AssetRollForwardDestination::construct(
                fileDestinationHost.get_FileDestination(),
                TargetFolder);
        }

        return dataDrivenDestination;
    }

    /// <summary>
    /// Constructs the fixed asset roll forward destination factory.
    /// </summary>
    /// <param name = "_originDestinationFactory">The original destination.</param>
    /// <param name = "_TargetFolder">The string containing a folder name that corresponds to the report, that's being created.</param>
    /// <returns>The destination factory for the fixed asset roll forward report.</returns>
    public static AssetRollForwardDestinationFactory construct(ERIFileDestinationFactory _originDestinationFactory, str _TargetFolder)
    {
        AssetRollForwardDestinationFactory destinationFactory = new AssetRollForwardDestinationFactory(_originDestinationFactory, _TargetFolder);

        ERIFileDestinationFactoryPostProcessorsHost factoryPostProcessing = ERCast::asObject(destinationFactory.originDestinationFactory) as ERIFileDestinationFactoryPostProcessorsHost;

        if (factoryPostProcessing)
        {
            factoryPostProcessing.addDestinationPostProcessor(destinationFactory);
        }
        return destinationFactory;
    }

    public ERIFileDestination processDestinationAfterCreation(ERIFileDestination _sourceDestination)
    {
        return AssetRollForwardDestination::construct(_sourceDestination, TargetFolder);
    }

    protected void new(ERIFileDestinationFactory _originDestinationFactory, str _TargetFolder)
    {
        originDestinationFactory = _originDestinationFactory;
        TargetFolder = _TargetFolder;
    }
}
```

3.  Modify the existing `AssetRollForwardService` class and write code to set up a custom destination factory for the report runner. Notice that when a custom destination factory is constructed, the application driven parameter (a target folder) is passed to be used for storing generated files.

> [!NOTE] Make sure that the specified folder (**c:\\0** in this example) is present in the local file system of the server that runs the Application Object Server (AOS) service. Otherwise the [DirectoryNotFoundException](https://docs.microsoft.com/en-us/dotnet/api/system.io.directorynotfoundexception?view=netcore-3.1) exceptions will be thrown at runtime.

```xpp
using Microsoft.Dynamics365.LocalizationFramework;
/// <summary>
/// The electronic reporting service class for fixed asset roll forward report
/// </summary>
class AssetRollForwardService extends SysOperationServiceBase
{
    public const str ERFormatModelName = 'Fixed assets';
    public const str ERModelDataSourceName = 'model';
    public const str DefaultExportedFileName = 'AssetRollForward';

    /// <summary>
    /// Generates report by general electronic reporting
    /// </summary>
    /// <param name = "_contract">The Asset Period Statement contract</param>
    public void generateReportByGER(AssetRollForwardContract _contract)
    {
        ERFormatMappingId   formatMappingId;
        AssetRollForwardDP  dataProvider;
        AssetRollForwardTmp assetRollForwardTmp;
        Query               query;

        query = new Query(SysOperationHelper::base64Decode(_contract.parmQuery()));
        dataProvider = AssetRollForwardDP::construct();
        formatMappingId = _contract.parmFormatMapping();
        assetRollForwardTmp = dataProvider.getAssetRollForwardTmp(_contract, query);

        if (assetRollForwardTmp)
        {
            try
            {
                ERIModelDefinitionParamsAction parameters = new ERModelDefinitionParamsUIActionComposite()
                    .add(new ERModelDefinitionDatabaseContext().addTemporaryTable(assetRollForwardTmp))
                    .add(new ERModelDefinitionObjectParameterAction(ERModelDataSourceName, 'MyParameters', _contract, true));

                // Call ER to generate the report.
                ERIFormatMappingRun formatMappingRun = ERObjectsFactory::createFormatMappingRunByFormatMappingId(formatMappingId, DefaultExportedFileName);
                formatMappingRun.withParameter(parameters);
                formatMappingRun.withFileDestination(_contract.getFileDestination());

                ERIFileDestinationFactoryHost factoryHost = ERCast::asObject(formatMappingRun) as ERIFileDestinationFactoryHost;
                if (factoryHost)
                {
                    ERIFileDestinationFactory fileDestinationFactory = factoryHost.getFileDestinationFactory();
                    factoryHost.setFileDestinationFactory(AssetRollForwardDestinationFactory::construct(fileDestinationFactory, @'c:\0\'));
                    formatMappingRun.run();
                }
            }
            catch
            {
                // An error occurred while exporting data.
                error("@SYP4861341");
            }
        }
        else
        {
            // There is no data available.
            info("@SYS300117");
        }
    }
}
```

4.  Rebuild your project.

Run the Fixed asset roll forward report
---------------------------------------

1.  Go to **Fixed assets \> Inquiries and reports \> Transaction reports \> Fixed asset roll forward**.
2.  In the **From date** field, enter 1/1/2017.
3.  In the **To date** field, enter 1/31/2017.
4.  In the **Currency field**, select **Accounting currency**.
5.  In the **Format mapping** field, select **Fixed asset roll forward**.
6.  Select **OK**.
7.  Explore the local **C:\\0** folder to find a generated file.

> [!NOTE]
> Note that since the `originDestination` object is not used in this example in the `AssetRollForwardDestination` object, configures for the ER format [destinations](electronic-reporting-destinations.md) will be ignored at runtime.

## Additional resources

- [Electronic reporting (ER) destinations](electronic-reporting-destinations.md)
- [Extensibility home page](../extensibility/extensibility-home-page.md)
