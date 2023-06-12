# List Users

`GET /auth/users`

Returns a list of users

{% hint style="info" %}
* Request headers required. See [Request Headers](../../../getting-started/request-headers.md) for more information.
* Authentication required. See [Authentication Headers](../../../getting-started/request-headers.md#authentication-headers) for more information.
{% endhint %}

## Required Permissions

| Name              | Conditions      |
| ----------------- | --------------- |
| `Auth:Users:Read` | Always Required |

## Responses

{% tabs %}
{% tab title="200" %}
**Success: A list of users in the caller's org**

```JSON
{
  "items": [
    {
      "username": "permissioned-user@example.co",
      "userId": "us-C6N4O4-H3N3O6-7g9sb1259f8q8orq2gimrfo59l",
      "kind": "CustomerEmployee",
      "credentialUuid": "cr-4uc9u-12ij1-9s08327e73jqqcnr",
      "orgId": "or-yanke-mars-6ulofamogg84s87v",
      "permissions": [],
      "scopes": [],
      "isActive": true,
      "isServiceAccount": false,
      "isRegistered": true,
      "permissionAssignments": [
        {
          "permissionId": "pm-paris-lithi-17bf4kf01h8ajph4",
          "permissionName": "DfnsFullAdminAccess",
          "assignmentId": "",
          "operations": [
            "ApiKeys:Create",
            "ApiKeys:Read",
            "ApiKeys:Revoke",
            "AssetAccounts:Archive",
            "AssetAccounts:Create",
            "AssetAccounts:Read",
            "Auth:Action:Sign",
            "Auth:Apps:Create",
            "Auth:Apps:Read",
            "Auth:Apps:Update",
            "Auth:Creds:Create",
            "Auth:Creds:Read",
            "Auth:Creds:Update",
            "Auth:Types:Application",
            "Auth:Types:Employee",
            "Auth:Types:EndUser",
            "Auth:Types:Pat",
            "Auth:Types:ServiceAccount",
            "Auth:Users:Create",
            "Auth:Users:Delegate",
            "Auth:Users:Read",
            "Auth:Users:Update",
            "Balances:Read",
            "CallbackEvents:Read",
            "CallbackSubscriptions:Archive",
            "CallbackSubscriptions:Create",
            "CallbackSubscriptions:Read",
            "Employees:Read",
            "Payments:Create",
            "Payments:Read",
            "PermissionAssignments:Create",
            "PermissionAssignments:Read",
            "PermissionAssignments:Revoke",
            "PermissionPredicates:Archive",
            "PermissionPredicates:Create",
            "PermissionPredicates:Read",
            "PermissionPredicates:Update",
            "Permissions:Archive",
            "Permissions:Create",
            "Permissions:Read",
            "Permissions:Update",
            "Policies:Archive",
            "Policies:Create",
            "Policies:Read",
            "Policies:Update",
            "PolicyControlExecutions:Read",
            "PolicyControlExecutions:Update",
            "PolicyControls:Archive",
            "PolicyControls:Create",
            "PolicyControls:Read",
            "PolicyControls:Update",
            "PolicyRules:Archive",
            "PolicyRules:Create",
            "PolicyRules:Read",
            "PolicyRules:Update",
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
      ]
    },
    {
      "username": "no-permission-user@example.co",
      "userId": "us-4g62b-mvd1k-9do99i72qggnc78l",
      "kind": "CustomerEmployee",
      "credentialUuid": "cr-4uc9u-12ij1-9s08327e73jqqcnr",
      "orgId": "or-yanke-mars-6ulofamogg84s87v",
      "permissions": [],
      "scopes": [],
      "isActive": true,
      "isServiceAccount": false,
      "isRegistered": true,
      "permissionAssignments": []
    }
  ]
}
```
{% endtab %}

{% tab title="400" %}
**`X-DFNS-NONCE` header is missing or invalid**

```JSON
{
  "error": {
    "message": "request nonce is missing or invalid",
  }
}
```

**`X-DFNS-NONCE` already used**

```JSON
{
  "error": {
    "message": "request nonce has already been used"
  }
}
```
{% endtab %}

{% tab title="401" %}
**Caller not authenticated**

```JSON
{
  "error": {
    "message": "Not Authorized."
  }
}
```
{% endtab %}

{% tab title="403" %}
**Caller does not have access to the resource or endpoint**

```JSON
{
  "error": {
    "message": "CustomerEmployee us-24vwa-92s33-8tvqi1dg0a95megt is not authorized to perform operation (/auth/users)"
  }
}
```
{% endtab %}

{% tab title="500" %}
**An error occurred on the server**

```JSON
{
  "error": {
    "message": "Internal Server Error"
  }
}
```
{% endtab %}
{% endtabs %}

## Examples <a href="#examples" id="examples"></a>

{% tabs %}
{% tab title="TypeScript" %}
{% code title="listUsers.ts" overflow="wrap" lineNumbers="true" %}
```typescript
import { httpClient } from './dfnsHttpClient'
import { UserInfo } from './types'

const authToken = process.env['DFNS_API_KEY']
const appId = process.env['DFNS_APP_ID']
httpClient.get<{items: UserInfo[]}>(
  appId,
  authToken,
  '/auth/users'
).then((users) => {
  if (users.items.length === 0) {
    console.log('No Users')
    return
  }
  console.log(`Users for ${users.items[0].orgId}:`)
  for (const user of users.items) {
    console.log(`${user.isActive ? '' : '(DEACTIVATED) '}${user.username}`)
    console.log(`  Kind: ${user.kind}`)
    console.log(`  Registration Status: ${user.isRegistered ? 'Registered':'Pending'}`)
  }
}).catch((error) => {
  console.error(`Failed to list users: ${error.message}`)
})
```
{% endcode %}

{% code title="types.ts" overflow="wrap" lineNumbers="true" %}
```typescript
export type PermissionAssignmentInfo = {
  permissionName: string
  permissionId: string
  assignmentId: string
  operations?: string[]
}

export enum UserAuthKind {
  EndUser = "EndUser",
  CustomerEmployee = "CustomerEmployee",
  DfnsStaff = "DfnsStaff"
}

export type UserInfo = {
  username: string
  userId: string
  kind: UserAuthKind
  credentialUuid: string
  orgId: string
  permissions?: string[]
  scopes?: string[]
  isActive: boolean
  isServiceAccount: boolean
  isRegistered: boolean
  permissionAssignments: PermissionAssignmentInfo[]
}
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code title="listUsers.js" overflow="wrap" lineNumbers="true" %}
```javascript
import { httpClient } from './dfnsHttpClient'

const authToken = process.env['DFNS_API_KEY']
const appId = process.env['DFNS_APP_ID']
httpClient.get(
  appId,
  authToken,
  '/auth/users'
).then((users) => {
  if (users.items.length === 0) {
    console.log('No Users')
    return
  }
  console.log(`Users for ${users.items[0].orgId}:`)
  for (const user of users.items) {
    console.log(`${user.isActive ? '' : '(DEACTIVATED) '}${user.username}`)
    console.log(`  Kind: ${user.kind}`)
    console.log(`  Registration Status: ${user.isRegistered ? 'Registered':'Pending'}`)
  }
}).catch((error) => {
  console.error(`Failed to list users: ${error.message}`)
})
```
{% endcode %}
{% endtab %}

{% tab title="Curl" %}
{% code title="listUsers.sh" overflow="wrap" lineNumbers="true" %}
```shell
currentTime=$( date -u +"%Y-%m-%dT%H:%M:%SZ" )
nonce=$( echo "{\"date\":\"$currentTime\",\"uuid\":\"$(uuidgen)\"}" | base64 | tr '/+' '_-' | tr -d '=' )

curl "/auth/users" \
 -H "Content-Type: application/json" \
 -H "X-DFNS-NONCE: $nonce" \
 -H "X-DFNS-APPID: $DFNS_APP_ID" \
 -H "Authoriztion: Bearer $DFNS_API_KEY"
```
{% endcode %}
{% endtab %}
{% endtabs %}