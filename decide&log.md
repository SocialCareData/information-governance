# Determine Validity and Respond (The Decision)

Validity determination is managed by the recipient of requests using a  Policy Decision Point (PDP) service.

The PDP must be able to:

1. Receive the requestObject and fetch the relevant dsaObject.
2. Apply the rules on the dsaObject to determine if the request is valid.   
3. Generate a machine readable response PERMIT, DENY or REVIEW to Instruct the receiving system to proceed with the request, or not, or escalate for human review.

It should be noted that the PDP’s role is to determine if a request is valid against a data sharing agreement. **It will not assess the risk of sharing data.** This risk judgement will need to be made as part of a subsequent matching process if data relating to an individual is identified.

# Logging and Auditing

All activities must be logged in a transparent and auditable manner using a standardised approach designed to record the history and flow of data actions.

To ensure all data controllers and processors can meet their legal obligations we recommend that requestors and responders make a permanent record of the following data

| Requestor | Responder |
| :---- | :---- |
| Log the Information Request (requestObject)  | Log the Information Request (requestObject) |
| Log the DSA (dsaObject) and version | Log the DSA (dsaObject) and version |
|  | Make a record of the decision making process and outcome |
|  | Log response sent to the requestor (PERMIT, DENY) |
| Log response received from responder (PERMIT, DENY) |  |

An Immutable Log / Distributed Ledger could be used to store a complete audit trail in a secure format.

This could use W3C PROV-O (Provenance Ontology) or similar to ensure every key step (Request, Decision, Data Release) is logged as an Activity that involved specific Agents (Parties 1 & 2\) and affected Entities (The Request, The Policy, and The Data).

Further work is required to develop a comprehensive standard for logging and auditing MAIS requests.

### Standards for Information Governance

1. [Machine-Readable Sharing Agreements and Policies](dsa.md)
2. [Formulating an Information Request](request.md)
3. [Determine Validity and Respond / logging and auditing](decide&log.md)
* [Context](context.md)
* [Research](README.md)
