# Policy Engine

Policies enable businesses to enforce rules and request approvals on top of actions taken using the Dfns API.  Policies are used as part of risk management, information security, or other compliance functions.&#x20;

The policy Engine allows you to create a policy, specifying the conditions that will result in an approval being triggered, as well as the approval groups whose approval will be required.  For example:

Clare, a compliance officer, has to implement these new policies:

1. For payments over $100,000, request approval from a Vice President.
2. For payments over $250,000, request approval from both a Vice President and a Managing Director.

To do that Clare will have to create two `Policies`:

* **Large Payment**:&#x20;
  * Rule: `TransactionAmountLimit` with amount value of $100,000.
  * Approval scoped to VicePresidents.
* **Very Large Payment**:
  * Rule: `TransactionAmountLimit` with amount value of $250,000.
  * Approval scoped to ManagingDirectors.

When a policy is triggered, it generates and approval which must be either approved or rejected by members of the corresponding approval group.  Here's a schematic of the Policy Engine entity model:&#x20;

<figure><img src="../../.gitbook/assets/our policy engine diagram.png" alt=""><figcaption><p>Policy Engine Schematic</p></figcaption></figure>

For questions on the Policy Engine as well as feature requests, please email [docs@dfns.co](mailto:docs@dfns.co).&#x20;

{% hint style="warning" %}
Policy engine has recently been updated to simplify the model. Until the old policy engine is removed, the following logic will be applied to asset transfers from wallets:

* The new policy engine will be triggered only if:
  * No relevant policies from the old policy engine exist.
  * No policies from the old policy engine are triggered.
* If a policy from the new engine is triggered, then the new approval flow will be started. Otherwise, the old approval flow will be triggered.
{% endhint %}

