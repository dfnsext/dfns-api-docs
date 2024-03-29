
## CreateAssetAccount
`RESTful Endpoint: POST /assets/asset-accounts`

Creates new `AssetAccount` entity associated with a specific `assetSymbol` (such as `ETH`). Returns new asset ID.

{% hint style="info" %}
* Request headers required. See [Request Headers](../../../getting-started/request-headers.md "mention") for more information.
* Authentication required. See [Authentication Headers](../../../getting-started/request-headers.md#authentication-headers) for more information.
{% endhint %}

### Required Permissions

| Name                               | Conditions      |
| ---------------------------------- | --------------- |
| `AssetAccounts:CreateAssetAccount` | Always Required |

## Notes

1.  If `publicKey` is provided then `AssetAccount` will be added to the existing public-key (SigningGroup).    
    
2.  Error `groupThreshold/groupSize cannot be empty` happens if the default values of `3/7` for `groupThreshold` or `groupSize` respectively didn't get applied server-side. In the rare case that this happens, add those values to the request body in production (and `3/5` on testnets).  
    
3.  Error `parties is larger than the available number of peers` happens whenever you set `groupThreshold` or `groupSize` higher than the number of nodes provisioned by the system (`3/7` on production, `3/5` on testnets).        
    
4.  This operation is asynchronous. We create a record in the database with a `Creating` status and return a response with an asset account ID (starting with `aa-`). In the background, we generate a new public key. When this is done, the record in database is updated with additional information and the status is set to `Enabled`.  
    If it were synchronous, then the response would have to contain all the information about the created asset account, such as public key. This would mean a significant delay on the initial response, up to the key generation time (10, 15, even 30+ seconds).

5. Our MPC threshold signature protocol requires computationally heavy setup for [ECDSA](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm) key generation. With our current deployment, this process takes on average half a minute. If you anticipate a higher key generation throughput, please reach out to us.




<!--  -->

### Input Body Parameters
* assetSymbol: # [ENUM]

Asset symbol indicating which asset this account is managing. BTC or ETH are obvious examples, but there are thousands of possible symbols. In case of coins (ERC20 and alike) use `COIN.BLOCKCHAIN` syntax, such as USDC.ETH or USDC.SOL to indicate that USDC on Ethereum or USDC on Solana is required. To get a list of all allowed values, send a `CreateAssetAccount` request with the `assetSymbol` field empty.
* groupSize: 
* groupThreshold: 
* publicKey: `PublicKey` which is used by `AssetAccount`. Usually this is used to derive addresses on a given blockchain network.

Alternatively can be used to verify signatures produced by the platform.
* externalId: 
* tags: 
* name: Custom name that can be added for an account.

_Please consult OpenAPI file full breakdown and including nested properties._
### Successful Response
* tags: `Tag[]`. Multiple tags can be attached to an entity to categorise or otherwise mark it. For example tags could indicate risk (High, Medium, Low), departments (Trading, Sales, IT), purpose (Treasury, Hot, Deposits), and jurisdictions (US, EU, DE).

Multiple tags can be attached to same entity.
* externalId: `String`. Field can be used if entity is created in external (customer’s) system first. This way the external id can be attached to identify entity from Dfns’s data store.
* orgId: `EntityId`. Indicates id of the Organisation, such as usually a customer, or sub-devision, sub-tenant, and others.
* id: `EntityId`. 
* status: `AssetAccountStatus`. Indicates whether account is ready to be used.
* address: `String`. Blockchain address for a chosen Blockchain network.
* publicKey: `String`. `PublicKey` which is used by `AssetAccount`. Usually this is used to derive addresses on a given blockchain network.

Alternatively can be used to verify signatures produced by the platform.
* publicKeyId: `EntityId`. 
* assetSymbol: `AssetSymbol`. # [ENUM]

Asset symbol indicating which asset this account is managing. BTC or ETH are obvious examples, but there are thousands of possible symbols. In case of coins (ERC20 and alike) use `COIN.BLOCKCHAIN` syntax, such as USDC.ETH or USDC.SOL to indicate that USDC on Ethereum or USDC on Solana is required. To get a list of all allowed values, send a `CreateAssetAccount` request with the `assetSymbol` field empty.
* name: `String`. Custom name that can be added for an account.
* dateCreated: `IsoDatetime`. 
* dateUpdate: `IsoDatetime`. 
* groupSize: `Decimal`. 
* groupThreshold: `Decimal`. 
* authorizations: `AssetAccountAuthorization[]`.
### Error Responses
#### `404` **publicKeyNotFound** 
Unable to find `publicKey` provided in request body.
* serviceName: `String`. 
* message: `String`. 
* causes: `String[]`. 
* shouldTriggerInvestigaton: `Bool`. 
* isDfnsError: `Bool`. 
* httpStatus: `Integer`. 
* errorName: `String`. 

#### `400` **invalidConfiguration** 
Unable to create asset account entity with provided configuration
* serviceName: `String`. 
* message: `String`. 
* causes: `String[]`. 
* shouldTriggerInvestigaton: `Bool`. 
* isDfnsError: `Bool`. 
* httpStatus: `Integer`. 
* errorName: `String`. 

#### `402` **paymentRequired** 

* serviceName: `String`. 
* message: `String`. 
* causes: `String[]`. 
* shouldTriggerInvestigaton: `Bool`. 
* isDfnsError: `Bool`. 
* httpStatus: `Integer`. 
* errorName: `String`.


