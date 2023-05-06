---
title: Customize and build your mobile app using the wrap wizard
description: Learn about how to use the wrap wizard to package canvas apps into a native mobile app package.
author: makolomi
ms.topic: article
ms.custom: canvas
ms.reviewer: mkaur
ms.date: 2/9/2023
ms.subservice: canvas-maker
ms.author: makolomi
search.audienceType: 
  - maker
contributors:
  - mkaur
  - makolomi
---

# Use the wrap wizard to build your mobile app

Use the wrap feature to package one or more canvas app(s) as a single native mobile app package using the step-by-step wizard.

The wrap feature in Power Apps lets you create native mobile versions of your [canvas apps](../../canvas-apps/getting-started.md) as custom-branded Android and iOS mobile apps. You can distribute such *wrapped* native mobile apps to the end users through Microsoft Intune, App Center or other native distribution methods.

Wrap feature allows you to create mobile apps for iOS, Android or Google Play Store:

- iOS (IPA package)
- Android (APK package)
- Google Play Store (AAB package)

The wrap feature will wrap your canvas apps in a native mobile app shell that you can digitally sign and distribute.
You can use Microsoft Intune, App Center or Apple Business Manager, Google Play Store to distribute your native mobile apps created with wrap.

When you update your app and republish it, the app is automatically updated.


## Prerequisites

