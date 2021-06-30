---
title: Add editable tables in canvas apps | Microsoft Docs
description: Learn how to configure an app interface with editable tables that allow you to edit data from the data source directly through the app.
author: denisem-msft
ms.service: powerapps
ms.topic: tutorial
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 6/11/2021
ms.author: denisem
search.audienceType: 
  - maker
search.app: 
  - PowerApps
---

# Add editable tables in canvas apps

Designing a productivity application to have related data and functions in one place enables you to achieve more without having to switch back and fourth between the screens. Microsoft Excel is one such example that allows editing data real-time in fast and efficient way.

Using Power Apps, you can apply the same concept by providing it as a front end to any data source. You're also able to customize it even more.

![Power Apps front end](./media/add-editable-tables/admin-cat-mngmt-app.png "Power Apps front end")

This tutorial uses the following components to make a sample app:

- A data source (Microsoft Dataverse, you can also use Excel instead)
- Form&mdash;For new items
- Gallery&mdash;To display existing items and
- Text input controls&mdash;To update existing items

## Prerequisites

To follow this tutorial, you'll need access to a [Power Platform environment](/power-platform/admin/environments-overview#types-of-environments), and the ability to create tables in Microsoft Dataverse.

The tutorial uses the following structure to create the sample app:

![Dataverse columns for sample table](./media/add-editable-tables/dataverse-table-columns.png "Dataverse columns for sample table")

To learn about how to add columns, see [Work with table columns](/powerapps/teams/table-columns).

A new main form has been created to add sample data:

![New main form for adding data to Dataverse table](./media/add-editable-tables/main-form.png "New main form for adding data to Dataverse table")

To learn about how to create a main form with the required columns, see [Create a form](/powerapps/maker/model-driven-apps/create-and-edit-forms#create-a-form). Be sure to use the correct [form order](/powerapps/maker/model-driven-apps/control-access-forms#set-the-form-order) for adding records using the new form.

## Step 1: Create blank app

1. Sign in to [Power Apps](https://make.powerapps.com).
1. Select **Canvas app from blank** under **Make your own app** in Power Apps Home.
1. Enter a name for the app, such as "Catalog Management App".
1. Choose **Tablet** format.
1. Select **Create**.

## Step 2: Add a data source

This section shows how to add a Dataverse table as the data source for the sample app. You can also use an Excel file from a SharePoint site, or OneDrive as the data source; or any other data source type of your choice.

1. From the left-pane, select **Data** > **Add data**.
1. Select **See all tables**.
1. Select **Editable tables**, or the table that you created earlier.

    ![Add Dataverse table as the data source](./media/add-editable-tables/add-table-data-source.png "Add Dataverse table as the data source")

For more information about adding a connection to a canvas app, see [Add data source](add-data-connection.md#add-data-source).

## Step 3: Set up a form control

This step adds a form control to add new items.

1. Select **+** (Insert) > **Edit form**.

    ![Add edit form control](./media/add-editable-tables/add-edit-form-control.png "Add edit form control")

1. On the right-pane, choose the table as the data source for the edit form control.

    ![Choose the table as the data source for edit form control](./media/add-editable-tables/select-data-source-for-form.png "Choose the table as the data source for edit form control")

1. Use the **Edit fields** properties option to select the columns to show on the edit form control. You can also change the column order as appropriate.

    ![Edit fields on the edit form control](./media/add-editable-tables/edit-fields.png "Edit fields on the edit form control")

1. Choose the **Default mode** for the form to **New**.

    ![Choose form control mode as New](./media/add-editable-tables/default-form-control-mode.png "Choose form control mode as New")

1. Adjust the **Width**, **Height** properties for size of the data cards to fill the canvas as appropriate.

1. On the left-pane, select **+** (Insert) > **Button**.

1. Update the button text to **Add product**.

1. Select **OnSelect** property for the button control from the top-left side of the screen.

1. In the formula bar, enter the following formula.

    ```powerapps-dot
    SubmitForm(Form1);
    NewForm(Form1);
    ```

    - [SubmitForm](functions/function-form.md) function submits the new product details to the Dataverse table.
    - [NewForm](functions/function-form.md) changes the mode of the form back to new form to add new products.
    - **Form1** in this formula is the name of the edit form control added earlier. Update the form name in this formula if your form name is different.

    ![Button OnSelect - new form](./media/add-editable-tables/button-onselect-newform.png "Button OnSelect - new form")

1. Insert a new Form control by clicking Insert > Forms > Edit Form

1. In the flyout, connect the data source to the one you just connected to, or manually update the DataSource property in the formula bar.

1. Change the Form.DisplayMode property to New (or FormMode.New)

1. Make sure to add a button to submit the form – Button.OnSelect = NewForm(Form)

   ![Add a button formula](./media/add-editable-tables/add-button-formula.png "Add a button formula.")



See additional documentation on the form control here

## See also

- [Control reference](reference-properties.md)
- [Working with formulas](working-with-formulas.md)

[!INCLUDE[footer-include](../../includes/footer-banner.md)]