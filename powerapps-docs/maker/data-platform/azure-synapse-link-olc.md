---
title: "Manage your Azure Synapse Link with Environment Events | MicrosoftDocs"
description: "Learn how to manage your Azure Synapse Link for Dataverse profiles with Environment events."
ms.custom: ""
ms.date: 11/01/2021
ms.reviewer: "Mattp123"
ms.service: powerapps
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "conceptual"
applies_to: 
  - "powerapps"
author: "sama-zaki"
ms.assetid: 
ms.subservice: dataverse-maker
ms.author: "matp"
manager: "kvivek"
search.audienceType: 
  - maker
search.app: 
  - PowerApps
  - D365CE
contributors: ""
---

# Manage your Azure Synapse Link during Environment Life Cycle Events

[!INCLUDE[cc-data-platform-banner](../../includes/cc-data-platform-banner.md)]

Azure Synapse Link for Dataverse provides a continuous pipeline of data from Dataverse to Azure Synapse Analytics and/or Azure Data Lake. Once the link is created it continuously writes all the initial data as well as any incremental data. When you make changes to your Power Platform Environment, this can affect the state of your Azure Synapse Link for Dataverse. This article explains the behavior  of the Azure Synapse Link for Dataverse and possible user action during environment lifecycle events.

> [!NOTE]
> Azure Synapse Link for Microsoft Dataverse was formerly known as Export to data lake. The service was renamed effective May 2021 and will continue to export data to Azure Data Lake as well as Azure Synapse Analytics.

## Environment Lifecycle Events Overview

|Environment Operation |Synapse Link          |Data                  |User Action           |
|----------------------|----------------------|----------------------|----------------------|
|Backup and Restore |Stops syncing |Maintained |Use solutions to transport the link across environments |
|Copy |Source continues syncing |Source is maintained |Use solutions to transport the link across environments |
|Delete |Stops syncing |Maintained |None |
|Edit the Properties |Error |Maintained |Unlink and relink |
|Move |Source stops syncing |Source is maintained |Use solutions to transport the link across environments |
|Recover |Continue syncing |Maintained |None |
|Reset |Removed |Maintained |Delete data before recreating the link |

## Backup and Restore an Environment

Azure Synapse Link for Dataverse profiles are not part of an [environment backup or the subsequent restore](https://docs.microsoft.com/en-us/power-platform/admin/backup-restore-environments). Once an environment is restored, use solutions to [export and import the configuration](./azure-synapse-link-solution.md) to preserve the configuration of the Azure Synapse Link across environments.

## Copy an Environment

Azure Synapse Link for Dataverse profiles are not copied as part of the [copy an environment](https://docs.microsoft.com/en-us/power-platform/admin/copy-environment) process. To preserve the configuration of the Azure Synapse Link across environments, use solutions to [export and import the configuration](./azure-synapse-link-solution.md).

## Delete an Environment

When an [environment is deleted](https://docs.microsoft.com/en-us/power-platform/admin/delete-environment), all Azure Synapse Link profiles are deleted and the data sync is stopped. All data written at the time of deletion is still available in your Azure Synapse Analytics workspace and/or Azure Data Lake.

## Edit the Properties of an Environment

Azure Synapse Link for Dataverse profiles will fail if the Environment Name or URL environment properties are changed. You will need to unlink the Azure Synapse Link, optionally deleting the file system, and create a new link.

## Move an Environment

If an [environment is migrated from one tenant to another](https://docs.microsoft.com/en-us/power-platform/admin/move-environment-tenant), all Azure Synapse Link profiles are deleted and the data sync is stopped. All data written at the time of deletion is still available in your Azure Synapse Analytics workspace and/or Azure Data Lake. To preserve the configuration of the Azure Synapse Link across environments, use solutions to [export and import the configuration](./azure-synapse-link-solution.md).

## Recover an Environment

When [recovering a deleted environment](https://docs.microsoft.com/en-us/power-platform/admin/recover-environment) within the grace period, all Azure Synapse Link for Dataverse will be available and will continue syncing data with no user action as long as the data in your Azure Synapse Analytics workspace and/or Azure Data Lake has not been modified.

## Reset an Environment

If an [environment is reset](https://docs.microsoft.com/en-us/power-platform/admin/reset-environment), all Azure Synapse Link for Dataverse profiles will be removed from the environment. All the corresponding data in Azure Synapse Analytics workspace and/or Azure Data Lake will still be available but will not be synced. The user may need to clean up the data in the Azure Synapse Analytics workspace and/or Azure Data Lake and will need to recreate the Azure Synapse Link for Dataverse.

### See also

[Azure Synapse Link for Dataverse](./export-to-data-lake.md)

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
