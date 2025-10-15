# Information governance

## Status

Version 0.1 - intial

Effective Date: 2025-10-09
## Machine-Readable Sharing Agreements and Policies

Data Sharing agreements and policies provide the context for data sharing they define:

* **Purpose and scope:** Outlining the purpose for which the data is being shared and the specific scope of the agreement. This helps ensure that all parties understand how the data will be used.  
* **Roles and Responsibilities:** Specifying the roles and responsibilities of each organisation involved in the data-sharing agreement. This helps ensure that all parties understand who will handle the data, maintain it, and ensure compliance with the agreement.  
* **Controls on Data Use**: Including specific and clear controls over how the data can be used, any restrictions on sharing it further, and limits on the time period for which the data can be accessed. This helps ensure that all parties understand how the data can be used.

These agreements essentially define the rules under which data can be used. To enable data sharing at speed and scale, these agreements and the rules within them, must be encoded into machine readable formats. This enables a requesting system to assert that it is valid under a specific DSA 

The table below proposes a schema for encoding a data sharing agreement, this is based on ODRL and indicates how ODRL syntax could be used (subject to testing).

| Field | Cardinality | Data Type and format | Description | ODRL mapping |
| :---- | :---- | :---- | :---- | :---- |
| dsaObject | 1 (Must) | Object | The top-level container for all rules. | odrl:Agreement Policy |
| dsaURI | 1 (MUST) | URI | URI of DSA (directly linking to a published machine readable copy of the DSA) |  |
| **Parties** |  |  | The parties to the agreement. |  |
| DataProvider | 1, Many (Must) | URI | The party granting the rights (the data owner/controller). Identified by a URI. | odrl:Assigner |
| DataRecipient | 1, Many (Must) | URI | The party receiving the rights (the data consumer). Identified by a URI. | odrl:Assignee |
| **Purpose and scope of agreement** |  |  | Defining what data can be used for what purpose. |  |
| Data | 1, Many (Must) | URI / String | The specific data or data set (e.g., a database, file, or stream) that the rules apply to. Identified by a unique URI. | odrl:Target (Asset) |
| Purpose | 1, Many (Must) | Code | Used to limit Permission rules. E.g., a permission to analyse is constrained by odrl:purpose being equal to "research" or "service improvement". | odrl:Constraint on odrl:purpose |
| StartDate | 1 (Must) | DateStamp | Used to limit Permission rules to a specific time frame. | odrl:dateTime |
| **EndData** | 1 (Must) | DateStamp | Used to limit Permission rules to a specific time frame, typically using  | odrl:until |
| **Data usage rules** |  |  | The core usage clauses of the DSA are directly translated into ODRL Rules: Permissions, Prohibitions, and Duties |  |
| PermittedUse  | 1, Many (May) | Code | Grants the right to perform an Action on the Asset, such as odrl:read, odrl:reproduce, or odrl:analyze. | odrl:Permission	  |
| Restrictions | 0, Many (May) | Code | Explicitly forbids an Action For example blocking dissemination by prohibiting odrl:transfer or odrl:distribute. Or commercial use by prohibiting odrl:sell | odrl:Prohibition	  |
| DataRecipientResponsibilities  | 0, Many (May) | Code | These are actions the Recipient must perform. For example, the Permission to access the data may have a Duty to delete the data after the agreement duration. | odrl:Duty	  |
| SecurityMeasure | 0, Many (May) | Code | A Permission to reproduce the data may be conditioned on a Duty to encrypt the copies, constrained by specific encryption algorithms (e.g., AES-256) | odrl:Duty \+ Constraint |
| LegalCompliance  | 0, Many (May) | Code | Compliance with specific regulations (e.g., GDPR) can be modeled as a Constraint on all rules. | odrl:Constraint |

### Standards for Information Governance

1. [Machine-Readable Sharing Agreements and Policies](dsa.md)
2. [Formulating an Information Request](request.md)
3. [Determine Validity and Respond / logging and auditing](decide&log.md)
* [Context](context.md)
* [Research](README.md)
