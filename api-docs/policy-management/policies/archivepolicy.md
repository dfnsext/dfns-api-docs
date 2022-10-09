
## ArchivePolicy
`RESTful Endpoint: DELETE /policies/{policyId}`

Scopes:
 * as Employee Auth: Policies:ArchivePolicy
 * as API Key: Policies:ArchivePolicy

Deactivates a specific `Policy` entity by its `PolicyId` and marks its `status` as `Archived`.
### Input Query Parameters
* Path parameter `policyId`: undefined

### Successful Response
* id: `EntityId`. 
* version: `String`. 
* activityKind: `PolicyActivityKind`. 
* tags: `Tag[]`. 
* dateCreated: `IsoDatetime`. 
* isImmutable: `Bool`. 
* orgId: `EntityId`. 
* description: `String`. 
* author: `Username`. 
* name: `String`. 
* status: `PolicyStatus`. 
* controlIds: `EntityId[]`. 
* ruleIds: `EntityId[]`. 
* filter: `PolicyObjectFilter`.
### Error Responses
#### `404` **policyNotFound** 
Policy with provided Id doesn't exist. Please see `causes` for additional information.
* serviceName: `String`. 
* message: `String`. 
* causes: `String[]`. 
* shouldTriggerInvestigaton: `Bool`. 
* isDfnsError: `Bool`. 
* httpStatus: `Integer`. 
* errorName: `String`.

