# Activate Application

`PUT /auth/apps/{appId}/activate`

Activate a specific application

{% hint style="info" %}
* User action signature required. See [User Action Signing](../user-action-signing/) for more information.
* Request headers required. See [Request Headers](../../../getting-started/request-headers.md) for more information.
* Authentication required. See [Authentication Headers](../../../getting-started/request-headers.md#authentication-headers) for more information.
{% endhint %}

## Required Permissions

| Name                     | Conditions      |
| ------------------------ | --------------- |
| `Auth:Apps:Update`       | Always Required |
| `Auth:Types:Application` | Always Required |

## Parameters

|                                            |                                       |
| ------------------------------------------ | ------------------------------------- |
| `appId` <mark style="color:red;">\*</mark> | the ID of the application to activate |

### Example

```
/auth/apps/ap-7pdin-482de-87l94d8909f9lve0/activate
```

## Responses

{% hint style="info" %}
* See [Common Errors](../../../getting-started/errors.md#common-errors) for common errors.
* See [Application Management Errors](../../../getting-started/errors.md#application-management-errors) for application management specific errors.
{% endhint %}

{% tabs %}
{% tab title="200" %}
**Success** - The application that was modified

```json
{
  "appId": "ap-4s6se-e2t7n-89gfg50iaos73pm6",
  "kind": "ServerSideApplication",
  "orgId": "or-yanke-mars-6ulofamogg8fs87v",
  "expectedRpId": "localhost",
  "expectedOrigin": "http://localhost:3000",
  "name": "Codys Localhost Server-Side App",
  "isActive": true,
  "permissionAssignments": [
    {
      "permissionId": "pm-lit-yanke-46bfekf1548aeph4",
      "permissionName": "WalletAdmin",
      "assignmentId": "",
      "operations": [
        "Auth:Action:Sign",
        "Auth:Apps:Read",
        "Auth:Types:Application",
        "Auth:Types:Employee",
        "Auth:Types:EndUser",
        "Auth:Types:Pat",
        "Auth:Types:ServiceAccount",
        "Auth:Users:Read",
        "Balances:Read",
        "Payments:Create",
        "Payments:Read",
        "PublicKeyAddresses:Read",
        "PublicKeys:Create",
        "PublicKeys:Read",
        "Signatures:Create",
        "Signatures:Read",
        "Transactions:Create",
        "Transactions:Read",
        "Wallets:Create",
        "Wallets:Read",
        "Wallets:Update"
      ]
    }
  ],
  "accessTokens": [
    {
      "dateCreated": "2023-04-11T16:38:55.098Z",
      "credId": "Y2ktM2J2YnEtdWF1bDctOG8zYmFrY2d2b2xhZTUzYg",
      "isActive": true,
      "kind": "Application",
      "linkedAppId": "ap-4s6se-e2t7n-89gfg50iaos73pm6",
      "linkedUserId": "",
      "name": "Codys Localhost Server-Side App",
      "orgId": "or-yanke-mars-6ulofamogg8fs87v",
      "permissionAssignments": [],
      "publicKey": "SHA256:lH6mAX/74SbWzSjwNBFapwJsUdccVQzA8yj7K8/R5eo",
      "tokenId": "to-3oona-vc575-9ueb17f2t4uq0m9b"
    }
  ]
}
```
{% endtab %}
{% endtabs %}
