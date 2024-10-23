This section corresponds to transaction [\[QRPH-60\]](QRPH-60.html) of the IHE Technical Framework. Transaction [\[QRPH-60\]](QRPH-60.html) is used by the Data Responder and Data Consumer Actors to Query for ODH Quality Data. 

### Scope

The Data Consumer [\[QRPH-60\]](QRPH-60.html) transaction sends a query for Quality Data to the Data Responder. This transaction is used to query an entity for information needed to compute ODH quality measures

### Actors Roles

**Table: Actor Roles**

|Actor | Role |
|-------------------+--------------------------|
| [Data Responder](volume-1.html#DataResponder)    | The Data Responder responds to a query for ODH quality data. |
| [Data Consumer](volume-1.html#DataCOnsumer) | The Data Consumer sends a query for the ODH quality data and receives the response returned by the Data Responder.  |

### Referenced Standards

**FHIR-R4** [HL7 FHIR Release 4.0]({{site.data.fhir.path}})
**FHIR Bulk Data Access** [FHIR Bulk Data Access](https://www.hl7.org/fhir/uv/bulkdata/)
**HL7 FHIR CQF** [HL7 FHIR CQF](https://fhir.org/guides/cqf/common/)
**HL7 FHIR DEQM** [HL7 FHIR DEQM](https://build.fhir.org/ig/HL7/davinci-deqm/)
**LOINC**  [LOINC](https://loinc.org/) 
**SNOMED**   [SNOMED](https://www.snomed.org/)


### Interactions

<figure>
{%include QRPH-60-seq.svg%}
<p id="fX.X.X.X-X" class="figureTitle">Figure X.X.X.X-X: Query for ODH Quality Data Interaction Diagram</p>
</figure>
<br clear="all">

#### Query for ODH Quality Data

The Data Consumer initiates a query to the Data Responder. The Data Responder returns the ODH quality measure report data to the Data Consumer that will use this data for quality outcomes measure analysis.

##### Trigger Events

When the organization is ready to measure ODH quality data, they would initiate a Query for ODH Quality Data [\[QRPH-60\]](QRPH-60.html).

##### Message Semantics

The message is a FHIR transaction using a query action by sending an HTTP GET request  composed of a FHIR Bundle Resource containing a measure report. This query uses the following semantics:
GET [base]/patient?condition.code:in=[Value set resource URL]&[other search criteria defined below]
GET [base]/patient?procedure.code:in=[Value set resource URL]&[other search criteria defined below]
GET [base]/patient?medicationAdministration.medicationCodableConcept:in=[Value set resource URL]&[other search criteria defined below]
GET [base]/patient? Observation.value[x]:in=[Value set resource URL]&[other search criteria defined below] Where code = 21843-8 History of Usual Occupation, LOINC
GET [base]/patient? Observation.value[x]:in=[Value set resource URL]&[other search criteria defined below] Where code = 21844-6 History of Usual Industry, LOINC
GET [base]/patient? Observation.value[x]:in=[Value set resource URL]&[other search criteria defined below] Where code = 11341-5 History of Occupation, LOINC for the past or present job
GET [base]/patient? Observation.value[x]:in=[Value set resource URL]&[other search criteria defined below] Where code = 86188-0 History of Occupation Industry, LOINC for the past or present  industry

The Value Set resource URL to be used in these queries is defined for each measure set or measure as determined by the quality measurement organization. The URL SHALL reference an active URL.
The following table defines additional search criteria that may be used to filter the query results:

Table 3.xx.4.1.2-1: Additional Search Criteria
|  Attribute       |   Criteria   |
|---------|---------------|
| Age (as computed as encounter.period - patient.birthdate)  | Patient age within a specified range. This may be in years, months, or days as defined by the measure or measure set  |
| Encounter.period | Specify reporting period range |
|  Resource.meta.lastUpdated       | Date comparison to support updated information and polling mechanisms |
| Observation.valueCodeableConcept where Obsercation.code=11341-5 | Specify an occupation filter for Usual Occupation |
| Observation.valueCodeableConcept. component:odh-PastOrPresentIndustry.valueCodeableConcept  where Obsercation.code=86188-0        | Specify an industry filter for Usual Industry |
| Observation.valueCodeableConcept where Obsercation.code=21843-8 | Specify an occupation filter for Past or Present Job |
| Observation.valueCodeableConcept. component:odh-PastOrPresentIndustry.valueCodeableConcept  where Obsercation.code=21844-6 | Specify an industry filter for Past or Present Industry |
| Encounter.type        | Query may be constrained to inpatient, outpatient, or emergency patients |
| Observation.valueCodeableConcept. component:odh-PastOrPresentIndustry.valueCodeableConcept  where Obsercation.code=74165-2        | Specify an industry filter for Employment Status |
{: .grid}
A Group may be defined to support this use case such that the filters described above are pre-defined. In this case, the query uses the following semantics:
 [fhir base]/Group/[id]/$export


##### Expected Actions

The Data Consumer initiates a Query for ODH Quality Data [\[QRPH-60\]](QRPH-60.html) to retrieve the measure report resource bundle that returns the resources specified in QRPH TF-3: 6.6.X FHIR Resource Bundle Content using the message semantics specified in Section 3.xx.4.1.2. The Data Responder receives the query and responds with the resources specified in QRPH TF-3: 6.6.X FHIR Resource Bundle Content according to FHIR Search specification with the query response information or an error message. See: [HL7 FHIR Release 4.0](http://hl7.org/fhir/R4/index.html).


### CapabilityStatement Resource

Server implementing this transaction shall provide a CapabilityStatement Resource as described in ITI TF-2x: Appendix Z.3 indicating the transaction has been implemented.

* Requirements CapabilityStatement for [Data Consumer](CapabilityStatement-IHE.ToDo.client.html)
* Requirements CapabilityStatement for [Data Responder](CapabilityStatement-IHE.ToDo.server.html)

### Security Considerations

See [MHD Security Considerations](volume-1.html#security-considerations)

#### Security Audit Considerations

There must be a trusted connection between the Data Responder and Data Consumer. This will be carried out in implementation and can either be a business relationship or a secured connection done through ATNA. The Data Consumer has control of what information will be requested. The Data Responder has control of what information will be returned. This transaction may include identifiable health information, or it may leverage deidentification, see the ITI De-Identification White Paper for guidance. Depending upon the implementation and application, may constitute a disclosure of health information that requires audit, encryption, and authentication of the Data Consumer and Data Responder. For further guidance, see ITI TF-2.x: Appendix Z.8 “Mobile Security Considerations”. 

##### Client Audit

''TODO: the specifics''

##### Server Audit

''TODO: the specifics''
