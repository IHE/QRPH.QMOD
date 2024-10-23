This section corresponds to transaction [\[QRPH-60\]](QRPH-60.html) of the IHE Technical Framework. Transaction [\[QRPH-60\]](QRPH-60.html) is used by the Data Responder and Data Consumer Actors to Query for ODH Quality Data. 

### Scope

The Data Consumer [\[QRPH-60\]](QRPH-60.html) transaction sends a query for Quality Data to the Data Responder. This transaction is used to query an entity for information needed to compute ODH quality measures

### Actors Roles

**Table: Actor Roles**

|Actor | Role |
|-------------------+--------------------------|
| [Data Responder ](volume-1.html#DataResponder)    | The Data Responder responds to a query for ODH quality data. |
| [Data Consumer ](volume-1.html#DataCOnsumer) | The Data Consumer sends a query for the ODH quality data and receives the response returned by the Data Responder.  |

### Referenced Standards

**FHIR-R4** [HL7 FHIR Release 4.0]({{site.data.fhir.path}})

### Interactions

<figure>
{%include domain-Y-seq.svg%}
<p id="fX.X.X.X-X" class="figureTitle">Figure X.X.X.X-X: Query for ODH Quality Data Interaction Diagram</p>
</figure>
<br clear="all">

#### go Query Message

This message uses the HTTP GET method on the target Server endpoint to convey the query parameters FHIR query.

##### Trigger Events

''TODO: define the triggers''

##### Message Semantics

''TODO: define the message -- usually with a StructureDefintion''

##### Expected Actions

''TODO: define expected actions''

#### Go Response Message

##### Trigger Events

''TODO: define the triggers''

##### Message Semantics

''TODO: define the message -- usually with a StructureDefintion''

##### Expected Actions

''TODO: define expected actions''

### CapabilityStatement Resource

Server implementing this transaction shall provide a CapabilityStatement Resource as described in ITI TF-2x: Appendix Z.3 indicating the transaction has been implemented.

* Requirements CapabilityStatement for [Client](CapabilityStatement-IHE.ToDo.client.html)
* Requirements CapabilityStatement for [Server](CapabilityStatement-IHE.ToDo.server.html)

### Security Considerations

See [MHD Security Considerations](volume-1.html#security-considerations)

#### Security Audit Considerations

''TODO: The security audit criteria ''

##### Client Audit

''TODO: the specifics''

##### Server Audit

''TODO: the specifics''
