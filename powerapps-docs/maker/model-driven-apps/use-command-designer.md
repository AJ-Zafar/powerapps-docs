---
title: "Customize the command bar (preview) | MicrosoftDocs"
description: "Use the command designer to customize the command bar."
Keywords: command bar, command designer
author: caburk
ms.author: caburk
ms.reviewer: matp
manager: kvivek
ms.date: 07/26/2021
ms.service: powerapps
ms.topic: conceptual
search.audienceType: 
  - maker
search.app: 
  - PowerApps
  - D365CE
---

# Customize the command bar using command designer

[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

This topic guides you through creating and editing modern commands using the new low-code designer and Power Fx.

  > [!IMPORTANT]
  > - This is a preview feature, and may not be available in all regions.
  > - This is a new infrastructure that stores metadata separately from classic commands. However, classic and modern commands can run side-by-side.
  > - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)]
  
 ### Create a new model-driven app using modern app designer

1. Go to [make.powerapps.com](https://make.powerapps.com/?cds-app-module-designer.isCustomPageEnabled=true)

1. On the left navigation pane, select **Solutions** and then open or create a solution to contain the new model-driven app.

1. Select **New** > **App** > **Model-driven app**

1. Select **Use modern app designer**, and then select **Next**

    > [!div class="mx-imgBorder"]
    > ![New model-driven app design prompt](media/add-page-to-model-app/solution-explorer-new-model-app-designer-prompt.png "New model-driven app design prompt")

1. Enter the new app's name.

    > [!div class="mx-imgBorder"]
    > ![New model-driven app name prompt](media/add-page-to-model-app/app-designer-name-prompt.png "New model-driven app name prompt")

### Open an existing model-driven app using modern app designer

1. Open [make.powerapps.com](https://make.powerapps.com/?cds-app-module-designer.isCustomPageEnabled=true)

1. On the left navigation pane, select **Solutions**, and then open the solution containing the existing model-driven app.

1. Open the model-driven app menu and select **Edit** > **Edit in preview** to open the modern app designer.

    > [!div class="mx-imgBorder"]
    > ![Open modern app designer preview](media/add-page-to-model-app/open-modern-app-designer-preview.png "Open modern app designer preview")
    
## Create or edit modern commands

Command designer can currently only be accessed through the modern app designer.

 > [!NOTE]
 > Classic commands cannot currently be edited within the command designer. 
 
 ### Edit the command bar
 
 1. Open modern app designer.
 
 1. Ensure to **publish** the app.
 
 1. Select any table from the **Pages** area.
 
 1. Click the elipsis. Select **Edit command bar (preview)** 
    > [!div class="mx-imgBorder"]
    > ![App Designer entry point](powerapps-docs/maker/model-driven-apps/media/CommandDesigner-App designer entry point.png "App Designer entry point")
 
 1. Select the **location** of the command bar you'd like to edit.
    > [!div class="mx-imgBorder"]
    > ![Select location](powerapps-docs/maker/model-driven-apps/media/CommandDesigner-Command bar location selection.png "Select location")
  
 ### Create a new command
 > [!NOTE]
 > Unlike classic commands, modern commands will only be displayed within the app you're editing. This prevents unwanted cross pollination within other apps as well as better runtime performance. Support for creating commands that display across all apps is targeted for a future release. 
 > A command component library will be created on your behalf to store **Power Fx** formulas.
 
 1. In command designer click **+ New**.
 
 1. Provide a **label** and or an **icon**.
 
 1. You may choose from any system font icons or web resource SVG files. To upload your own icon, choose **Web resource** then upload an **SVG**, **Save**, and **Publish** the web resource. 
 
 1. Move the command to the desired location. You may arrange modern commands amonst classic commands.
 
 1. Optionally provide **Tooltip** and **Accessibility** information
 
 
 ## User Power Fx for Actions and Visibility
 You may now use Power Fx for both Actions (what happens when the button is clicked) as well as visibility (logic to control when the button is visible). Power Fx is not supported in classic commands. 
 
 You’ll notice it has a similar formula bar experience as canvas apps. However, not all functions available within canvas apps are supported currently for commands. Additionally, we've introduced some new functions specific to commands.
 
 For working with **Dataverse** data you may use Power Fx formulas just as you would in canvas apps. The main difference is you cannot currently add additional tables as data sources directly from the command designer. However, you may **open the command component library in canvas studio and add additional tables as data sources** and then use them within the command designer. 
  > [!NOTE]
  > Dataverse is currently the only data source supported. Additional data sources will be supported in future releases. 
  
  ## Use JavaScript for Actions
  JavaScript is supported both in classic and modern commands and will remain supported for the foreseeable future. In fact, it’s now much simpler to create commands and associate your JavaScript. 
  
1.	For the **Action** choose **Run JavaScript**

2.	Click **Add library** or select one from the list. The list is populated with any libraries in use by the current command bar. 
 
    > [!div class="mx-imgBorder"]
    > ![Add JavaScript Library](powerapps-docs/maker/model-driven-apps/media/CommandDesigner-Add JavaScript Library.png "Add JavaScript Library")

3.	Search for existing JavaScript web resources or you may add your own. **Add**.

    > [!div class="mx-imgBorder"]
    > ![Add JavaScript Library](powerapps-docs/maker/model-driven-apps/media/CommandDesigner-Add JavaScript Library Modal.png "Add JavaScript Library")
 
4.	Type the Function name.	For example, chose the Main_system_library.js then call this function: XrmCore.Commands.Open.opennewrecord

6.	Add parameters to pass to your function. Existing functionality is supported here. 

    > [!div class="mx-imgBorder"]
    > ![Add Parameters](powerapps-docs/maker/model-driven-apps/media/CommandDesigner-Add JavaScript Parameters.png "Add Parameters")
 
  > [!NOTE] 
  > We are not supporting the use of calling multiple JavaScript libraries or calling multiple functions from a single command.
  
  
  ## Related topics
