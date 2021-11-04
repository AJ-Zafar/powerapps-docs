---
title: "Localize labels and strings on a custom page (preview)" 
description: "This article outlines how to load resx files with localized content and how to use PowerFx to set content for labels on your custom page."
ms.custom: ""
ms.date: 11/01/2021
ms.reviewer: ""
ms.service: powerapps
ms.subservice: mda-maker
ms.topic: "article"
author: "mspilde"
ms.author: "matp"
manager: "kvivek"
search.audienceType: 
  - maker
search.app: 
  - "PowerApps"
  - D365CE
---
# Localize labels, messages and tooltips on a custom page (preview)

[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

This article outlines how to add localized content to a custom page by uploading [web resource RESX](/powerapps/developer/model-driven-apps/resx-web-resources) files for each language into your solution and how to use Power Fx to set the content on a label of a form. This functionality also applies to tooltips and any message that uses a text control.

  > [!IMPORTANT]
  > - This is a preview feature, and isn't available in all regions.
  > - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)]

## Localizing labels on a custom page

Providing localized content on a custom page in a model-driven app is vital when building apps that support global users or a multilingual organization.  This can be done by uploading text files in a .resx format as a web resource.  The files will need to contain the translated text that you want to use for labels on your custom pages.
The process has the following steps:
1.	Enable languages for your environment.
2.	Adding localized resx web resource files into your solution.
3.	Adding localized files to your custom page.
4.	Managing localized web resources.
5.	Adding localized strings to your label controls.
6.	Running your app with localized content.

## Enable languages for your environment

