# Working with groups in Microsoft Graph

Groups are collections of [users](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/user) who share access to resources in Microsoft services or in your app. Microsoft Graph provides you with APIs to create and manage a variety of different types of groups and group functionality to suit your scenario needs. All operations in Microsoft Graph on groups require administrator consent.

**NOTE**
Groups are only supported for work or school accounts, and not supported for Microsoft personal accounts.

There are 2 general types of groups, distinguished by their use cases and specific properties' values on each resource. 

| Type              | Use case | groupType | mail-enabled | security-enabled | 
|-------------------|----------|-----------|--------------|------------------|
| Office 365 groups | Facilitating user collaboration with shared Microsoft online resources. | ["Unified"] | true | false | 
| Security groups | Controlling user access to in-app resources. | [] | false | true |


## Office 365 groups
The power of Office 365 groups is in its collaborative nature, perfect for people who work together on a project or a team. They are created with resources that members of the group share including:

- Outlook mail conversations and threads
- Outlook calendar
- SharePoint Document Library
- OneNote notebook
- SharePoint Team Site
- Planner

Your app can access and manage these resources through the API.

### Example of Outlook group

```http

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#groups/$entity",
    "id": "4c5ee71b-e6a5-4343-9e2c-4244bc7e0938",
    "deletedDateTime": null,
    "classification": "MBI",
    "createdDateTime": "2016-08-23T14:46:56Z",
    "description": "This is an Outlook group",
    "displayName": "OutlookGroup101",
    "groupTypes": [
        "Unified"
    ],
    "mail": "outlookgroup101@service.microsoft.com",
    "mailEnabled": true,
    "mailNickname": "outlookgroup101",
    "preferredLanguage": null,
    "proxyAddresses": [
        "smtp:outlookgroup101@microsoft.onmicrosoft.com",
        "SMTP:outlookgroup101@service.microsoft.com"
    ],
    "securityEnabled": false,
    "theme": null,
    "visibility": "Public"
}
```
Learn more about Office 365 groups and the administrator experiences [here](https://support.office.com/en-us/article/Learn-about-Office-365-groups-b565caa1-5c40-40ef-9915-60fdb2d97fa2).

## Security groups
Security groups are for controlling user access to resources. By checking whether or not a user is a member of a security group, your app can make authorization decisions when that user is trying to access some secure resources in your app. Security groups can have users and other security groups as members.

### Example of security group

```http
{
    "@odata.type": "#microsoft.graph.group",
    "id": "f87faa71-57a8-4c14-91f0-517f54645106",
    "deletedDateTime": null,
    "classification": null,
    "createdDateTime": "2016-07-20T09:21:23Z",
    "description": "This group is a Security Group",
    "displayName": "SecurityGroup101",
    "groupTypes": [],
    "mail": null,
    "mailEnabled": false,
    "mailNickname": "mysg",
    "preferredLanguage": null,
    "proxyAddresses": [],
    "securityEnabled": true
}
```
## Dynamic membership 
All types of groups can have dynamic membership rules which automatically add or remove members from the group based on user properties. For example, a "Marketing employees" group would include every user with the department property set to "Marketing", so that new marketing employees are automatically added to the group and employees who leave the department are automatically removed from the group. This rule can be specified in a "membershipRule" field during group creation as ```"membershipRule": 'user.department -eq "Marketing"'``` GroupType must also include ```"DynamicMembership"```. The following request creates a new Office 365 group for the marketing employees: 

```http
POST https://graph.microsoft.com/v1.0/groups
{
    "description": "Marketing department folks",
    "displayName": "Marketing department",
    "groupTypes": [
        "Unified",
        "DynamicMembership"
    ],
    "mailEnabled": true,
    "mailNickname": "marketing",
    "securityEnabled": false,
    "membershipRule": 'user.department -eq "Marketing"',
    "membershipRuleProcessingState": "on"
}
```

Learn more about formulating membershipRules in [advanced rules](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal).

**NOTE** Dynamic membership rules requires the tenant to have a license at tier [Azure Active Directory Premium P1](https://azure.microsoft.com/en-us/pricing/details/active-directory/) or greater.

## Common use cases

Using Microsoft Graph, you can perform the these common operations and more:

| **Use cases**		   | **REST resources**	| **See also** |
|:---------------|:--------|:----------|
| **Group object and methods** | | |
| Create new groups, get existing groups, update the properties on groups, and delete groups. Currently, only security groups and Outlook groups can be created through the API. | [group](group.md) | [Create new groups](../api/group_post_groups.md) <br/> [List groups](../api/group_list.md) <br/> [Update groups](../api/group_update.md) <br/> [Delete groups](../api/group_delete.md) |
| **Group membership methods** | | |
| List the members of a group, and add or remove members. | [user](user.md) <br/> [group](group.md)| [List members](../api/group_list_members.md) <br/> [Add member](../api/group_post_members.md) <br/> [Remove member](../api/group_delete_members.md)|
| Check if a user is a member of a group, get all the groups the user is a member of. | [user](user.md) <br/> [group](group.md)| [Check member groups](../api/group_checkmembergroups.md) <br/> [Get member groups](../api/group_get_membergroups.md)|
| List the owners of a group, and add or remove owners. | [user](user.md) <br/> [group](group.md)| [List owners](../api/group_list_members.md) <br/> [Add member](../api/group_post_members.md) <br/> [Remove member](../api/group_delete_members.md)|

## Other types of groups

You may encounter some of these types of groups being returned when performing operations that return collections of groups. The following groups can be returned through Microsoft Graph, but can't be created or otherwise managed using this API.

| Type              | Use case | groupType | mail-enabled | security-enabled | Learn more |
|-------------------|----------|-----------|--------------|------------------|------------|
| Groups in Yammer | Facilitating user collaboration with through Yammer posts. | ["Unified"] | true | false | [Yammer developer API docs](https://developer.yammer.com/docs) |
| Mail-enabled security groups | Controlling user access to in-app resources, with a shared group mailbox. | [] | true | true | [Manage mail-enabled security groups Exchange article](https://technet.microsoft.com/en-us/library/bb123521(v=exchg.160).aspx) |
| Distribution groups | Distributing mail to the members of the group. | [] | true | false | [Manage distribution groups Exchange article](https://technet.microsoft.com/en-us/library/mt577270(v=exchg.160).aspx) |
