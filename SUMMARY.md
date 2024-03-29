# Table of contents

* [👋 Welcome](README.md)

## Getting Started

* [Onboarding to Dfns](getting-started/onboarding-to-dfns.md)
* [Dfns Environments](getting-started/dfns-environments.md)
* [Data Model Concepts](getting-started/DataModelConcepts.md)
* [Postman](getting-started/postman-integration.md)
* [Typescript SDK](getting-started/typescript-sdk.md)
* [Videos](getting-started/Videos.md)

## API Docs

* [Introduction](api-docs/README.md)
* [Authentication](api-docs/authentication/README.md)
  * [Delegated Authentication](api-docs/authentication/delegated-auth/README.md)
    * [Delegated Registration](api-docs/authentication/delegated-auth/delegatedregistration.md)
    * [Delegated Registration Restart](api-docs/authentication/delegated-auth/delegatedregistration-1.md)
    * [Delegated Login](api-docs/authentication/delegated-auth/delegatedlogin.md)
  * [User Action Signing](api-docs/authentication/user-action-signing/README.md)
    * [Create User Action Signature Challenge](api-docs/authentication/user-action-signing/initUserActionSigning.md)
    * [Create User Action Signature](api-docs/authentication/user-action-signing/completeUserActionSigning.md)
  * [Registration](api-docs/authentication/registration/README.md)
    * [Create User Registration Challenge](api-docs/authentication/registration/initUserRegistration.md)
    * [Complete User Registration](api-docs/authentication/registration/completeUserRegistration.md)
    * [Resend Registration Email](api-docs/authentication/registration/resendRegistrationEmail.md)
  * [Login](api-docs/authentication/login/README.md)
    * [Create User Login Challenge](api-docs/authentication/login/initlogin.md)
    * [Complete User Login](api-docs/authentication/login/completeLogin.md)
  * [Users](api-docs/authentication/user-management/README.md)
    * [List Users](api-docs/authentication/user-management/listUsers.md)
    * [Create User](api-docs/authentication/user-management/createUser.md)
    * [Get User](api-docs/authentication/user-management/getUser.md)
    * [Update User](api-docs/authentication/user-management/updateUser.md)
    * [Activate User](api-docs/authentication/user-management/activateUser.md)
    * [Deactivate User](api-docs/authentication/user-management/deactivateUser.md)
    * [Archive User](api-docs/authentication/user-management/archiveUser.md)
  * [Service Accounts](api-docs/authentication/service-account-management/README.md)
    * [List Service Accounts](api-docs/authentication/service-account-management/listServiceAccounts.md)
    * [Create Service Account](api-docs/authentication/service-account-management/createServiceAccount.md)
    * [Get Service Account](api-docs/authentication/service-account-management/getServiceAccount.md)
    * [Update Service Account](api-docs/authentication/service-account-management/updateServiceAccount.md)
    * [Activate Service Account](api-docs/authentication/service-account-management/activateServiceAccount.md)
    * [Deactivate Service Account](api-docs/authentication/service-account-management/deactivateServiceAccount.md)
    * [Archive Service Account](api-docs/authentication/service-account-management/archiveServiceAccount.md)
  * [Applications](api-docs/authentication/application-management/README.md)
    * [List Applications](api-docs/authentication/application-management/listApplications.md)
    * [Create Application](api-docs/authentication/application-management/createClientSideApplication.md)
    * [Create Server-Signed Application](api-docs/authentication/application-management/createServerSideApplication.md)
    * [Get Application](api-docs/authentication/application-management/getApplication.md)
    * [Update Application](api-docs/authentication/application-management/updateApplication.md)
    * [Activate Application](api-docs/authentication/application-management/activateApplication.md)
    * [Deactivate Application](api-docs/authentication/application-management/deactivateApplication.md)
    * [Archive Application](api-docs/authentication/application-management/archiveApplication.md)
  * [Personal Access Tokens](api-docs/authentication/personal-access-token-management/README.md)
    * [List Personal Access Tokens](api-docs/authentication/personal-access-token-management/listPersonalAccessTokens.md)
    * [Create Personal Access Token](api-docs/authentication/personal-access-token-management/createPersonalAccessToken.md)
    * [Get Personal Access Token](api-docs/authentication/personal-access-token-management/getPersonalAccessToken.md)
    * [Update Personal Access Token](api-docs/authentication/personal-access-token-management/updatePersonalAccessToken.md)
    * [Activate Personal Access Token](api-docs/authentication/personal-access-token-management/activatePersonalAccessToken.md)
    * [Deactivate Personal Access Token](api-docs/authentication/personal-access-token-management/deactivatePersonalAccessToken.md)
    * [Archive Personal Access Token](api-docs/authentication/personal-access-token-management/archivePersonalAccessToken.md)
  * [Credentials](api-docs/authentication/credential-management/README.md)
    * [Create User Credential Challenge](api-docs/authentication/credential-management/createUserCredentialChallenge.md)
    * [Create User Credential](api-docs/authentication/credential-management/createUserCredential.md)
    * [Activate User Credential](api-docs/authentication/credential-management/activateCredential.md)
    * [Deactivate User Credential](api-docs/authentication/credential-management/deactivateCredential.md)
    * [List User Credentials](api-docs/authentication/credential-management/listUserCredentials.md)
  * [User Recovery](api-docs/authentication/user-recovery/README.md)
    * [Send User Recovery Verification Email](api-docs/authentication/user-recovery/createUserRecoveryCode.md)
    * [Create User Recovery Challenge](api-docs/authentication/user-recovery/createUserRecoveryChallenge.md)
    * [Recover User](api-docs/authentication/user-recovery/createUserRecovery.md)
    * [Delegated User Recovery](api-docs/authentication/user-recovery/delegatedrecovery.md)
