# Policy Engine

`Policy Engine` allows our customers (and their customers in multi-tenancy mode) to add, rules, controls, and create policies out of them. Let's take the following example:

Clare, the customer's compliance officer, has to implement four new policies:

1. To notify the Managing Directors when the new employee is added.
2. To notify the senior management when payment above £50,000 is initiated.
3. To request approval from a Vice President and notify Managing Directors for payments over £100,000.
4. To request approval from a Vice President and a Managing Director for payments over £250,000.

To do that Clare will have to create \`\`Policy`Rules`:

* **Onboarded Employee**: `EmployeeAdded`, with the default configuration.
* **Medium Payment**: `PaymentAmountLimit` with amount value of 50,000 in GBP.
* **Large Payment**: `PaymentAmountLimit` with amount value of 100,000 inGBP.
* **Very Large Payment**: `PaymentAmountLimit` with amount value of 250,000 in GBP.

And following `Policy`Controls\`:

* Notify Vice Presidents: `NotifyOverEmail` scoped to VicePresident group or permission.
* Notify Managing Directors: `NotifyOverEmail` scoped to ManagingDirector group or permission.
* Vice President Approval: `RequestApproval` scoped to VicePresident group.
* Managing Director Approval: `RequestApproval` scoped to ManagingDirector group.

Finally, Clare will create Policies:

* New Employee Added `Policy` with the following
  * Rules: Onboarded Employee
  * Controls: Notify Managing Directors
* Medium Payment `Policy` with the following
  * Rules: Medium Payment
  * Controls: Notify Vice Presidents, Notify Managing Directors.
* Large Payment `Policy` with the following
  * Rules: Large Payment
  * Controls: Vice President Approval
* Very Large Payment `Policy` with the following
  * Rules: Very Large Payment
  * Controls: Vice President Approval, Managing Director Approval

It is important to note that when `Policy`Rules`,` Policy`Controls`, or `Policy` are immutable. When they are updated, the new `Policy` is created, and the previous `Policy` is marked as Archived. The specific `Policy` can be identified by a compound key containing its unique id and version. This way full audit log can be produced, with reference to the exact version of the `Policy` that was used.

## More about Rules

Dfns supports the following rule types:

* PaymentAmountLimit rule is triggered when payment exceeds a given limit. The amount can be specified in the following assets: USD, GBP, EUR, BTC, or ETH. Furthermore, the rule can be narrowed down either to a given User (employee or customer), or given wallets. By default, it is applied globally to all users and wallets belonging to the customer.
* PaymentAmountVelocity rule is triggered when the compound amount of multiple payments exceeds a given limit. The amount can be specified in the following assets: USD, GBP, EUR, BTC, or ETH. Furthermore, the rule can be narrowed down either to a given User (employee or customer), or given wallets. By default, it is applied globally to all users and wallets belonging to the customer.
  * `EmployeeAdded` rule is triggered when a new employee is added. This rule can be narrowed by specific permission.
  * `EmployeeUpdated` rule is triggered when employee details, such as name, email, contact data, or permissions are updated. This rule can be narrowed by specific permission.
  * `EmployeePermissionsUpdated` rule is triggered when employee permissions are updated.
  * `Policy`CreatedOrUpdated`rule is triggered when the`Policy\` is created or updated.
  * `Policy`RuleCreatedOrUpdated`rule is triggered when the`Policy\` rule is created or updated.
  * `Policy`ControlCreatedOrUpdated`rule is triggered when the`Policy\` control is created or updated.
