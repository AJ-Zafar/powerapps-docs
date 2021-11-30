---
title: Map input fields of a component
description: Learn about how to map input fields of a component to the table or record.
author: hemantgaur
ms.service: powerapps
ms.subservice: canvas-developer
ms.topic: article
ms.date: 11/29/2021
ms.author: hemantg
ms.reviewer: tapanm
search.audienceType:
  - maker
search.app:
  - PowerApps
contributors:
  - hemantgaur
  - tapanm-msft
  - gregli-msft
---

# Map input fields of a component

[This article is pre-release documentation and is subject to change.]

A component can receive input values to emit or process data using custom input properties. In this article, you'll learn about working with such components that expect one or more input properties with a specific schema for the given table or record.

> [!TIP]
> To learn more about using custom input and output properties in components, go to [Custom properties in components](create-component.md#custom-properties).

## Map columns

Use the [RenameColumns()](functions/function-table-shaping.md) function to rename one or more columns of a table
to match the input property schema for input column selection.

For example, consider a component that expects a table input with the following format:

| **Flavor** | **UnitPrice** | **QuantitySold** |
|------------|---------------|------------------|
| Strawberry | 1.99          | 20               |
| Chocolate      | 2.99          | 45               |

The input property expects table data type:

:::image type="content" source="media/map-component-input-fields/custom-input-property.png" alt-text="Custom input property expecting Table data type.":::

The schema of the input property looks like the following formula:

```powerapps-dot
Table({Flavor: "Strawberry",UnitPrice: 1.99, QuantitySold:20})
```

:::image type="content" source="media/map-component-input-fields/custom-property-formula.png" alt-text="Custom input property formula defined as table and sample values.":::

The app consuming this component has the following "IceCreams" table that doesn’t match with the component schema:

| **FlavorName** | **Price** | **SaleNumber** |
|----------------|-----------|----------------|
| Strawberry     | 1.99      | 20             |
| Chocolate      | 2.99      | 45             |

:::image type="content" source="media/map-component-input-fields/icecreams-table.png" alt-text="Schema of IceCreams table.":::

To map the correct fields, use **RenameColumn()** function to rename expected columns.

```powerapps-dot
RenameColumns(IceCreams,"cra56_flavorname","Flavor","cra56_price","UnitPrice","cra56_salenumber","QuantitySold")
```

:::image type="content" source="media/map-component-input-fields/app-custom-input-property.png" alt-text="App using component that uses custom input property mapping with the correct columns using RenameColumns function.":::

**IceCreams** table now looks like the following and the input fields are
selected with matching field names.

| **FlavorName** | **Price** | **SaleNumber** |
|------------|---------------|------------------|
| Strawberry | 1.99          | 20               |
| Chocolate  | 2.99          | 45               |

## Map records

Use [With()](functions/function-with.md) function to map a single record.

For example, continuing from the [earlier example](#map-columns) for mapping columns, a component custom input takes a record and the schema is:

```powerapps-dot
{Flavor: "Strawberry",UnitPrice: 1.99, QuantitySold: 20}
```

:::image type="content" source="media/map-component-input-fields/custom-record-property.png" alt-text="Custom input property formula defined as record and sample values.":::

Since the **IceCreams** data source expects column names as **FlavorName**, **Price**, and **SaleNumber**, we'll need to change the mapping for the record once the component is added to the app.

Use **With()** function to select the fields of the **IceCreams** table and map them to the component input:

```powerapps-dot
With(Gallery3.Selected,{Flavor:FlavorName,UnitPrice:Price,QuantitySold:SaleNumber})
```

:::image type="content" source="media/map-component-input-fields/app-component-record.png" alt-text="Component record in app mapped to the data source schema.":::

Below animation shows the example of component added to the app that shows the selected record from the gallery (above the component):

:::image type="content" source="media/map-component-input-fields/component-selected-record.gif" alt-text="Animation that shows selection of a record from gallery above changing the component instance text below.":::

## Map tables

, and [ForAll()](functions/function-forall.md) function for a table of records.


Not recommended method
----------------------

The data field selection dropdown is for mapping input fields with the
definition schema. When there is a component which has a record or table type of
input property in the screen and your input a record or table for the input, you
can find the data field selection dropdowns in the advanced property pane shown
below.

Few people have used it. By default, the selection assigns fields quietly. This
has caused confusions. As the example below, it assigned the same field to each
expected field by default. Not knowing where to change it and why it’s assigned
by default both are very frustrating behaviors. In this blog, we also have some
recommendations of how to do the input mapping whiling giving the input.

![Graphical user interface, application Description automatically generated](media/54d4845b50a0339ac3d457ac356006b1.png)

The current implementation of the feature will be phased out. This starts by
introducing the switch in Settings \> Upcoming features \> Retired \> XXXX. For
now, all new apps will have this set to *off by default*. All existing apps will
have this switch set to *on by default*. The apps with this feature will
continue to work. You will be able to turn on the feature again for new apps,
however this is discouraged at this time. 