* [Wallets](api-docs/wallets/README.md)
  * [Create Wallet](api-docs/wallets/create-wallet/README.md)
  * [Delegate Wallet](api-docs/wallets/delegate-wallet.md)
  * [Get Wallet by ID](api-docs/wallets/get-wallet-by-id.md)
  * [List Wallets](api-docs/wallets/list-wallets.md)
  * [Get Wallet Assets](api-docs/wallets/get-wallet-assets.md)
  * [Get Wallet NFTs](api-docs/wallets/get-wallet-nfts.md)
  * [Get Wallet History](api-docs/wallets/get-wallet-history.md)
  * [Transfer Asset from Wallet](api-docs/wallets/transfer-asset-from-wallet.md)
  * [Get Wallet Transfer Request by ID](api-docs/wallets/get-wallet-transfer-request-by-id.md)
  * [List Wallet Transfer Requests](api-docs/wallets/list-wallet-transfer-requests.md)
  * [Broadcast Transaction from Wallet](api-docs/wallets/broadcast-transaction-from-wallet.md)
    * [Algorand: Broadcast Transaction](api-docs/wallets/broadcast-transaction-from-wallet/algorand-broadcast-transaction.md)
    * [Bitcoin/Litecoin: Broadcast Transaction](api-docs/wallets/broadcast-transaction-from-wallet/bitcoin-broadcast-transaction.md)
    * [EVM: Broadcast Transaction](api-docs/wallets/broadcast-transaction-from-wallet/evm-broadcast-transaction.md)
    * [Solana: Broadcast Transaction](api-docs/wallets/broadcast-transaction-from-wallet/solana-broadcast-transaction.md)
    * [Tezos: Broadcast Transaction](api-docs/wallets/broadcast-transaction-from-wallet/tezos-broadcast-transaction.md)
    * [Tron: Broadcast Transaction](api-docs/wallets/broadcast-transaction-from-wallet/tron-broadcast-transaction.md)
    * [XRPLedger (aka Ripple): Broadcast Transaction](api-docs/wallets/broadcast-transaction-from-wallet/xrpledger-aka-ripple-broadcast-transaction.md)
  * [Get Wallet Transaction Request by ID](api-docs/wallets/get-wallet-transaction-request-by-id.md)
  * [List Wallet Transaction Requests](api-docs/wallets/list-wallet-transaction-requests.md)
  * [Generate Signature from Wallet](api-docs/wallets/generate-signature-from-wallet/README.md)
    * [Algorand: Generate Signature](api-docs/wallets/generate-signature-from-wallet/algorand-generate-signature.md)
    * [Bitcoin/Litecoin: Generate Signature](api-docs/wallets/generate-signature-from-wallet/bitcoin-generate-signature.md)
    * [EVM: Generate Signature](api-docs/wallets/generate-signature-from-wallet/evm-generate-signature.md)
    * [Solana: Generate Signature](api-docs/wallets/generate-signature-from-wallet/solana-generate-signature.md)
    * [Tezos: Generate Signature](api-docs/wallets/generate-signature-from-wallet/tezos-generate-signature.md)
    * [Tron: Generate Signature](api-docs/wallets/generate-signature-from-wallet/tron-generate-signature.md)
    * [XRPLedger (aka Ripple): Generate Signature](api-docs/wallets/generate-signature-from-wallet/xrpledger-aka-ripple-generate-signature.md)
    * [Pseudo Networks (All other chains): Generate Signature](api-docs/wallets/generate-signature-from-wallet/pseudo-networks-all-other-chains-generate-signature.md)
  * [Get Wallet Signature Request by ID](api-docs/wallets/get-wallet-signature-request-by-id.md)
  * [List Wallet Signature Requests](api-docs/wallets/list-wallet-signature-requests.md)
  * [Advanced Wallet APIs](api-docs/wallets/advanced-wallet-apis/README.md)
    * [Wallet Import](api-docs/wallets/advanced-wallet-apis/wallet-import.md)
    * [Export Wallet](api-docs/wallets/advanced-wallet-apis/export-wallet.md)
