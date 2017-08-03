# Working with groups in Microsoft Graph

Groups are collections of [users](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/user) who share access to resources in Microsoft services or in your app. Microsoft Graph provides you with APIs to create and manage a variety of different types of groups and group functionality to suit yoru scenario needs. All operations in Microsoft Graph on groups require administrator consent.

**NOTE**
Groups are only supported for work or school accounts, and not supported for Microsoft personal accounts.

## Office 365 groups
The power of Office 365 groups is in its collaborative nature, perfect for people who work together on a project or a team. They are created with resources that members of the group share including:

- SharePoint Document Library
- OneNote notebook
- SharePoint Team Site
- Planner

Your app can access and manage these resources through the API. Currently, there are 2 types of Office 365 groups accessible through the API

| Type           | Use case | Shared resources |
|----------------|----------|------------------|
| Outlook group  | Shared inbox mail-driven collaboration. | Mail conversations and threads, Outlook calendar |
| Microsoft Team | High velocity persistent chat-driven collaboration. | Channels, chat threads |

**NOTE** Currently, Microsoft Teams cannot be created through the API. 

**NOTE** Currently, you can check if an Office 365 group is an Outlook group or a Microsoft Teams by trying GET /group/{id}/channels. If it works, then it's a Microsoft Team, else it's an Outlook group.

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

## Security group and mail-enabled security group
Security groups are for controlling user access to resources. By checking whether or not a user is a member of a security group, your app can make authorization decisions when that user is trying to access some secure resources in your app. Mail-enabled security groups are the same on principle, but with a group mailbox provisioned by default so the group can receive mail. Security groups can have users and other security groups as members.

**NOTE** Currently, mail-enabled security groups cannot be created through the API.

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
All types of groups can have dynamic membership rules which automatically adds or removes members from the group based on criteria over their properties. For example, a "Marketing employees" group should include every user with the department property set to "Marketing", so that new marketing employees are automatically added to the group and employees who leave are automatically removed from the group. This rule can be specified in a "membershipRule" field during group creation as ```"membershipRule": 'user.department -eq "Marketing"'``` GroupType must also include ```"DynamicMembership"```. The following request creates a new Office365 group for the marketing employees: 

```http
https://graph.microsoft.com/beta/groups
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
