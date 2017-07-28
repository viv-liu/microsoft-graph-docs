# Working with groups in Microsoft Graph

Groups are collections of [users](*) and [devices](*) (and more?) who share access to resources in Office365 or in your app. All operations in Microsoft Graph on groups require administrator consent. Using Microsoft Graph, you can perform the following operations and more:
- create groups
- check if a user is a member of a group
- list all groups a user is a member of
- list the members of a group
- add and remove members from a group
- add and remove owners of a group.

**NOTE**
Groups are only supported for enterprise accounts, and not supported for Microsoft personal accounts.

## Office 365 groups
Office 365 groups are for people who collaborate on a project or a team. Members share access to Office365 resources including:
- calendar
- drive
- notes
- plans (beta)

Using the API, your app can access these resources to further drive engaging collaboration scenarios. There are 2 types of Office 365 groups:

| Type | Use case | Shared resources |
|------------|-------|--------|
| Outlook group | Mail-driven collaboration | Mail conversations and threads, tasks (beta) |
| Microsoft Team | High velocity chat-driven collaboration | Channels, chat threads |
| *TODO* Yammer group | How to access Yammer posts through API? |

**NOTE** Today, only Outlook groups can be created through the API. 

**NOTE** Today, you can check if an Office 365 group is an Outlook group or a Microsoft Teams by trying GET /group/{id}/channels. If it works, then it's a Microsoft Team, else it's an Outlook group.

### Example of Outlook group

```http

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#groups/$entity",
    "id": "4c5ee71b-e6a5-4343-9e2c-4244bc7e0938",
    "deletedDateTime": null,
    "classification": "MBI",
    "createdDateTime": "2016-08-23T14:46:56Z",
    "description": "This group will be use to track improvements we make to the Graph IA site",
    "displayName": "Awesome Graph Docs",
    "groupTypes": [
        "Unified"
    ],
    "mail": "graphia@service.microsoft.com",
    "mailEnabled": true,
    "mailNickname": "graphia",
    "preferredLanguage": null,
    "proxyAddresses": [
        "smtp:graphia@microsoft.onmicrosoft.com",
        "SMTP:graphia@service.microsoft.com"
    ],
    "renewedDateTime": "2016-08-23T14:46:56Z",
    "securityEnabled": false,
    "theme": null,
    "visibility": "Public"
}
```
## Security group and mail-enabled security group
Security groups are for controlling user access to resources. By checking whether or not a user is a member of a security group, your app can make authorization decisions when that user is trying to access some secure resources in your app. Mail-enabled security groups are the same on principle, but with a group mailbox provisioned by default so the group can receive mail.

**OPENQ** Can SGs be nested?

### Example of security group

```http
{
    "@odata.type": "#microsoft.graph.group",
    "id": "f87faa71-57a8-4c14-91f0-517f54645106",
    "deletedDateTime": null,
    "classification": null,
    "createdDateTime": "2016-07-20T09:21:23Z",
    "description": "This group is a Security Group",
    "displayName": "RCG-Read Write-CG-11366",
    "groupTypes": [],
    "mail": null,
    "mailEnabled": false,
    "mailNickname": "mysg",
    "preferredLanguage": null,
    "proxyAddresses": [],
    "renewedDateTime": "2016-07-20T09:21:23Z",
    "securityEnabled": true,
    "theme": null,
    "visibility": null
}
```
## Dynamic membership 
All types of groups can have dynamic membership rules which automatically adds or removes users or **devices???** from the group based on criteria over their properties. For example, a "Marketing employees" group should include every user with the department property set to "Marketing", so that new marketing employees are automatically added to the group and employees who leave are automatically removed from the group. This rule can be specified in a "membershipRule" field during group creation as ```"membershipRule": 'user.department -eq "Marketing"'``` GroupType must also include ```"DynamicMembership"```. The following request creates a new Office365 group for the marketing employees: 

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

## Administrator master switch
Where can an admin disable groups master switch. Planner today will show error. 
Group creation should succeed if master switch is on.

# END OF ARTICLE, the rest are notes and scribbles

## Distribution group (not sure if this is possible through MS Graph, talk to Dhana)
- for lightweight email distribution
- we don’t provide management experiences to manage thousands of members in a flat list
- or nested scenarios 
- group info and membership stored in EXO