* [Networks](api-docs/networks/README.md)
  * [Estimate fees](api-docs/networks/estimate-fees.md)
  * [Read Contract](api-docs/networks/read-contract.md)
* [Policy Engine](api-docs/policy-engine/README.md)
  * [Policies](api-docs/policy-engine/policies/README.md)
    * [Create Policy](api-docs/policy-engine/policies/create-policy/README.md)
      * [Rules](api-docs/policy-engine/policies/create-policy/rules/README.md)
        * [AlwaysRequireApproval](api-docs/policy-engine/policies/create-policy/rules/alwaysrequireapproval.md)
        * [TransactionAmountLimit](api-docs/policy-engine/policies/create-policy/rules/transactionamountlimit.md)
        * [TransactionAmountVelocity](api-docs/policy-engine/policies/create-policy/rules/transactionamountvelocity.md)
        * [TransactionCountVelocity](api-docs/policy-engine/policies/create-policy/rules/transactioncountvelocity.md)
      * [Approval Groups](api-docs/policy-engine/policies/create-policy/approval-groups.md)
      * [Filters](api-docs/policy-engine/policies/create-policy/filters.md)
    * [Update Policy](api-docs/policy-engine/policies/update-policy.md)
    * [Archive Policy](api-docs/policy-engine/policies/archive-policy.md)
    * [Get Policy](api-docs/policy-engine/policies/get-policy.md)
    * [List Policies](api-docs/policy-engine/policies/list-policies.md)
  * [Approvals](api-docs/policy-engine/approvals/README.md)
    * [Create Approval Decision](api-docs/policy-engine/approvals/create-approval-decision.md)
    * [List Approvals](api-docs/policy-engine/approvals/list-approvals.md)
* [Permissions](api-docs/permissions/README.md)
  * [Permissions Overview](api-docs/permissions/permissions-overview.md)
  * [API Reference](api-docs/permissions/permissions/README.md)
    * [Get Permission](api-docs/permissions/permissions/getpermissionbyid.md)
    * [List Permissions](api-docs/permissions/permissions/listpermissions.md)
    * [Create Permission](api-docs/permissions/permissions/createpermission.md)
    * [Update Permission](api-docs/permissions/permissions/updatepermission.md)
    * [Archive Permission](api-docs/permissions/permissions/archivepermission.md)
    * [Assign Permission](api-docs/permissions/permissions/createassignment.md)
    * [Revoke Permission](api-docs/permissions/permissions/revokeassignment.md)
    * [List Permission Assignments](api-docs/permissions/permissions/listassignments.md)
* [Webhooks](api-docs/webhooks/README.md)
  * [Create Webhook](api-docs/webhooks/create-webhook.md)
  * [Get Webhook](api-docs/webhooks/get-webhook.md)
  * [List Webhooks](api-docs/webhooks/list-webhooks.md)
  * [Update Webhook](api-docs/webhooks/update-webhook.md)
  * [Delete Webhook](api-docs/webhooks/delete-webhook.md)
  * [Ping Webhook](api-docs/webhooks/ping-webhook.md)
  * [Get Webhook Event](api-docs/webhooks/get-webhook-event.md)
  * [List Webhook Events](api-docs/webhooks/list-webhook-events.md)
