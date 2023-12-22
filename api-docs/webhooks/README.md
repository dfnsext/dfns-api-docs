---
description: Listen for events so you can automatically trigger reactions.
---

# Webhooks

When integrating with Dfns, you might want your applications to receive events as they occur in your Dfns account, so that your backend systems can execute actions accordingly.

To start being notified about Webhook Events, you first need to register webhooks. After you register them, Dfns can push real-time event data to your application’s webhook endpoint when events happen in your Dfns account. Dfns uses a `POST` http/https request to send webhook events to your app, as a JSON payload which includes a [Webhook Event Object](get-webhook-event.md#response).

Receiving webhook events are particularly useful for listening to asynchronous events, such as doing a wallet transfer request.



## Webhook Events

When an event happen in the system, which a webhook subscribed to, we build a Webhook Event with the following shape, containing some data around the event that happened. This is an example of a transfer request event payload delivered:

```json
{
  "id": "wh-xxx-xxxxxxx",
  "kind": "wallet.transfer.requested",
  "date": "2023-12-04T10:02:22.280Z",
  "data": {
    "transferRequest": {
      "id": "xfr-1vs8g-c1ub1-xxxxxxxxxxxxxxxx",
      "walletId": "wa-39abb-e9kpk-xxxxxxxxxxxxxxxx",
      "network": "EthereumSepolia",
      "requester": {
        "userId": "us-3v1ag-v6b36-xxxxxxxxxxxxxxxx",
        "tokenId": "to-7mkkj-c831n-xxxxxxxxxxxxxxxx",
        "appId": "ap-24vva-92s32-xxxxxxxxxxxxxxxx"
       },
      "requestBody": {
        "kind": "Native",
        "to": "0xb282dc7cde21717f18337a596e91ded00b79b25f",
        "amount": "1000000000"
      },
      "dateRequested": "2023-05-08T19:14:25.568Z",
      "status": "Pending"
    }
  },
  "status": "200",
  "timestampSent": 1701684144,
}
```

#### Supported Webhook Events

Currently, here are the event kinds which webhooks can subscribe to ⬇️

```
wallet.created
wallet.exported
wallet.delegated
wallet.signature.requested
wallet.signature.failed
wallet.signature.rejected
wallet.signature.signed
wallet.transaction.requested
wallet.transaction.failed
wallet.transaction.rejected
wallet.transaction.broadcasted
wallet.transaction.confirmed
wallet.transfer.requested
wallet.transfer.failed
wallet.transfer.rejected
wallet.transfer.broadcasted
wallet.transfer.confirmed
wallet.blockchainevent.detected
```

#### Event Data

Depending on its kind, every event holds `data` that corresponds to this kind. Here's an overview of what kind of `data` each event kind

* For `wallet.created`, `wallet.exported`, `wallet.delegated`:

{% code title="data" %}
```json
{ // Wallet object, as in "Create Wallet" endpoint response
  "wallet": {      
    "id": "wa-xxx-xxxxxxxxx",
    ...
  }
}
```
{% endcode %}

* For `wallet.transfer.requested`, `wallet.transfer.failed`, `wallet.transfer.rejected`, `wallet.transfer.broadcasted`, `wallet.transfer.confirmed`:

{% code title="data:" %}
```json
{ // Wallet Transfer Request object as in "Wallet Send Transfer" endpoint
  "transferRequest": {
    "id": "xfr-xxx-xxxxxxxxx",
    "walletId": "wa-xxx-xxxxxxxx",
    ...
  }
}
```
{% endcode %}

* For `wallet.transaction.requested`, `wallet.transaction.failed`, `wallet.transaction.rejected`, `wallet.transaction.broadcasted`, `wallet.transaction.confirmed`:

{% code title="data" %}
```json
{ // Wallet Transaction Request as in "Wallet Broadcast Transaction" endpoint
  "transactionRequest": {
    "id": "tx-xxx-xxxxxxxxx",
    "walletId": "wa-xxx-xxxxxxxx",
    ...
  }
}
```
{% endcode %}

* For `wallet.signature.requested`, `wallet.signature.failed`, `wallet.signature.rejected`, `wallet.signature.signed`:

{% code title="data" %}
```json
{ // Wallet Signature Request object as in "Wallet Generate Signature" endpoint
  "signatureRequest": {
    "id": "sig-xxx-xxxxxxxxx",
    "walletId": "wa-xxx-xxxxxxxx",
    ...
  }
}
```
{% endcode %}

* For `wallet.blockchainevent.detected`:

{% code title="data" %}
```json
{ // Blockchain Event object as in "Wallet Get Wallet History" endpoint
  "kind": "Erc20Transfer",
  "contract": "0x......",
  "from": "0x......",
  "to": "0x......",
  ...
}
```
{% endcode %}



#### Webhook Event Ordering <a href="#best-practices" id="best-practices"></a>

Dfns doesn’t guarantee delivery of events in the order in which they’re generated. For example, when a wallet [Transfer](../wallets/transfer-asset-from-wallet.md) is picked up on-chain by our blockchain indexers, we might generate the following events:

* `wallet.transfer.confirmed` - this event notifies you that the [Transfer Request](../wallets/transfer-asset-from-wallet.md) that you made has been confirmed on chain
* `wallet.blockchainevent.detected`- this event notifies you of the new Blockchain Event detected and added to your [Wallet History](../wallets/get-wallet-history.md) blockchain events

Your endpoint shouldn’t expect delivery of these events in this order, and needs to handle delivery accordingly.



#### Webhook Event Delivery & Retries

As of now, if an event fails to be properly delivered to a webhook, we will not retry delivering it. That means that if your http server is not setup properly, of for some reason fails to properly receive an event, we won't retry to send the event.

It is in our plans to add a retry mechanism, though please be aware that this is not implemented yet.



## Webhooks best practices <a href="#best-practices" id="best-practices"></a>

Review these best practices to make sure your webhooks remain secure and function well.

#### Verify events are sent from Dfns <a href="#verify-events" id="verify-events"></a>

Verify webhook signatures to confirm that received events are sent from Dfns. Dfns signs webhook events it sends to your endpoints by including a signature in each event’s `X-DFNS-WEBHOOK-SIGNATURE` header. This allows you to verify that the events were sent by Dfns, not by a third party.&#x20;

Dfns signatures is a [HMAC](https://en.wikipedia.org/wiki/Hash-based\_message\_authentication\_code) of the received event payload, using [SHA-256](https://en.wikipedia.org/wiki/SHA-2) hash function and the webhook secret as the secret. It has this shape:

```
X-DFNS-WEBHOOK-SIGNATURE: sha256=33008aa9673b764cc752362034dfe49ef466315c45d62b3e8cb8588b23d0d06a
```

Here is an example function showing how you can validate the webhook event signature:

{% tabs %}
{% tab title="NodeJS" %}
```javascript
const crypto = require('crypto')

const WEBHOOK_SECRET = process.env.WEBHOOK_SECRET // the webhook secret you got upon webhook creation
const REPLAY_ATTACK_TOLERANCE = 5 * 60 // 5 minutes

function verifyDfnsWebhookSignature(eventPayload, eventSignature) {
  const messageToSign = JSON.stringify(eventPayload) // this assumes "eventPayload" was already JSON-parsed, and is an object (the full payload of the webhook event)

  const signature = crypto
    .createHmac('sha256', WEBHOOK_SECRET)
    .update(messageToSign)
    .digest('hex')

  const trustedSig = Buffer.from(`sha256=${signature}`, 'ascii')
  const untrustedSig = Buffer.from(eventSignature, 'ascii')

  const isSignatureValid = crypto.timingSafeEqual(trustedSig, untrustedSig) // using a constant-time equality comparison (to avoid timing attacks)

  const now = new Date().getTime() / 1000 // your server unix timestamp
  const isTimestampWithinTolerance = Math.abs(now - eventPayload.timestampSent) < REPLAY_ATTACK_TOLERANCE

  return isSignatureValid && isTimestampWithinTolerance
}
```
{% endtab %}
{% endtabs %}

#### Only listen to event types your integration requires <a href="#only-listen-to-event-types-your-integration-requires" id="only-listen-to-event-types-your-integration-requires"></a>

Configure your webhook endpoints to receive only the types of events required by your integration. Listening for extra events (or all events) puts undue strain on the server and we don’t recommend it.

#### Handle duplicate events <a href="#handle-duplicate-events" id="handle-duplicate-events"></a>

Webhook endpoints might occasionally receive the same event more than once. You can guard against duplicated event receipts by making sure your your event processing is idempotent.

#### Receive events with an HTTPS server <a href="#receive-events-with-an-https-server" id="receive-events-with-an-https-server"></a>

If you use an HTTPS URL for your webhook, we validate that the connection to your server is secure before sending your webhook data. For this to work, your server must be correctly configured to support HTTPS with a valid server certificate.

#### Exempt webhook route from CSRF protection <a href="#csrf-protection" id="csrf-protection"></a>

If you’re using Rails, Django, or another web framework, your site might automatically check that every POST request contains a _CSRF token_. This is an important security feature that helps protect you and your users from [cross-site request forgery](https://www.owasp.org/index.php/Cross-Site\_Request\_Forgery\_\(CSRF\)) attempts. However, this security measure might also prevent your site from processing legitimate events. If so, you might need to exempt the webhooks route from CSRF protection.

{% tabs %}
{% tab title="Rails" %}
```ruby
class DfnsController < ApplicationController
  # If your controller accepts requests other than webhooks,
  # you'll probably want to use `protect_from_forgery` to add CSRF
  # protection for your application. But don't forget to exempt
  # your webhook route!
  protect_from_forgery except: :webhook

  def webhook
    # Process webhook data in `params`
  end
end
```
{% endtab %}

{% tab title="Django" %}
```python
import json

# Webhooks are always sent as HTTP POST requests, so ensure
# that only POST requests reach your webhook view by
# decorating `webhook()` with `require_POST`.
#
# To ensure that the webhook view can receive webhooks,
# also decorate `webhook()` with `csrf_exempt`.
@require_POST
@csrf_exempt
def webhook(request):
  # Process webhook data in `request.body`
```
{% endtab %}
{% endtabs %}



## Local Development

To add a new webhook, you first need a http server which can receive requests from public internet.&#x20;

During development, one way to achieve this (without deploying a new server on a cloud provider), is to spin up a local server on your machine (localhost), and then use a tunnel services (eg [https://ngrok.com](https://ngrok.com/)) to create a public url pointing to your local server.

As an example, here are steps to create a basic Express server in **NodeJS:**

* Create a new npm project, install express

```
mkdir basic-server && cd basic-server
npm init
npm install express
```

* Add a new file `index.js` :

```javascript
const express = require('express')

const app = express()
const port = 3000

app.use(express.json())

app.post('/', (req) => {
  console.log('Received event:', req.body)
})

app.listen(port, () => {
  console.log(`Listening on port ${port}`)
})
```

* In one terminal, run your server

```
node index.js
```

* In another terminal, start a [ngrok](https://ngrok.com/docs/getting-started/) tunnel pointing to your local server

```
ngrok http 3000
```

* Now, you can [Create a Webhook](create-webhook.md) using the url displayed in the result of above the terminal (looking like "`https://xxxxxx.ngrok-free.dev`"), and test that the webhook is setup properly by using [Ping Webhook](ping-webhook.md). If properly setup, you should see incoming events received by your local server.

{% hint style="warning" %}
If you use a free Ngrok account, every time you re-launch the tunnel you'll get a new url, so make sure you update the Dfns webhook url to test.
{% endhint %}


