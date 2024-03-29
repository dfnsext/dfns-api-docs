# Update Policy

`PUT /v2/policies/{policyId}`

Updates a policy.

{% hint style="info" %}
* User action signature required. See [User Action Signing](../../authentication/user-action-signing/) for more information.
* Request headers required. See [Request Headers](../../../getting-started/request-headers.md) for more information.
* Authentication required. See [Authentication Headers](../../../getting-started/request-headers.md#authentication-headers) for more information.
{% endhint %}

## Required Permissions

| Name              | Conditions      |
| ----------------- | --------------- |
| `Policies:Update` | Always Required |

## Parameters <a href="#parameters.1" id="parameters.1"></a>

### Path parameters <a href="#path-parameters" id="path-parameters"></a>

<table><thead><tr><th width="248">Path parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>policyId</code></td><td>Unique identifier of the policy</td></tr></tbody></table>



## Request body <a href="#request-body" id="request-body"></a>

<table><thead><tr><th width="217">Request body fields</th><th width="113">Required/Optional</th><th>Description</th><th>Type</th></tr></thead><tbody><tr><td><code>name</code></td><td>Required</td><td>A name for the Policy.</td><td>String</td></tr><tr><td><code>activityKind</code></td><td>Required</td><td>Determines which actions on the API may trigger an Approval. See supported values above.</td><td>Enumerated Type</td></tr><tr><td><code>rule</code></td><td>Required</td><td>Conditions that will be evaluated for relevant activity.</td><td>Object</td></tr><tr><td><code>approvalGroups</code></td><td>Required</td><td>The users that will be allowed to approve an activity.</td><td>List of objects</td></tr><tr><td><code>filters</code></td><td>Optional</td><td>Specify a list of entities to scope the policy to (eg. wallets).</td><td>Object</td></tr><tr><td><code>autoRejectTimeout</code></td><td>Optional</td><td>Time (in minutes) after which an approval will automatically be rejected.</td><td>Positive Integer</td></tr></tbody></table>

### Rule Object (see [rules](create-policy/rules/))

<table><thead><tr><th width="199">Request body fields</th><th width="185">Required/Optional</th><th width="218">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>kind</code></td><td>Required</td><td>The kind of rule that will be specified.</td><td>Enumerated Type</td></tr><tr><td><code>configuration</code></td><td>Required/Optional</td><td>Details specific to the rule kind.</td><td>Object</td></tr></tbody></table>

### Approval Groups Object (see [approval groups](create-policy/approval-groups.md))

<table><thead><tr><th width="254">Request body fields</th><th width="113">Required/Optional</th><th width="218">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>name</code></td><td>Optional</td><td>Name of the approval group.</td><td>String</td></tr><tr><td><code>quorum</code></td><td>Required</td><td>Quorum required for approval of activity.</td><td>Positive Integer</td></tr><tr><td><code>approvers</code></td><td>Optional</td><td>Finer-grained approval group configuration.</td><td>Object</td></tr></tbody></table>

### Filter Object (see [filters](create-policy/filters.md))

<table><thead><tr><th width="254">Request body fields</th><th width="113">Required/Optional</th><th width="218">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>id</code></td><td>Optional</td><td>Apply policy only to entities with specified ID.</td><td>Object</td></tr></tbody></table>

### Request Example <a href="#request-example.1" id="request-example.1"></a>

```json
{
  "name": "Transfer Limit",
  "activityKind": "Wallets:Sign",
  "rule": {
    "kind": "TransactionAmountLimit",
    "configuration": {
      "currency": "EUR",
      "limit": "1000",
    },
  },
  "approvalGroups": [
    {
      "name": "Admins",
      "quorum": 1,
      "approvers": {
        "userId": {
          "oneOf": ["us-..."],
        },
      },
    },
  ],
  "filters": {
    "id": {
      "in": ["wa-..."],
    }
  },
  "autoRejectTimeout": 60,
}
```

## Response <a href="#response" id="response"></a>

### Response example 200 - no approval required <a href="#response-example" id="response-example"></a>

<pre class="language-json"><code class="lang-json"><strong>{
</strong><strong>  "id": "plc-...",
</strong>  "name": "Transfer Limit",
  "rule": {
    "kind": "TransactionAmountLimit",
    "configuration": {
      "currency": "EUR",
      "limit": "1000",
    },
  },
  "status": "Active",
  "filters": {
    "id": {
      "oneOf": ["wa-..."]
    }
  },
  "activityKind": "Wallets:Sign",
  "approvalGroups": [
    {
      "name": "Admins",
      "quorum": 1,
      "approvers": {
        "userId": {
          "oneOf": ["us-..."],
        },
      },
    }
  ],
  "autoRejectTimeout": 60
}
</code></pre>

### Response example 202 - approval required <a href="#response-example" id="response-example"></a>

```json
{
  "id": "cr-...",
  "orgId": "or-...",
  "requester": {
    "appId": "ap-...",
    "userId": "us-...",
    "tokenId": "to-..."
  },
    "kind": "Policy",
    "operationKind": "Update",
    "status": "Pending",
    "entityId": "plc-...",
    "body": {
        "id": "plc-...",
        "name": "Transfer Limit",
        "rule": {
          "kind": "TransactionAmountLimit",
          "configuration": {
            "currency": "EUR",
            "limit": "1000",
          },
        },
        "status": "Active",
        "filters": {
          "id": {
            "oneOf": ["wa-..."]
          }
        },
        "activityKind": "Wallets:Sign",
        "approvalGroups": [
            {
              "name": "Admins",
              "quorum": 1,
              "approvers": {
                "userId": {
                  "oneOf": ["us-..."],
                },
              },
           }
        ],
        "autoRejectTimeout": 60
  },
  "dateCreated": "2023-12-22T20:57:55.814Z",
  "dateResolved": "2023-12-22T20:57:55.814Z"
}
```
