# Broadcast Transaction

`POST /public-keys/transactions`

Broadcast transaction enables communication with any arbitrary smart contract by replicating the native transaction protocol fields in the body of the request.   It can be used to make native payments, call smart contract functions, and even deploy new smart contracts.  Note for reading from a "view" function on EVM chains, please use [Call Read Function](../../../blockchains/call-read-function.md).&#x20;

Currently, only EVM compatible chains are supported. We plan to add additional chain support in the future. Please don't hesitate to contact us if you need support for a non-EVM chain.&#x20;

### Required Permissions

Transactions:Create

### Request body <a href="#request-body" id="request-body"></a>

The following fields are common to all `templateKinds:`

| Request body fields | Required/Optional | Description                                                                                                                                                               | Type            |
| ------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| `publicKeyId`       | Required          | <p>Unique identifier of the <code>PublicKey</code> like:<br><br><code>pk-orange-magnesium-a0606d08b2</code></p>                                                           | String          |
| `network`           | Required          | Enumerated type representing the Blockchain network from the list found [here](https://dfns.gitbook.io/dfns-docs/api-docs/dfns-api-enumerated-types#network).             | Enumerated Type |
| `templateKind`      | Required          | Enumerated type representing the Blockchain transaction template that dictates the remaining acceptable fields.  Currently, the only supported value is "`EvmGenericTx`". | Enumerated Type |

For details on specific templateKinds, please see the chain specific sub pages underneath this article in the left hand navigation.&#x20;

### Request example <a href="#request-example.1" id="request-example.1"></a>

#### Sample request using EvmGenericTx <a href="#sample-request" id="sample-request"></a>

```shell
curl -X POST "/public-keys/transactions" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <TOKEN>" \
-d '{
    "publicKeyId": "pk-orange-magnesium-a0606d08b2",
    "network": "ETH",
    "templateKind": "EvmGenericTx",
    "data": "0x368b87720000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000b48656c6c6f204d616a6964000000000000000000000000000000000000000000",
    "to": "0xeE1C5C88026AA51c653155276dE578d7c02aDB0c"
}'
```

### Response <a href="#response" id="response"></a>

#### Response example <a href="#response-example" id="response-example"></a>

Status begins as `Initiated` and changes to `Executed` once broadcast to the mempool.  Use [GetTransactionById](../gettransactionbyid.md) to query for updated status and to retrieve a blockchain transaction hash.

```json
{
    "transaction": {
        "publicKeyId": "pk-shade-wisconsin-c28c38b2e8",
        "network": "ETH",
        "templateKind": "EvmGenericTx",
        "data": "0x095ea7b3000000000000000000000000bebc44782c7db0a1a60cb6fe97d0b483032ff1c7ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "to": "0xbEbc44782C7dB0a1A60Cb6fe97d0b483032FF1C7",
        "gasLimit": "100000000"
    },
    "snapshot": "{\"publicKeyId\":\"pk-shade-wisconsin-c28c38b2e8\",\"network\":\"ETH\",\"templateKind\":\"EvmGenericTx\",\"data\":\"0x095ea7b3000000000000000000000000bebc44782c7db0a1a60cb6fe97d0b483032ff1c7ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff\",\"to\":\"0xbEbc44782C7dB0a1A60Cb6fe97d0b483032FF1C7\",\"gasLimit\":\"100000000\"}",
    "dateUpdated": "2022-10-31T19:10:02.228Z",
    "initiator": {
        "kind": "Employee",
        "employeeId": "oe-nine-artist-9de60fef6963",
        "orgId": "cu-purple-pip-1b417b958500"
    },
    "orgId": "cu-purple-pip-1b417b958500",
    "publicKeyId": "pk-shade-wisconsin-c28c38b2e8",
    "network": "ETH",
    "status": "Initiated",
    "id": "tx-sierra-lima-272e2ce093",
    "dateCreated": "2022-10-31T19:10:02.229Z"
}
```