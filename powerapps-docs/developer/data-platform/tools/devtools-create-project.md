---
title: "Create a Power Platform Tools project | Microsoft Docs"
description: "Learn how to start a new Visual Studio project for plug-in or custom workflow assembly development using Power Platform Tools."
ms.custom: ""
ms.date: 07/19/2021
ms.reviewer: "pehecke"
ms.service: powerapps
ms.topic: "article"
author: "phecke" # GitHub ID
ms.subservice: dataverse-developer
ms.author: "pehecke" # MSFT alias of Microsoft employees only
manager: "kvivek" # MSFT alias of manager or PM counterpart
search.audienceType: 
  - developer
search.app: 
  - PowerApps
  - D365CE
---

# Create a Power Platform Tools project

Like any Visual Studio solution, you begin by creating a new project. In the new project dialog, enter "Power Platform" in the search box. You will see a list of available Power Platform Tools project C# templates as described below.

If you have not installed the Power Platform Tools extension for Visual Studio, do so now before continuing with the steps in this article. More info [Install Power Platform Tools](devtools-install.md)

## Available project templates

The following table introduces the available Power Platform Tools project templates.

| C# project template | Description |
| --- | --- |
| Power Platform Solution Template | Solution template for creating a Power Platform solution. This template is for a Microsoft Dataverse solution and not a Visual Studio solution. |
| Power Platform Plug-in Library | Project template for creating a Power Platform plug-in class library and assembly (DLL).|
| Power Platform Package | Project template for creating a Power Platform package (CrmPackage). The package is used to deploy the solution and custom code libraries to a Dataverse environment.|
| Power Platform Workflow Activity Library | Project template for creating a Power Platform custom workflow activity class library and assembly (DLL).|
| Customizations Project | Project template for all customizations of a Power Platform (Dataverse) solution. |

## Use the Power Platform solution template

The Power Platform solution template is a good starting point for any new solution. You can add and remove projects to and from the solution. However, you should not remove the CrmPackage project. Doing so will cause deployment of the Power Platform solution to the target environment to fail.

> [!IMPORTANT]
> A Power Platform solution must contain one and only one CrmPackage project. Otherwise, the Dataverse solution deployment will fail.

The plug-in library and workflow library project templates are typically used for more advanced scenarios where you may want to add multiple custom code assemblies to a Power Platform solution or if you are only interested in developing that specific custom code component. Before you can deploy a solution that contains only a project of these types, you must add a CrmPackage project to the Visual Studio solution.

The easy way to create a Power Platform solution with a plug-in and/or workflow activity project is to use the solution template.

1. In the Visual Studio new project dialog, choose **Power Platform Solution Template** and then select **Next**.

1. Enter the requested project information, choose .NET Framework 4.6.2 or 4.7.2, and select **Create**. At this point you should see either a Dataverse login dialog or a dialog to reuse your last connection. Do whatever is appropriate to connect to your Dataverse environment.

1. At the **Configure Microsoft Power Platform Solution** dialog, choose either to use an existing Dataverse solution or to create a new solution. Depending on what you have chosen, you will either be prompted to enter information about the new solution or select the existing solution from a list.

1. Once the target Power Platform solution has been identified or created, you will specify existing items or create new projects using one of the above templates. The dialog will expand to show step #2 where you can choose (only) one of each available project to add to your solution. Choose (check) one or more projects from the list and select **Next**.

1. In step #3 of the dialog, enter names for your chosen projects and select **Done**. Choose names that you will want to see as project names in Visual Studio Solution Explorer.

In **Solution Explorer**, you should now see a solution containing a single **CrmPackage** project and one or more projects based of the project templates that you chose. Each plug-in or custom workflow activity class library will build an assembly. You can add additional classes to each class library as desired.

## Managing projects

The following procedures describe some common operations for your Visual Studio solution.

### Add a new project to a Power Platform solution

To add a new project to a Visual Studio solution, follow these steps.

1. Right-click the solution in **Solution Explorer**, select **Add**, and then choose **New Project**.

1. Select one of the installed Power Platform Tools templates and select **Next**.

1. Fill in any required information and select **Create**. For a plug-in or workflow activity library, be sure to choose .NET Framework 4.6.2 (or 4.7.2).

### Add an existing project to a Power Platform solution

1. Right-click the solution in **Solution Explorer**, select **Add**, and then choose **Existing Project**.

1. Navigate to the .csprog file of the target project, select it, and choose **Open**.

1. In **Solution Explorer**, under the CrmPackage project, right-click **References** and select **Add Reference**.

1. In the **Projects** tab of the **Add Reference** dialog, select the projects from the list and then click **Add** to add them to the list of selected projects and components.

1. Click **OK** to add the projects and close the **Add Reference** dialog box.

### Remove a project from a Power Platform solution

In **Solution Explorer**, right-click the project and select **Remove**. The project will automatically be removed from the CrmPackage references.

### See Also

*Developer Toolkit specific articles*  
[Install Power Platform Tools](devtools-install.md)  
[Create a plug-in using Power Platform Tools](devtools-create-plugin.md)

*General event handler articles*  
[Event framework](../event-framework.md)  
[Use plug-ins to extend business processes](../plug-ins.md)  
[Workflow extensions](../workflow/workflow-extensions.md)

[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
