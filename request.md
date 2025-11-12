## Formulating an Information Request with the `Request` object

A request for information must be a structured assertion (Request Object) that explicitly links the requested action to a valid, pre-defined data sharing context.  The Request Object will replace the Reason in the data exchange specification. The Request Object must include the following information and be structured as shown in the table below

* The Requesters Identity, using a verifiable identifier/credential  
* The specific data categories or data set requested.  
* The explicit, machine-readable purpose (matching a DPV term) for which the data is being requested.  
* The unique identifier (URI) of the data sharing policy that the request claims to be valid under.

| Field | Cardinality | Data Type and format | Description | Use |
| :---- | :---- | :---- | :---- | :---- |
|`Request.Identifier` | 1 (MUST) | **Object** | Unique identifier of the request | Logging and auditing. Autofilled. |
|↳ `Request.Identifier.value` | 1 (MUST) | String | The single unique identifier attached to the request. |  |
|↳ `Request.Identifier.System` | 1 (MUST) | URI | System that the identifier adheres to|  |
|`Request.DateStamp` | 1 (MUST) | ISO8601 DateTime (`YYYY-MM-DDTHH:mm:ss`) | DateTime of request | Logging and auditing. Autofilled. |
|`Request.RequesterIdentifier` | 1 (MUST) | `APICatalogueID` | The verifiable identity of the party making the request. | Authorisation check: to ensure the entity is the permitted organisation defined in the policy. Autofilled. |
|↳ `Request.RequesterIdentifier.value` | 1 (MUST) | String | The single unique identifier of the requester. | Autofilled. |
|↳ `Request.requester.Identifier.system` | 1 (MUST) | URI | System that the identifier adheres to| Autofilled. |
|`Request.RequestedData`| 1 (MUST) | **Object** | Object that contain the query parameters of the request| User choice. |
|↳ `Request.RequestedData.Query` | 1 (MUST) | `Person` object | The identifying record of the Person the requester would like information from respondents about. Conforms to the `Person` (identification) standard. | |
|`Request.AssertedPurpose` | 1 (MUST) | `SharingPurpose` | The reason for the request, using the same vocabulary as `SharingPolicy` | Constraint Check: Ensures the purpose aligns with the permitted purpose in the policy. User choice. |
|`Request.SharingPolicies` | 1, Many (MUST) | `SharingPolicy` | One or more data sharing policies the request is made under the aegis of. | Context Check: Enables the receiving system to check the requester's copy of the policy corresponds to their copy of the policy and to evaluate the request against its rules. Autofilled based on user choice regarding breadth of search.|