To add languages for your custom page you need to first enable the languages you want to support in the model-driven app where your custom page will be running.  Make sure you have enabled languages from the Power Platform admin center. More information: [Enable the language](/power-platform/admin/enable-languages#enable-the-language)

After completing the steps to enable language(s) in the environment, you'll need to create a RESX file for each language in the proper format for the strings you want localized on your custom page for your model-driven app.

After you have the created the RESX files with the localized strings you can add them into your solution as a web resource. There are two ways to accomplish this task, the first is to open your solution in make.powerapps.com and select the option to add a web resource to your solution in your environment or you can add a web resource while working on a custom page.  Adding while working on a custom page will be covered in the section on adding localized files to your custom page. More information: [RESX web resources](/powerapps/developer/model-driven-apps/resx-web-resources)

## Add localized RESX Web resource files to your solution

1. Go to [make.powerapps.com](https://make.powerapps.com),select the **Solutions** area, and open the solution you want.
1. On the command bar select **New** > **More** > **Web Resource**. This opens a panel to add your RESX web resource file.

All files added to your solution need to follow a specific format that includes **{filename}.LanguageID.resx**, where the [language id](/power-platform/admin/language-collations#language-and-associated-collation-used-with-dataverse) is the numeric value for that language. This format is necessary because the framework relies on the naming convention to identify which resource file should be used to associate the appropriate localized string to a label control.

> [!IMPORTANT]
> The RESX {filename} *must be the same* for all your files.  

For example, all localized string files might have the name `CustomPageLoc.LanguageID.resx`, which means for English it is `CustomPageLoc.1033.resx`, for French `CustomPageLoc.1036.resx`, and for Arabic `CustomPageLoc.1025.resx`.  The display name for every file added must be the same name.

In the example below all files have `CPLoc` as the display name. *The display name must be the same to ensure all localized content is used properly on a custom page for each language.*  We recommend that you add the corresponding name for the language in the **Description** field to help identify the content when you view the files in the custom page designer. Also, you'll need to add the same language's RESX that you're working in. For example, if you are authoring in English, be sure to add the English RESX file.

:::image type="content" source="media/page-localization/studio-web-resource-dialog.png"alt-text="Power Apps Studio web resource dialog.":::

After you have added your web resource to your solution make sure you publish your changes to ensure the file is included and available. Then you can add it to your custom page.  The following is a screen shot of the web resource RESX files that have been added to a solution and are now available to add to a custom page.

:::image type="content" source="media/page-localization/studio-web-resource-panel.png"alt-text="Power Apps Studio web resource panel.":::

## Adding localized files to your custom page

You can add localized files to your custom page when you're creating or editing a page.  More information: [Overview of custom pages for model-driven apps](/powerapps/maker/model-driven-apps/model-app-page-overview)

To add a language to your page, select the **Resources** icon on the left to open the **Resources** pane.

:::image type="content" source="media/page-localization/studio-page-resource-pointer.png "alt-text="Power Apps Studio custom page resources.":::

Select**Add resource** in either one of two places.

:::image type="content" source="media/page-localization/studio-page-resource-add-resource.png"alt-text="Power Apps Studio custom page add web resource.":::

A dialog opens that lists all the available web resources in your solution. To find your files quickly you can use the search at the top of the dialog to search for the **Display name** that displays all your localized RESX files. You only need to select and add the file that matches the language that you are using to author your page. In this example, the English file is the only file you need to add.

:::image type="content" source="media/page-localization/studio-page-web-resource-add-resource-dialog.png" alt-text="Power Apps Studio custom page add web resource dialog.":::

> [!NOTE]
> It isn't necessary to add every file. You only need to add one. The solution and platform maps the uploaded languages based on the display name to the language web resource files that you added to your solution. When you add multiple files, a dialog is displayed with an error message, which states that files have already been loaded to your page.

If you don't see the RESX web resource with the language you want to add in the dialog, you'll need to add the file to your solution using the steps described earlier in this article. 

After selecting **Add**, the panel closes, and the web resource is listed in the **Resources** pane.

:::image type="content" source="media/page-localization/studio-page-web-resource-add-resource-dialog-resx.png"alt-text="Power Apps Studio custom page web resource with resx file.":::

## Managing localized web resources

After a web resource language has been added to your page you can quickly and easily manage the file by selecting the **...** ellipses next to the file. A flyout opens where you can refresh the web resource if it has been changed or updated. You can also remove the resource from your page. You'll need to refresh the RESX resources on your page if the display name has changed or any of the string keys have been updated in the RESX file that's been published to your solution. Note that updating the translations in the RESX file and publishing the solution doesn't require the RESX on your page to be refreshed.

:::image type="content" source="media/page-localization/studio-page-web-resource-add-resource-dialog-refresh.png"alt-text="Power Apps Studio custom page web resource with resx file.":::

## Adding localized string to your label controls

To add localized content to your label control you'll need to select the label and set the function to the resource using the text function of the control. To do this, select the label control and select the **Text** function.

:::image type="content" source="media/page-localization/studio-page-text-option.png"alt-text="Power Apps Studio custom page text option on a control.":::

Using the text function, set the value to the web resource and the value you want that is in your web resource RESX file.  After setting the expression the content will appear in the preview for the page.

:::image type="content" source="media/page-localization/studio-page-text-function.png"alt-text="Power Apps Studio custom page text function for a control.":::

Save and publish your changes to the page.

> [!NOTE]
> Make sure you also save and publish your changes to the app. Saving and publishing both the page and app are needed to ensure your localized labels render with the appropriate strings at runtime.

## Running your app with localized content

1. After publishing your page and your app, select **Play** in the app designer to open the app in a separate browser tab.
1. Select your custom page on the site map.

   :::image type="content" source="media/page-localization/studio-page-runtime-1.png"alt-text="Power Apps Studio custom page runtime.":::

1. The labels for your controls display the localized content. Test each language added to your app and pages by selecting **Personalization Settings** under **Settings** (gear icon) at the top of the app.

   :::image type="content" source="media/page-localization/studio-page-runtime-2.png"alt-text="Power Apps Studio custom page runtime setting options.":::

1. Then, on the **Languages** tab, set the **User Interface Language** to the language you would like to test.

   :::image type="content" source="media/page-localization/studio-page-runtime-3.png"alt-text="Power Apps Studio custom page runtime setting dialog.":::

### See also
[Create or edit model-driven app web resources to extend an app](create-edit-web-resources.md)