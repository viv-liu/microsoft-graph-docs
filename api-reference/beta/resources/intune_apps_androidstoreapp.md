﻿#  resource type

> **Important**: APIs under the /beta version in Microsoft Graph are in preview and are subject to change. Use of these APIs in production applications is not supported.

> **Note:** Using the Microsoft Graph APIs to configure Intune controls and policies still requires that the Intune service is [correctly licensed](https://go.microsoft.com/fwlink/?linkid=839381) by the customer.

Contains properties and inherited properties for Android store apps.

Inherits from [mobileApp](../resources/intune_apps_mobileapp.md)

## Methods
|Method|Return Type|Description|
|---|---|---|
|[List androidStoreApps](../api/intune_apps_androidstoreapp_list.md)|[androidStoreApp](../resources/intune_apps_androidstoreapp.md) collection|List properties and relationships of the [androidStoreApp](../resources/intune_apps_androidstoreapp.md) objects.|
|[Get androidStoreApp](../api/intune_apps_androidstoreapp_get.md)|[androidStoreApp](../resources/intune_apps_androidstoreapp.md)|Read properties and relationships of the [androidStoreApp](../resources/intune_apps_androidstoreapp.md) object.|
|[Create androidStoreApp](../api/intune_apps_androidstoreapp_create.md)|[androidStoreApp](../resources/intune_apps_androidstoreapp.md)|Create a new [androidStoreApp](../resources/intune_apps_androidstoreapp.md) object.|
|[Delete androidStoreApp](../api/intune_apps_androidstoreapp_delete.md)|None|Deletes a [androidStoreApp](../resources/intune_apps_androidstoreapp.md).|
|[Update androidStoreApp](../api/intune_apps_androidstoreapp_update.md)|[androidStoreApp](../resources/intune_apps_androidstoreapp.md)|Update the properties of a [androidStoreApp](../resources/intune_apps_androidstoreapp.md) object.|
|[List mobileAppCategories](../api/intune_apps_mobileappcategory_list.md)|[mobileAppCategory](../resources/intune_apps_mobileappcategory.md) collection|List properties and relationships of the [mobileAppCategory](../resources/intune_apps_mobileappcategory.md) objects.|
|[List mobileAppGroupAssignments](../api/intune_apps_mobileappgroupassignment_list.md)|[mobileAppGroupAssignment](../resources/intune_apps_mobileappgroupassignment.md) collection|List properties and relationships of the [mobileAppGroupAssignment](../resources/intune_apps_mobileappgroupassignment.md) objects.|
|[Get mobileAppInstallSummary](../api/intune_apps_mobileappinstallsummary_get.md)|[mobileAppInstallSummary](../resources/intune_apps_mobileappinstallsummary.md)|Read properties and relationships of the [mobileAppInstallSummary](../resources/intune_apps_mobileappinstallsummary.md) object.|
|[List mobileAppInstallStatuses](../api/intune_apps_mobileappinstallstatus_list.md)|[mobileAppInstallStatus](../resources/intune_apps_mobileappinstallstatus.md) collection|List properties and relationships of the [mobileAppInstallStatus](../resources/intune_apps_mobileappinstallstatus.md) objects.|
|[List userAppInstallStatuses](../api/intune_apps_userappinstallstatus_list.md)|[userAppInstallStatus](../resources/intune_apps_userappinstallstatus.md) collection|List properties and relationships of the [userAppInstallStatus](../resources/intune_apps_userappinstallstatus.md) objects.|

## Properties
|Property|Type|Description|
|---|---|---|
|id|String|Key of the entity. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|displayName|String|The admin provided or imported title of the app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|description|String|The description of the app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|publisher|String|The publisher of the app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|largeIcon|[mimeContent](../resources/intune_apps_mimecontent.md)|The large icon, to be displayed in the app details and used for upload of the icon. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|createdDateTime|DateTimeOffset|The date and time the app was created. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|lastModifiedDateTime|DateTimeOffset|The date and time the app was last modified. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|isFeatured|Boolean|The value indicating whether the app is marked as featured by the admin. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|privacyInformationUrl|String|The privacy statement Url. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|informationUrl|String|The more information Url. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|owner|String|The owner of the app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|developer|String|The developer of the app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|notes|String|Notes for the app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|uploadState|Int32|The upload state. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|appIdentifier|String|The Identity Name.|
|appStoreUrl|String|The Android app store URL.|
|minimumSupportedOperatingSystem|[androidMinimumOperatingSystem](../resources/intune_apps_androidminimumoperatingsystem.md)|The value for the minimum applicable operating system.|

## Relationships
|Relationship|Type|Description|
|---|---|---|
|categories|[mobileAppCategory](../resources/intune_apps_mobileappcategory.md) collection|The list of categories for this app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|groupAssignments|[mobileAppGroupAssignment](../resources/intune_apps_mobileappgroupassignment.md) collection|The list of group assignments for this mobile app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|installSummary|[mobileAppInstallSummary](../resources/intune_apps_mobileappinstallsummary.md)|Mobile App Install Summary. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|deviceStatuses|[mobileAppInstallStatus](../resources/intune_apps_mobileappinstallstatus.md) collection|The list of installation states for this mobile app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|
|userStatuses|[userAppInstallStatus](../resources/intune_apps_userappinstallstatus.md) collection|The list of installation states for this mobile app. Inherited from [mobileApp](../resources/intune_apps_mobileapp.md)|

## JSON Representation
Here is a JSON representation of the resource.
<!-- {
  "blockType": "resource",
  "keyProperty": "id",
  "@odata.type": "microsoft.graph.androidStoreApp"
}
-->
```json
{
  "@odata.type": "#microsoft.graph.androidStoreApp",
  "id": "String (identifier)",
  "displayName": "String",
  "description": "String",
  "publisher": "String",
  "largeIcon": {
    "@odata.type": "microsoft.graph.mimeContent",
    "type": "String",
    "value": "binary"
  },
  "createdDateTime": "String (timestamp)",
  "lastModifiedDateTime": "String (timestamp)",
  "isFeatured": true,
  "privacyInformationUrl": "String",
  "informationUrl": "String",
  "owner": "String",
  "developer": "String",
  "notes": "String",
  "uploadState": 1024,
  "appIdentifier": "String",
  "appStoreUrl": "String",
  "minimumSupportedOperatingSystem": {
    "@odata.type": "microsoft.graph.androidMinimumOperatingSystem",
    "v4_0": true,
    "v4_0_3": true,
    "v4_1": true,
    "v4_2": true,
    "v4_3": true,
    "v4_4": true,
    "v5_0": true,
    "v5_1": true
  }
}
```



