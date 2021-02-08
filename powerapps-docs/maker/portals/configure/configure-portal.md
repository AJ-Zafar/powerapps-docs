---
title: "Overview of Portal Management app | MicrosoftDocs"
description: "Information about Portal Management app."
author: sandhangitmsft
ms.service: powerapps
ms.topic: conceptual
ms.custom: 
ms.date: 08/07/2020
ms.author: sandhan
ms.reviewer: tapanm
---

# Portal Management app

> [!NOTE]
> Effective November 2020:
> - Common Data Service has been renamed to Microsoft Dataverse. [Learn more](https://aka.ms/PAuAppBlog)
> - Some terminology in Microsoft Dataverse has been updated. For example, *entity* is now *table* and *field* is now *column*. [Learn more](https://go.microsoft.com/fwlink/?linkid=2147247)
>
> Power Apps portals articles will be updated soon to reflect the latest terminology.

The Portal Management app lets you do advanced configuration actions on your portal. The app is available after the database on Microsoft Dataverse is created successfully.

To open the Portal Management app, go to the **Your apps** section on the Power Apps home page, locate the Portal Management app, and select it.

> [!div class=mx-imgBorder]
> ![Portal Management app](../media/portal-mgmt.png "Portal Management app")

The Portal Management app is opened in Unified Interface. You can configure your portal as per your requirement.

> [!div class=mx-imgBorder]
> ![Portal Management app in Unified Interface](../media/portal-mgmt-unified-interface.png "Portal Management app in Unified Interface")

### Browser considerations

If your web browser has any extensions such as ad-blockers, you may see a script error when using the Portal Management app: `One of the scripts for this record has caused an error. For more details, download the log file.` In addition, the downloaded log file may reference this error: `ReferenceError: Web resource method does not exist.` 

![Script error](media/configure-portal/script-error.png "Script error") 

This error occurs for forms such as [Web pages](web-page.md), [Entity Forms](entity-forms.md), [Entity Lists](entity-lists.md), or [Web Form Steps](web-form-steps.md). To resolve this error, disable extensions such as ad-blockers in your browser. You may also use a different browser instead that doesn't have such extensions enabled.
