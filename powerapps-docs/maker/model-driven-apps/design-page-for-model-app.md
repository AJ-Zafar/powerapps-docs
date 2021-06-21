---
title: "Design a custom page for your model-driven app" 
description: ""
ms.custom: ""
ms.date: 04/02/2020
ms.reviewer: ""
ms.service: powerapps
ms.topic: "article"
author: "aorth"
ms.assetid: b4098c96-bce1-4f57-804f-8694e6254e81
ms.author: "matp"
manager: "kvivek"
search.audienceType: 
  - maker
search.app: 
  - "PowerApps"
  - D365CE
---
# Design a custom page for your model-driven app (preview)

[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

This topic provides tips to design a custom page for use in a model-driven app.

  > [!IMPORTANT]
  > - This is a preview feature, and isn't available in all regions.
  > - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)]

## Supported controls in custom page
Custom page authoring will start with a subset of controls supported and will be gradually adding more controls.  Interaction with controls not supported may change so they should not be used until supported.

  | Control | Control Type | Notes |
  | --- | --- | --- |
  |Custom control|Custom|See [Power Apps Component Framework supported canvas control](../../developer/component-framework/overview.md)|
  |Label<sup>1</sup>|Display||
  |Text Box<sup>1</sup>|Input||
  |Date Picker<sup>1</sup>|Input|
  |Button<sup>1</sup>|Input|
  |Combo Box<sup>1</sup>|Input|
  |Check Box<sup>1</sup>|Input|
  |Toggle<sup>1</sup>|Input|
  |Radio Group<sup>1</sup>|Input|
  |Slider<sup>1</sup>|Input|
  |Rating<sup>1</sup>|Input|
  |Vertical Container|Layout|New responsive horizontal layout container|
  |Horizontal Container|Layout|New responsive horizontal layout container|
  |Rich Text Editor|Input|
  |Gallery|List|
  |Icon|Media|
  |Image|Media|
  |Edit Form|Input|
  |Display Form|Input|
  
  > [!Note]
  > Controls with “1” are the new control version used by canvas apps in Teams; these controls are from the [Fluent UI library](https://developer.microsoft.com/en-us/fluentui#/controls/web) wrapped with [Power Apps Component Framework](../../developer/component-framework/overview.md). 

More examples of custom components is available in  
[Custom component samples](../../developer/component-framework/use-sample-components.md).

## Enable responsive layout with Container control

Responsive custom page layouts are defined by building a hierarchy of **Horizontal layout container** and **Vertical layout container** controls.  These controls are found under sidebar Insert > Layout.

Resize the topmost container to fill the entire space with these properties. 

  ```powerappsfl
  X=0
  Y=0
  Width=Parent.Width
  Height=Parent.Height
  ```

Learn more about at [Building responsive layout](../canvas-apps/build-responsive-apps.md "Building responsive layout").

### Vertical Container with fixed header, flexible body, fixed footer

1. On the **Vertical Container**, set **Align (horizontal)** to **Stretch**

1. Insert three **Horizontal Container** controls within the parent **Vertical Container**

1. On the first and third child horizontal container controls, set **Stretch height** off and reduce height to space needed (for example, Height=80)

### Horizontal Container with two even child containers

1. On the parent horizontal container, set **Align (vertical)** to **Stretch**

1. Insert two **Vertical Container** controls within the parent **Horizontal Container**

## Styling custom page controls to align to model-driven app controls

By creating the custom page from the modern app designer, the important properties are defaulted.  

1. Controls need to use different Font size based on their position in the page hierarchy

    > [!Note]
    > custom page text has a up scaling of 1.33 so need to divide target FontSize by 1.33 to get the desired size


    | Label Type | Target FontSize | FontSize to use |
    | --- | --- | --- |
    |Page title|17|12.75|
    |Normal labels|14|10.52|
    |Small labels|12|9.02|

1. Primary and secondary button controls need the following styling changes

    Primary buttons:
    ```powerappsfl
    Color=RGBA(255, 255, 255, 1)
    Fill=RGBA(41,114,182,1)
    Height=35
    FontWeight=Normal
    ```

    Secondary buttons:
    ```powerappsfl
    Color=RGBA(41,114,182,1)
    Fill=RGBA(255, 255, 255, 1)
    BorderColor=RGBA(41,114,182,1)
    Height=35
    FontWeight=Normal
    ```


## Related topics

[Model-driven app custom page overview](model-app-page-overview.md)

[Using PowerFx in custom page](page-powerfx-in-model-app.md)

[Building responsive layout](../canvas-apps/build-responsive-apps.md)

[Add a custom page to your model-driven app](add-page-to-model-app.md)

[Navigating to and from a custom page in your model-driven app](navigate-page-examples.md)