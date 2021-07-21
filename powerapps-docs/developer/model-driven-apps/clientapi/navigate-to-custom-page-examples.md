---
title: "Navigating to and from a custom page in your model-driven app using client API (preview)" 
description: "This topic provides examples of navigating from a model-driven app page using the Client API to a custom page."
ms.custom: ""
ms.date: 07/21/2021
ms.reviewer: ""
ms.service: powerapps
ms.subservice: mda-maker
ms.topic: "how-to"
author: "aorth"
ms.author: "nabuthuk"
manager: "kvivek"
search.audienceType: 
  - maker
  - developer
search.app: 
  - "PowerApps"
  - D365CE
---

# Navigating to and from a custom page using client API (preview)

[!INCLUDE [cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

This topic provides examples of navigating from a model-driven app page using the [Client API](../client-scripting.md) to a custom page. It also includes examples of navigating from a custom page to other custom pages or a model page.

outlines the steps to use the Client API to open a custom page as a full page, dialog, or pane.  It provides examples of **custom** as a pageType value in [navigateTo (Client API reference)](reference/xrm-navigation/navigateto.md).

  > [!IMPORTANT]
  > - This is a preview feature, and isn't available in all regions.
  > - [!INCLUDE[cc_preview_features_definition](../../../includes/cc-preview-features-definition.md)]


## Navigating from a model page to a custom page

### Finding the logical page name

Each of the following Client API examples take the logical name of the custom page as an argument. The logical name is the **Name** value for the page in solution explorer. 

> [!div class="mx-imgBorder"]
> ![Find page logical name](../../../maker/model-driven-apps/media/navigate-page-examples/find-page-logical-name.png "Find page logical name")

### Open as an inline full page without context

Within a model-driven app Client API event, call the following code and update the **name** parameter to be the logical page name.

```javascript
// Inline Page
var pageInput = {
    pageType: "custom",
    name: "<logical custom page name>",
};
var navigationOptions = {
    target: 1
};
Xrm.Navigation.navigateTo(pageInput, navigationOptions)
    .then(
        function () {
            // Called when page opens
        }
    ).catch(
        function (error) {
            // Handle error
        }
    );
```

### Open as an inline full page with a record context

This example uses the `recordId` parameter within the [NavigateTo](reference/Xrm-Navigation/navigateTo.md) function to provide the custom page with the record to use.  Within the custom page, the Param function retrieves the value and uses Lookup function to retrieve the record.

```javascript
// Inline Page
var pageInput = {
    pageType: "custom",
    name: "<logical custom page name>",
    entityName: "<logical table name>",
    recordId: "<record id>",
};
var navigationOptions = {
    target: 1
};
Xrm.Navigation.navigateTo(pageInput, navigationOptions)
    .then(
        function () {
            // Called when page opens
        }
    ).catch(
        function (error) {
            // Handle error
        }
    );
```

### Open as a centered dialog

Within a model-driven app Client API event, call the following code and update the **name** parameter to be the logical custom page name.  This mode supports the sizing parameters similar to the [Main Form Dialogs](../../../developer/model-driven-apps/customize-entity-forms.md#open-main-form-in-a-dialog-using-client-api).

```javascript
// Centered Dialog
var pageInput = {
    pageType: "custom",
    name: "<logical custom page name>",
};
var navigationOptions = {
    target: 2, 
    position: 1,
    width: {value: 50, unit:"%"},
    title: "<dialog title>"
};
Xrm.Navigation.navigateTo(pageInput, navigationOptions)
    .then(
        function () {
            // Called when the dialog closes
        }
    ).catch(
        function (error) {
            // Handle error
        }
    );
```

### Open as a side dialog

Within a model-driven app Client API event, call the following code and update the **name** parameter to be the logical custom page name.

```javascript
// Side Dialog
var pageInput = {
    pageType: "custom",
    name: "<logical page name>",
};
var navigationOptions = {
    target: 2, 
    position: 2,
    width: {value: 500, unit: "px"},
    title: "<dialog title>"
};
Xrm.Navigation.navigateTo(pageInput, navigationOptions)
    .then(
        function () {
            // Called when the dialog closes
        }
    ).catch(
        function (error) {
            // Handle error
        }
    );
```

### Open from a grid page primary field link as a full page with record id

This example uses the recordId parameter within the NavigateTo function to provide the custom page with the record to use.  Within the custom page, the Param function retrieves the value and uses Lookup function to retrieve the record.

1. Create a web resource of type JScript like the following and update the **name** parameter to be the logical page name  

    ```javascript
    function run(selectedItems)
    {
        let selectedItem = selectedItems[0];
        
        if (selectedItem) {		
            let pageInput = {
                pageType: "custom",
                name: "<logical page name>",
                entityName: selectedItem.TypeName,
                recordId: selectedItem.Id,
            };
            let navigationOptions = {
                target: 1
            };
            Xrm.Navigation.navigateTo(pageInput, navigationOptions)
                .then(
                    function () {
                        // Handle success
                    }
                ).catch(
                    function (error) {
                        // Handle error
                    }
                );
        }
    }
    ```

1. Customize the entity ribbon CommandDefinition for OpenRecordItem to call the function above and include the **CrmParameter** with the value **SelectedControlSelectedItemReferences**

    ```xml
        <JavaScriptFunction FunctionName="run" Library="$webresource:cr62c_OpenCustomPage">
            <CrmParameter Value="SelectedControlSelectedItemReferences" />
        </JavaScriptFunction>
    ```

1. In the custom page, override the **App**'s **OnStart** property to use the Param function to get the recordId and lookup the record

    ```powerappsfl
    App.OnStart=Set(RecordItem, 
        If(IsBlank(Param("recordId")),
            First(<entity>),
            LookUp(<entity>, <entityIdField> = GUID(Param("recordId"))))
        )
    ```

    > [!NOTE]
    > After changing OnStart property, will need to run OnStart from App context menu. This function is only run one within a session

1. Then the custom page can use the **RecordItem** parameter as a record. Below is how to use it in an EditForm.

    ```powerappsfl
    EditForm.Datasource=<datasource name>
    EditForm.Item=RecordItem
    ```

### Known issues

- Navigate function does not have support for opening a model or custom page to a dialog. All navigates from a custom page open inline.
- Navigate function does not support opening.
    - Dashboard collection or specific dashboard.
    - Specific model form. 
- Custom page can only open into the current session’s current app tab in a multi-session model-driven app.


## Related topics

[Model-driven app custom page overview](../../../maker/model-driven-apps/model-app-page-overview.md)

[Add a custom page to your model-driven app](../../../maker/model-driven-apps/add-page-to-model-app.md)

[Navigation advanced examples for custom page](../../../maker/model-driven-apps/navigate-page-advanced-examples.md)

[navigateTo (Client API reference)](reference/xrm-navigation/navigateto.md)