* [Dfns Change Log](api-docs/dfns-change-log.md)
* [API Errors](getting-started/errors.md)
* [Deprecated APIs](api-docs/deprecated-apis/README.md)
  * [Deprecated - Asset Accounts & Payments](api-docs/high-level-api-asset-accounts-and-payments/README.md)
    * [Asset Accounts](api-docs/deprecated-apis/high-level-api-asset-accounts-and-payments/asset-accounts/README.md)
      * [Create Asset Account](api-docs/high-level-api-asset-accounts-and-payments/asset-accounts/createassetaccount.md)
      * [Get Asset Account By ID](api-docs/deprecated-apis/high-level-api-asset-accounts-and-payments/asset-accounts/getassetaccountbyid.md)
      * [List Asset Accounts](api-docs/high-level-api-asset-accounts-and-payments/asset-accounts/listassetaccounts.md)
      * [Get Balance](api-docs/high-level-api-asset-accounts-and-payments/asset-accounts/getassetaccountbalancebyid.md)
    * [Payments](api-docs/deprecated-apis/high-level-api-asset-accounts-and-payments/payments/README.md)
      * [Initiate Payment](api-docs/deprecated-apis/high-level-api-asset-accounts-and-payments/payments/initiatepayment.md)
      * [Get Payment By ID](api-docs/deprecated-apis/high-level-api-asset-accounts-and-payments/payments/getpaymentbyid.md)
      * [List Payments](api-docs/deprecated-apis/high-level-api-asset-accounts-and-payments/payments/listpayments.md)
    * [Deprecated - Dfns API Enumerated Types](api-docs/deprecated-apis/high-level-api-asset-accounts-and-payments/dfns-api-enumerated-types.md)
  * [Deprecated - Keys & Transactions](api-docs/deprecated-apis/low-level-api-keys-and-transactions/README.md)
    * [Public Keys](api-docs/deprecated-apis/low-level-api-keys-and-transactions/public-keys-1/README.md)
      * [Create Public Key](api-docs/deprecated-apis/low-level-api-keys-and-transactions/public-keys-1/createpublickey.md)
      * [Get Public Key By ID](api-docs/deprecated-apis/low-level-api-keys-and-transactions/public-keys-1/getpublickeybyid.md)
      * [List Public Keys](api-docs/deprecated-apis/low-level-api-keys-and-transactions/public-keys-1/listpublickeys.md)
      * [Get Address For Network](api-docs/deprecated-apis/low-level-api-keys-and-transactions/public-keys-1/getaddressfornetwork.md)
    * [Transaction Execution](api-docs/deprecated-apis/low-level-api-keys-and-transactions/transaction-execution/README.md)
      * [Create Signature](api-docs/deprecated-apis/low-level-api-keys-and-transactions/transaction-execution/createsignature.md)
      * [Get Signature By ID](api-docs/deprecated-apis/low-level-api-keys-and-transactions/transaction-execution/getsignaturebyid.md)
      * [Broadcast Transaction](api-docs/deprecated-apis/low-level-api-keys-and-transactions/transaction-execution/broadcasttransaction/README.md)
        * [EVMGenericTx Template](api-docs/deprecated-apis/low-level-api-keys-and-transactions/transaction-execution/broadcasttransaction/evmgenerictx-template.md)
      * [Get Transaction By ID](api-docs/deprecated-apis/low-level-api-keys-and-transactions/transaction-execution/gettransactionbyid.md)
      * [List Transactions](api-docs/deprecated-apis/low-level-api-keys-and-transactions/transaction-execution/list-transactions.md)
  * [Deprecated - Policy Engine v1](api-docs/deprecated-apis/policy-management/README.md)
    * [Policy Engine Overview](api-docs/deprecated-apis/policy-management/datamodel.md)
    * [Policy Rules](api-docs/deprecated-apis/policy-management/policy-rules/README.md)
      * [Create Policy Rule](api-docs/deprecated-apis/policy-management/policy-rules/createpolicyrule.md)
      * [Get Policy Rule By ID](api-docs/deprecated-apis/policy-management/policy-rules/getpolicyrulebyid.md)
      * [List Policy Rules](api-docs/deprecated-apis/policy-management/policy-rules/listpolicyrules.md)
      * [Archive Policy Rule](api-docs/deprecated-apis/policy-management/policy-rules/archivepolicyrule.md)
    * [Policy Controls](api-docs/deprecated-apis/policy-management/policy-controls/README.md)
      * [Create Policy Control](api-docs/deprecated-apis/policy-management/policy-controls/createpolicycontrol.md)
      * [Get Policy Control By ID](api-docs/deprecated-apis/policy-management/policy-controls/getpolicycontrolbyid.md)
      * [List Policy Controls](api-docs/deprecated-apis/policy-management/policy-controls/listpolicycontrols.md)
      * [Archive Policy Control](api-docs/deprecated-apis/policy-management/policy-controls/archivepolicycontrol.md)
    * [Policies](api-docs/deprecated-apis/policy-management/policies/README.md)
      * [Create Policy](api-docs/deprecated-apis/policy-management/policies/createpolicy.md)
      * [Get Policy By ID](api-docs/deprecated-apis/policy-management/policies/getpolicybyid.md)
      * [List Policies](api-docs/deprecated-apis/policy-management/policies/listpolicies.md)
      * [Archive Policy](api-docs/deprecated-apis/policy-management/policies/archivepolicy.md)
    * [Policy Control Executions](api-docs/deprecated-apis/policy-management/policyexecution/README.md)
      * [Get Policy Control Execution By ID](api-docs/deprecated-apis/policy-management/policyexecution/getpolicycontrolexecutionbyid.md)
      * [List Policy Control Executions](api-docs/deprecated-apis/policy-management/policyexecution/listpolicycontrolexecutions.md)
      * [Approve / Reject Policy Control Execution](api-docs/deprecated-apis/policy-management/policyexecution/approve-reject-policy-execution.md)
  * [Deprecated - Blockchains](api-docs/deprecated-apis/blockchains/README.md)
    * [Call Read Function](api-docs/deprecated-apis/blockchains/call-read-function.md)
  * [Legacy Auth Only APIs](api-docs/deprecated-apis/legacy-auth-only-apis/README.md)
    * [Deprecated - ApiKeys](api-docs/deprecated-apis/legacy-auth-only-apis/apikeys/README.md)
      * [ApiKeys Overview](api-docs/deprecated-apis/legacy-auth-only-apis/apikeys/api-keys.md)
      * [Create API Key](api-docs/deprecated-apis/legacy-auth-only-apis/apikeys/createapikey.md)
      * [Get API Key By ID](api-docs/deprecated-apis/legacy-auth-only-apis/apikeys/getapikeybyid.md)
      * [List API Keys](api-docs/deprecated-apis/legacy-auth-only-apis/apikeys/listapikeys.md)
      * [Revoke API Key](api-docs/deprecated-apis/legacy-auth-only-apis/apikeys/revokeapikey.md)
    * [Deprecated - Employees](api-docs/deprecated-apis/legacy-auth-only-apis/employees/README.md)
      * [Employees Overview](api-docs/deprecated-apis/legacy-auth-only-apis/employees/employees-overview.md)
      * [Get Employee By ID](api-docs/deprecated-apis/legacy-auth-only-apis/employees/getpermissionbyid.md)
      * [List Employees](api-docs/deprecated-apis/legacy-auth-only-apis/employees/listpermissions.md)
  * [Deprecated - Callbacks](api-docs/deprecated-apis/readme-1/README.md)
    * [Deprecated - Callback Subscriptions](api-docs/deprecated-apis/readme-1/callback-subscriptions/README.md)
      * [Create Callback Subscription](api-docs/deprecated-apis/readme-1/callback-subscriptions/createcallbacksubscription.md)
      * [Get Callback Subscription By ID](api-docs/deprecated-apis/readme-1/callback-subscriptions/getcallbacksubscriptionbyid.md)
      * [List Callback Subscriptions](api-docs/deprecated-apis/readme-1/callback-subscriptions/listcallbacksubscriptions.md)
      * [Archive Callback Subscription](api-docs/deprecated-apis/readme-1/callback-subscriptions/archivecallbacksubscription.md)
    * [Deprecated - Callback Events](api-docs/deprecated-apis/readme-1/callback-events/README.md)
      * [List Callback Events](api-docs/deprecated-apis/readme-1/callback-events/listcallbackevents.md)
      * [Get Callback Event By ID](api-docs/deprecated-apis/readme-1/callback-events/getcallbackeventbyid.md)

## Advanced Topics

* [Authentication](advanced-topics/authentication/README.md)
  * [API Authentication](getting-started/authentication-authorization.md)
  * [Request Headers](getting-started/request-headers.md)
  * [Credentials](advanced-topics/authentication/credentials/README.md)
    * [Generate a Key Pair](advanced-topics/authentication/credentials/generate-a-key-pair.md)
    * [User Credentials](advanced-topics/authentication/credentials/user-credentials.md)
    * [Access Token Credentials](advanced-topics/authentication/credentials/access-token-credentials.md)
    * [Storing WebAuthn Credentials in Password Managers](advanced-topics/authentication/credentials/storing-webauthn-credentials-in-password-managers.md)
  * [Request Signing](advanced-topics/authentication/request-signing.md)
  * [API objects](advanced-topics/authentication/api-objects.md)
* [Delegated Signing](advanced-topics/delegated-signing.md)
* [FAQ](advanced-topics/faq.md)

## Integrations

* [Fiat On/Offboarding](integrations/fiat-on-offboarding.md)
* [Gasless Transactions & Account Abstraction](integrations/gasless-transactions.md)
