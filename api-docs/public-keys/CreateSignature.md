
## CreateSignature
`RESTful Endpoint: post /mpc/public-keys/{publicKeyId}/signatures`

Operation accepts a message, and uses Dfns MPC network to create signature against it.


### Input Query Parameters
* Path parameter `publicKeyId`: `String`.  
  

### Input Body Parameters
* hash: `String` 

_Please consult OpenAPI file full breakdown and including nested properties._


{% swagger src="../../.gitbook/assets/production-dfns-api-openapi.json" path="/mpc/public-keys/{publicKeyId}/signatures" method="post" %}
[production-dfns-api-openapi.json](../../.gitbook/assets/production-dfns-api-openapi.json)
{% endswagger %}
