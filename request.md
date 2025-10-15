# Formulating an Information Request

A request for information must be a structured assertion (Request Object) that explicitly links the requested action to a valid, pre-defined data sharing context.  The Request Object will replace the Reason in the data exchange specification. The Request Object must include the following information and be structured as shown in the table below

* The Requesters Identity, using a verifiable identifier/credential  
* The specific data categories or data set requested.  
* The explicit, machine-readable purpose (matching a DPV term) for which the data is being requested.  
* The unique identifier (URI) of the data sharing policy that the request claims to be valid under.

| Field | Cardinality | Data Type and format | Description | Use |
| :---- | :---- | :---- | :---- | :---- |
| requestObject | 1 (Must) | Object | Container object for request |  |
| requestType | 1 (MUST) | Code | Determines the type of request |  |
| requestId | 1 (MUST) | Object | Unique identifier of the request | Logging and auditing |
| ↳requestID.Value | 1 (MUST) | String | The single unique identifier attached to the request. |  |
| ↳requestId.System | 1 (MUST) | URI | System that the identifier adheres |  |
| DateStamp | 1 (MUST) | Date/Time | Date/time of request | Logging and auditing |
| requester.entityID | 1 (MUST) | Object | The verifiable identity of the party making the request. | Authorisation check: to ensure the entity is the permitted organisation defined in the policy. |
| ↳requester.entityId.Value | 1 (MUST) | String | The single unique identifier of the requester. |  |
| ↳requester.entityId.System | 1 (MUST) | URI | System that the identifier adheres |  |
| requestedData.dataCategories | 0, Many (MAY) | Code | Lists the data types requested, using a standard vocabulary like **DPV**. NOTE: at least 2 data categories or resource identifiers must be provided. | Scope Check: Ensures the requested data is permitted for sharing by the policy. |
| requestedData.resourceIdentifier | 0, Many (MAY) | Object | Lists specific data sets requested, by reference to URIs in a data catalogue. NOTE: at least 2 data categories or resource identifier must be provided | Scope Check: Ensures the requested data is permitted for sharing by the policy. |
| ↳requestedData.resourceIdentifier.Value | 1 (MUST) | String | The single unique identifier of the requester. |  |
| ↳requestedData.resourceIdentifier.System | 1 (MUST) | URI | URI of catalogue containing the resource |  |
| assertedPurpose | 1 (MUST) | Code | The specific, machine-readable reason for the request , using a standard vocabulary like DPV | Constraint Check: Ensures the purpose aligns with the permitted purpose in the policy. |
| Context | 1 (MUST) | Object | The unique URI or ID of the existing policy or data sharing agreement  | Context Check: Enables the receiving system to retrieve the specific policy to evaluate the request against its rules. |
| ↳Context.Value | 1 (MUST) | String | The single unique identifier of the context (Policy/DSA) |  |
| ↳Context.System | 1 (MUST) | URI | URI of catalogue containing the context (Policy/DSA) |  |

### Standards for Information Governance

1. [Machine-Readable Sharing Agreements and Policies](dsa.md)
2. [Formulating an Information Request](request.md)
3. [Determine Validity and Respond / logging and auditing](decide&log.md)
* [Context](context.md)
* [Research](README.md)
