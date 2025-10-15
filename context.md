# Information Governance Standard

## **Context**

Enabling automated information governance is critical to enabling data exchange at scale.

Our proposed Data Exchange Standard (version 0.3) uses a FHIR Parameters resource to transmit:

1. **Resource:** a Patient resource (person details – identifiers, DoB, names)  
2. **Reason:** URI string for legal justification (e.g., Children Act s47 investigation)

The initial approach to IG involved providing a reason for a request modelled as a simple URL to the legislation which provides the legal basis for the request. However, most data sharing is controlled through the use of data sharing agreements and these must be represented in machine readable forms to enable data sharing at speed and scale. We have designed a framework that enables users to:

1. Describe an existing data sharing agreement or policy in a machine readable format  
   * Encoding: Party 1 will share data \[X\] with party 2, for purpose \[Y\], in the context of DSA / policy / legal basis \[Z\]  
2. Enable Party 1 to formulate a request for information and assert that it is valid under a specific agreement \[as part of the data exchange request\]  
3. Enable Party 2 to make a determination that a request is valid or not and respond  
4. Log all this activity and share relevant details for transparency, audit, etc.

More information on our research into information governance can be found [in the readme file](README.md).

### Open standards for defining data sharing

A framework of open data standards and protocols to achieve machine-to-machine information governance, addressing all four requirements for describing sharing agreements, validating requests, making determinations, and ensuring auditability have been developed by the W3C.

The framework is built around Policy-Based Access Control (PBAC) principles, using semantic web standards to ensure machine readability and interoperability these standards include:

* **W3C Open Digital Rights Language (ODRL)** \- Ontology to define permissions, prohibitions, and duties. It is used to express the rule set in the DSA.  
* **W3C Data Privacy Vocabulary (DPV)** \- Standardised terms for describing data categories, processing purposes, and legal bases.	  
* **JSON-LD (or other format to be confirmed)** \- The serialisation format. Policies are expressed as Policy Graphs using these formats for interoperability and machine processability.

However these are only limited examples of these standards (ODRL and DPV) in use and further work is required to test this approach by encoding existing data sharing agreements and refining this specification based on lessons learnt. Therefore this version of the specification does not implement these standards, this may follow in a later version if viable.

### Standards for Information Governance

1. [Machine-Readable Sharing Agreements and Policies](dsa.md)
2. [Formulating an Information Request](request.md)
3. [Determine Validity and Respond / logging and auditing](decide&log.md)
* [Context](context.md)
* [Research](readme.md)
