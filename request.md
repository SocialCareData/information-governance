## Formulating an Information Request with the `Request` object

A request for information must be a structured assertion (Request Object) that explicitly links the requested action to a valid, pre-defined data sharing context.  The Request Object will replace the Reason in the data exchange specification. The Request Object must include the following information and be structured as shown in the table below

* The Requesters Identity, using a verifiable identifier/credential  
* The specific data categories or data set requested.  
* The explicit, machine-readable purpose (matching a DPV term) for which the data is being requested.  
* The unique identifier (URI) of the data sharing policy that the request claims to be valid under.

| Field | Cardinality | Data Type and format | Description | Use |
| :---- | :---- | :---- | :---- | :---- |
|`Request.Type` | 1 (MUST) | `RequestTypeCode` | The type of request |  |
|`Request.Identifier` | 1 (MUST) | Object | Unique identifier of the request | Logging and auditing |
|↳ `Request.Identifier.value` | 1 (MUST) | String | The single unique identifier attached to the request. |  |
|↳ `Request.Identifier.System` | 1 (MUST) | URI | System that the identifier adheres to|  |
|`Request.DateStamp` | 1 (MUST) | ISO8601 DateTime (`YYYY-MM-DDHH:mm:ss`) | DateTime of request | Logging and auditing |
|`Request.RequesterIdentifier` | 1 (MUST) | Object | The verifiable identity of the party making the request. | Authorisation check: to ensure the entity is the permitted organisation defined in the policy. |
|↳ `Request.RequesterIdentifier.value` | 1 (MUST) | String | The single unique identifier of the requester. |  |
|↳ `Request.requester.Identifier.system` | 1 (MUST) | URI | System that the identifier adheres to|  |
|`Request.RequestedData`| 1 (MUST) | Object | Object that contain the query parameters of the request|  |
|↳ `Request.RequestedData.dataCategories` | 0, Many (MAY) | `RequestDataCategoriesCode` | Lists the data types requested, using a standard vocabulary like **DPV**. NOTE: at least 2 data categories or resource identifiers must be provided. | Scope Check: Ensures the requested data is permitted for sharing by the policy. |
|↳ `Request.RequestedData.Query` | 1 (MUST) | PersonQueryObject OR OTHER QUERY OBJECT | Search query | UNDEFINED|
|`Request.AssertedPurpose` | 1 (MUST) | `RequestAssertedPurposeCode` | The specific, machine-readable reason for the request , using a standard vocabulary like DPV | Constraint Check: Ensures the purpose aligns with the permitted purpose in the policy. |
|`Request.SharingPolicyIdentifier` | 1 (MUST) | Object | The unique URI or ID of the existing policy or data sharing agreement  | Context Check: Enables the receiving system to retrieve the specific policy to evaluate the request against its rules. |
|↳ `Request.SharingPolicyIdentifier.value` | 1 (MUST) | String | The single unique identifier of the context (Policy/DSA) |  |
|↳ `Request.SharingPolicyIdentifier.system` | 1 (MUST) | URI | URI of catalogue containing the context (Policy/DSA) |  |
