## Machine-Readable Sharing Agreements and Policies with the `SharingPolicy` object

Data Sharing agreements and policies provide the context for data sharing they define:

* **Purpose and scope:** Outlining the purpose for which the data is being shared and the specific scope of the policy. This helps ensure that all parties understand how the data will be used.  
* **Roles and Responsibilities:** Specifying the roles and responsibilities of each organisation involved in the data-sharing policy. This helps ensure that all parties understand who will handle the data, maintain it, and ensure compliance with the agreement.  
* **Controls on Data Use**: Including specific and clear controls over how the data can be used, any restrictions on sharing it further, and limits on the time period for which the data can be accessed. This helps ensure that all parties understand how the data can be used.

These sharing policies (generally .pdf documents hosted online) essentially define the rules under which data can be used. To enable data sharing at speed and scale, these agreements and the rules within them, must be encoded into machine readable formats. This enables a requesting system to assert that it is valid under a specific policy. 

The table below proposes a schema for encoding a `SharingPolicy`. Some fields are based on ODRL and indicates how ODRL syntax could be used (subject to testing).

| Field | Cardinality | Data Type and format | Description | ODRL mapping |
| :---- | :---- | :---- | :---- | :---- |
|`SharingPolicy.URI` | 1 (MUST) | URI | URI of the SharingPolicy (directly linking to a published machine readable copy of the document that the sharing policy corresponds to) |  |
|`SharingPolicy.Identifier` | 1 (MUST) | **Object** | Unique ID object for the SharingPolicy |  |
|↳ `SharingPolicy.Identifier.value` | 1 (MUST) | String | The single unique identifier attached to the SharingPolicy. |  |
|↳ `SharingPolicy.Identifier.System` | 1 (MUST) | URI | System that the identifier adheres to|  |
|`SharingPolicy.Name` | 1 (MUST) | String | Name of the SharingPolicy |  |
|`SharingPolicy.Contact` | 1 (MUST) | String | Contact information for the document "owner". Note: this will be in the document that the URI links to, so is mostly here for when the URI is inaccessible or otherwise. |  |
|**Parties** |  |  | The parties to the agreement. |  |
|`SharingPolicy.Party` | 1, Many (MUST) | **Object** | Information about a single party in the sharing policy. Parties can be both providers and recipients of requests.| `odrl:Assigner` |
|`SharingPolicy.Party.Name` | 1 (MUST) | String | The name of a party in the sharing policy |  |
|`SharingPolicy.Party.CatalogueID` | 1, Many (MUST) | `APICatalogueID` | The ID of the party in the central API catalogue. | |
| **Purpose and scope of agreement** |  |  | Defining what data can be used for what purpose. |  |
|`SharingPolicy.Data` | 1, Many (MUST) | String or URI | A desription of the specific data or data set (e.g., a database, file, or stream) that the rules apply to. Can link to a description via URI. | `odrl:Target` (Asset) |
|`SharingPolicy.Purpose` | 1, Many (MUST) | `SharingPurpose` | Used to dictate what kinds of request are valid under the policy, like Section 47 or 17 inquiries, referrals, or otherwise. | `odrl:Constraint` on `odrl:purpose` |
|`SharingPolicy.StartDate` | 1 (MUST) | DateStamp | Used to limit Permission rules to a specific time frame. | `odrl:dateTime` |
|`SharingPolicy.EndDate` | 1 (MUST) | DateStamp | Used to limit Permission rules to a specific time frame, typically using  | `odrl:until` |
| **Data usage rules** |  |  | The core usage clauses of the SharingPolicy are directly translated into ODRL Rules: Permissions, Prohibitions, and Duties |  |
|`SharingPolicy.PermittedUse`| 1, Many (May) | Code | Grants the right to perform an Action on the Asset, such as `odrl:read`, `odrl:reproduce`, or `odrl:analyze`. | `odrl:Permission`	  |
|`SharingPolicy.Restrictions` | 0, Many (May) | Code | Explicitly forbids an Action For example blocking dissemination by prohibiting `odrl:transfer` or `odrl:distribute`. Or commercial use by prohibiting `odrl:sell` | `odrl:Prohibition`	  |
|`SharingPolicy.DataRecipientResponsibilities`  | 0, Many (May) | Code | These are actions the Recipient must perform. For example, the Permission to access the data may have a Duty to delete the data after the agreement duration. | `odrl:Duty`	  |
|`SharingPolicy.SecurityMeasure` | 0, Many (May) | Code | A Permission to reproduce the data may be conditioned on a Duty to encrypt the copies, constrained by specific encryption algorithms (e.g., AES-256) | `odrl:Duty` \+ Constraint |
|`SharingPolicy.LegalCompliance`  | 0, Many (May) | Code | Compliance with specific regulations (e.g., GDPR) can be modeled as a Constraint on all rules. | `odrl:Constraint` |