- what a DG looks like in Graph

## Office365 group

- **Outlook group**: groups working on an initiative, planner board to track tasks, email. Might not need a response right away. 
- **Yammer group**: no email, no calendar, enterprise social, good for communicating across org.
(creation not possible today, unless EDU endpoint: graph.microsoft.com/edu) 
- **Microsoft teams**: chat, high velocity orgs, live service, iterating rapidly with fast responses, stay in context within channel, code highlight
(creation not possible today)

**NOTE** 
Office365 groups cannot be nested. 
**OPENQ**
- What happens if the tenant doesn't have the OneDrive license? Is that part turned off?
- What each flavor looks like in Graph 


**OPENQ** Can you read a DG if it already exists? A: Yes
No way to tell Teams from Outlook group
```http
{
    "error": {
        "code": "DynamicGroupLicenseError_NoProperLicense",
        "message": "Tenant does not have proper license to create/update dynamic group membership properties.",
        "innerError": {
            "request-id": "23101d28-229d-446c-b2c3-f5a28ffadb46",
            "date": "2017-07-13T17:01:33"
        }
    }
}
```

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

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#groups/$entity",
    "id": "7b91471f-47fb-483b-9b1f-e64ef9a90d34",
    "deletedDateTime": null,
    "classification": null,
    "createdDateTime": "2017-07-13T20:47:10Z",
    "description": "Marketing department folks",
    "displayName": "Marketing department",
    "groupTypes": [
        "Unified",
        "DynamicMembership"
    ],
    "mail": "marketing@adatumisv.onmicrosoft.com",
    "mailEnabled": true,
    "mailNickname": "marketing",
    "membershipRule": "user.department -eq \"Marketing\"",
    "membershipRuleProcessingState": "On",
    "onPremisesLastSyncDateTime": null,
    "onPremisesProvisioningErrors": [],
    "onPremisesSecurityIdentifier": null,
    "onPremisesSyncEnabled": null,
    "preferredLanguage": null,
    "proxyAddresses": [
        "SMTP:marketing@adatumisv.onmicrosoft.com"
    ],
    "renewedDateTime": "2017-07-13T20:47:10Z",
    "resourceBehaviorOptions": [],
    "resourceProvisioningOptions": [],
    "securityEnabled": false,
    "theme": null,
    "visibility": "Public"
}
```

```http
https://graph.microsoft.com/v1.0/groups
{
    "description": "Test DG",
    "displayName": "Test DG",
    "groupTypes": [],
    "mailEnabled": true,
    "mailNickname": "dg",
    "securityEnabled": false,
}

{
    "error": {
        "code": "InternalServerError",
        "message": "The given key was not present in the dictionary.",
        "innerError": {
            "request-id": "f0a38b42-2553-442d-8c33-c3a7bcd07074",
            "date": "2017-07-20T18:06:47"
        }
    }
}
```

## Viv Test MS Team

```http
{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#groups/$entity",
    "id": "64fde3af-08ed-4c88-9cda-0f006a3286b1",
    "deletedDateTime": null,
    "classification": "MBI",
    "createdDateTime": "2017-06-19T22:35:32Z",
    "description": "Viv Test",
    "displayName": "Viv Test",
    "groupTypes": [
        "Unified"
    ],
    "mail": "VivTest@service.microsoft.com",
    "mailEnabled": true,
    "mailNickname": "VivTest",
    "membershipRule": null,
    "membershipRuleProcessingState": null,
    "onPremisesLastSyncDateTime": null,
    "onPremisesProvisioningErrors": [],
    "onPremisesSecurityIdentifier": null,
    "onPremisesSyncEnabled": null,
    "preferredLanguage": null,
    "proxyAddresses": [
        "smtp:VivTest@microsoft.onmicrosoft.com",
        "SMTP:VivTest@service.microsoft.com"
    ],
    "renewedDateTime": "2017-06-19T22:35:32Z",
    "resourceBehaviorOptions": [],
    "resourceProvisioningOptions": [],
    "securityEnabled": false,
    "theme": null,
    "visibility": "Private"
}
```

## Yammer group

```http
https://graph.microsoft.com/beta/groups/bcb056a1-bf93-4d0e-94ce-ffcdcc468b2e

```