You'll need access to:
- [Azure portal](https://portal.azure.com/) to register your app and configure the API permissions on the Microsoft Identity platform.
- [App Center](https://appcenter.ms/) to add new organization and apps.
- This feature requires the apps to be part of a  [managed or unmanaged solution](/power-platform/alm/solution-concepts-alm#managed-and-unmanaged-solutions). If your apps aren't part of a solution already, add them to an existing or a new solution. More information: [Create a canvas app from within a solution](../../canvas-apps/add-app-solution.md#add-an-existing-canvas-app-to-a-solution). 

To use Android platform, ensure you [<u>generate keys</u>](code-sign-android.md#generate-keys), and then [generate signature hash](code-sign-android.md#generate-signature-hash) before you [<u>register the app</u>](how-to.md#app-registration). You'll need the generated signature hash to configure the **Redirect URI**.

## Add canvas app to solution

Wrap for Power Apps requires the apps to be part of a solution. If your canvas apps aren't part of a solution already, add them to an existing or a new solution. Go to **Solutions** section, select a solution and press **Edit** button.

:::image type="content" source="media/wrap-canvas-app/select-solution.png" alt-text="Select a solution.":::

Chooose **+ Add existing** option from the top menu and select **App > Canvas app** in the dropdown list.

:::image type="content" source="media/wrap-canvas-app/select-add-existing.png" alt-text="Select Add existing from the menu.":::

Select **Oustide Dataverse** tab and choose your app from the list. Press **Add** button to add this app to a solution.

:::image type="content" source="media/wrap-canvas-app/add-app.png" alt-text="Select Add app to a solution.":::

More information: [Add an app to a solution](../../canvas-apps/add-app-solution.md#add-an-existing-canvas-app-to-a-solution)


## Create native mobile apps for iOS and Android using the wizard

1. Sign in to [Power Apps](https://make.powerapp.com/).

2. Select **Apps**, from the left navigation pane. 

3. Select the app that you want to wrap, and then select **Wrap** on the command bar.

   > [!div class="mx-imgBorder"] 
   > ![Select the app to wrap.](media/how-to-v2/select-app-to-wrap.png "Select the app to wrap")


### Step 1: Select Apps 

1. On the **Select the app(s) to wrap** screen, select your primary and secondary app.

   - **Primary app**: Select the app your end users will see when they launch the mobile app.
   - **Secondary app(s)**: Optional additional apps that you can bundle the same build for mobile app package along with the Primary app.

     > [!div class="mx-imgBorder"] 
     > ![Choose the apps to wrap.](media/how-to-v2/select-apps.png "Choose the apps to wrap")
  
     > [!NOTE]
     > You can use the same Primary app in multiple wrap projects.

2.  Select **Next**.

### Step 2: Target Platform 

1.  On the **Choose mobile platform to target** screen, enter a **Bundle ID** of our choice. 

    > [!NOTE]
    > The **Bundle ID** is a unique identifier that you create for your app. A bundle ID must contain one period (.) and no spaces. 

2. Under **Target platforms(s)**, select all the mobile platforms that your end users use on their mobile devices.

3. (Optional) Set the **Sign my app** toggle to **ON** to automatically code sign your mobile app, then select the **Azure Key Vault URI** from the list and click **Next**. 
If you do not have any entries in **Azure Key Vault URI** list, you need to create **Azure Key Vault** first. For more information, see [Set up Azure Key Vault for automated code signing](#Set-up-Azure-Key-Vault-for-automated-code-signing).

You can also code sign your mobile app package manually instead of using automatic code signing in wrap wizard. For more information on how to code sign your app manually, see:
  
   - [Code sign for iOS](code-sign-ios.md)
   - [Code sign for Android](code-sign-android.md) 
   - [Code sign for Google Play Store](https://developer.android.com/studio/publish/app-signing)

4.  Select **Next**.

### Step 3: Configure Branding

1. On the **Configure Branding Step**, set the following look and feel options for your app:
   
   - **App icons**: Upload icons to use for your app. All five icons need to be selected for your wrapped mobile app
   - **Splash screen image**: Image that will be used on the splash screen of your mobile app, while it loads. Default image used when not provided.
   - **Welcome screen image**: Image that will be used on the welcome (sign in) screen of your mobile app, while it loads. Default image used when not provided.
   - **Background fill color**: Hexadecimal color code used for the background of the welcome screen.
   - **Button fill color**: Hexadecimal color code used to fill the button color.
   - **Status bar text theme**: Color for the status bar text at the top of the app.
   
     > [!NOTE]
     > All the images must be in .png format. 

2.  Select **Next**.

### Step 4: Register app

On the **Register your app** screen, register your application in Azure to establish a trust relationship between your app and the Microsoft identity platform. Your app must be registered in Azure ADD so that your app users can sign in. 

#### New app registration

Select **New app registration** to create a new registration for your app.

   > [!div class="mx-imgBorder"] 
   > ![New app registration.](media/how-to-v2/new-app-reg.png "New app registration")




### Step 5: Manage output

On the **Manage output** screen, create or select an existing App Center location to send your mobile app once the build is complete. To create a new location, seect **New location** on top of the screen and then select **Android** or **iOS**.

- **Android**: Choose an existing location or create a new location.

- **iOS**: Choose an existing location or create a new location.

You can also choose to create your App Center location manually at [App Center](https://appcenter.ms/). For more information. see [Create an App Center container for your mobile app manually](#Creating-an-App-Center-container-for-your-mobile-app-manually).

### Step 6: Wrap up

On the **Wrap up** screen, review the app details and then select **Build**.
After a successful build, you'll see your mobile app in the App Center location that you have selected in the previous step.

## Set up Azure Key Vault for automated code signing 

You need to have [Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/general/basic-concepts) set up to automatically sign your Android or iOS mobile app package in **Step 2** of wrap wizard.
  
**Prerequisites**
  
- You'll need to have a [Apple account](https://developer.apple.com) enrolled in Apple developer Program or Apple enterprise developer program.
- Create a [distribution certificate](code-sign-ios.md#create-the-distribution-certificate) or [ad-hoc Provisioning Profile](code-sign-ios.md#create-an-ios-provisioning-profile) or enterprise provisioning profile.
- Azure Active Directory subscription to [create Key Vault](/azure/key-vault/general/quick-create-portal).
- Admin access for your tenant.
   
Follow these steps to create Azure Key Valut and configure KeyVault URI:
  
1. Sign in to your tenent as an admin and create an Azure service principal for 1P AAD application: 4e1f8dc5-5a42-45ce-a096-700fa485ba20 (WrapKeyVaultAccessApp) by running the following script: <br>
`Connect-AzureAD -TenantId <your tenant ID> New-AzureADServicePrincipal -AppId 4e1f8dc5-5a42-45ce-a096-700fa485ba20 -DisplayName "Wrap KeyVault Access App"`
  
2. Add a role to the service principal listed above in the subscription where the Key Vault is going to exist. For detailed steps, see [Assign a user as an administrator of an Azure subscription](/azure/role-based-access-control/role-assignments-portal-subscription-admin). Note: In step 3, you may choose Contributor, as only a minimal role is required to access the Key vault.

3. Create or access existing key vault: [Create a key vault using the Azure portal](/azure/key-vault/general/quick-create-portal)
4. Add access policies for the key vault.
  
   :::image type="content" source="media/wrap-canvas-app/wrap-keyvault.gif" alt-text="Add access policies for the key vault.":::
  
5. Depending on your device, do one of following:
   - For Android, create the .pfx file upload it to the keyvault certificate section. More information: [Generate keys](code-sign-android.md#generate-keys) 
  
     :::image type="content" source="media/wrap-canvas-app/wrap-1.png" alt-text="Create a cert for Android.":::
     > [!NOTE]
      > The name of the certificate must be present in the tag step. The password also needs match the password you entered during the store pass parameter used to create the .pfx file in step 2.
  
   - For iOS: 
     1. Install the .cer into Keychain Access app by double clicking it. More information: [Create the distribution certificate](code-sign-ios.md#create-the-distribution-certificate) </br> Then export the file as a .p12 file by right clicking your certificate file and the select **Export** and select the file format .p12. 
        > [!NOTE]
        > The .p12 password that you set in step 4 is required when uploading it to the keyvault in the next step.
     2. [Create the provisioning profile](code-sign-ios.md#create-an-ios-provisioning-profile) and run the following command to encode it to base64:
        - Mac: base64 `-i example.mobileprovision`
        - Windows:  `certutil -encode data.txt tmp.b64`
     
     3. Get the outputted `base64` string from previous step and upload to Keyvault secret. Then, get the .p12 file and upload it to Keyvault Certificate.
  
        :::image type="content" source="media/wrap-canvas-app/wrap-2.png" alt-text="Create a cert for iOS.":::

6. Once iOS or Android certificates are created and uploaded, add three tags with the name as the bundle id, and the value corresponding to the name of the uploaded certificate(s).
  
     :::image type="content" source="media/wrap-canvas-app/wrap-3.png" alt-text="Add tags.":::
  
  
  
## Creating an App Center container for your mobile app manually

You can manually create your App Center contaner for you mobile app. More information: [App Center container](overview.md#app-center-container)

> [!TIP]
> For more information about App Center, go to [Visual Studio App Center documentation](/appcenter/).

1. Go to [App Center](https://appcenter.ms/).
1. Sign in with your work or school account.
1. If you don't have any existing organization, select **Add new** &gt; **Add new organization** to create a new organization.
1. Select the organization from the list on the left-pane.
1. Select **Apps** &gt; **Add app**.
1. Enter app name.
1. Select app release type.
1. Select **Custom** OS for iOS apps, or **Android** OS for Android apps.

    > [!NOTE]
    > You must create separate App Center containers for each platform.

1. For **Android** OS, select **Platform** as **React Native**.

    > [!NOTE]
    > **Platform** must be **React Native** for all apps in App Center.

    :::image type="content" source="media/wrap-canvas-app/app-center-app.png" alt-text="App center app configuration.":::

1. Select **Add new app**.

1. Copy the app's App Center URL that you'll need later when configuring the wrap project inside Power Apps.

    For example, `https://appcenter.ms/orgs/Contoso-sales/apps/Sample-canvas-app-for-Android-OS/`

    :::image type="content" source="media/wrap-canvas-app/app-center-url.png" alt-text="App center URL.":::

    More information: [App Center URL](overview.md#app-center-url)
 

## Signing your mobile app package manually (optional)
If you do not want to aumomatically sign your mobile app package during wrap process in **Step 2**, you can do so manually after the mobile app package is build. [Code signing](overview.md#code-signing) process is different for Android and iOS devices.

- [Code signing for iOS](code-sign-ios.md)
- [Code signing for Android](code-sign-android.md)
- [Code signing for Google Play Store](https://developer.android.com/studio/publish/app-signing)

## Test and distribute mobile app package

For testing and distribution, see [App Center Test](/appcenter/test-cloud/) and [Distribute](/appcenter/distribution/).

### See also

- [Wrap overview](overview.md)
- [Code sign for iOS](code-sign-ios.md)
- [Code sign for Android](code-sign-android.md)
