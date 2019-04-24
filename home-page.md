
# Home Page
<p id="publish-box">
This is a pre-release version (Ballot 1) of Payer Data exchange  (PDex) R1/STU.
There is no current official version.
</p>

This specification is currently undergoing ballot and connectathon testing. It is expected to evolve, possibly significantly, as part of that process.


Feedback is welcome and may be submitted through the [FHIR gForge tracker](http://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemAdd&tracker_id=677/) indicating US Da Vinci PDex as the specification. If balloting on this IG, please submit your comments via the tracker and just reference them in your ballot submission implementation guide.


## Overview

This guide is based on the [HL7 FHIR](http://build.fhir.org/index.html) standard, as well as the [CDS Hooks](https://cds-hooks.org/) and [SMART on FHIR](http://docs.smarthealthit.org/) standards, which build additional capabilities on top of FHIR. This architecture is intended to maximize the number of clinical and payer systems that conform to this guide as well as to allow for easy growth and extensibility of system capabilities in the future.

Implementers of this specification therefore need to understand some basic information about these specifications, which act as building blocks for this Implementation Guide.

# Introduction
                                                                                                                                                   
 The PDex IG identifies three actors and specifies three interactions that occur. Each interaction differs based upon the actors involved and the data payload that **SHALL** be communicated. 
                                                                                                                                                    
  Whereas the Blue Button 2.0 initiative is specifying the profiles used to communicate claims information between health plans and their members. The PDex Implementation Guide (IG) is focused on presenting a member’s health and claims information in FHIR clinical profiles that are more easily consumed by Electronic Medical Records (EMR) systems. 
                                                                                                                                                   
 The same FHIR profiles used to support communication between the health plan and providers will also be used to provide the payload of member health information that will be exchanged between health plans when authorized by a health plan member.
                                                                                                                                                   
 While the authorization and communication mechanisms may differ between the provider-to-payer exchange (P2HPX) and the member-authorized  Payer-to-Payer exchange (MauthHPX) or member-authorized Payer to Third-Party Application exchange (Mauth3PX)  the payload of member history will be the same.  
                                                                                                                                                   
 The objective with the above approach is to:
 - Minimize the proliferation of FHIR profiles by encouraging the re-use of FHIR profiles that have seen significant development effort invested in development and implementation
 - Consolidate the number of operational interfaces that health plans and  EMR systems need to maintain in order to meet regulatory requirements.
   
## Implementation Guide Scope

The first release of the PDex IG will focus on the following in scope items. Items in the deferred scope category will be considered for future iterations of the IG, or will be accommodated via an alternative Da Vinci Use Case project. Out of scope items are not being considered at this time.

### In Scope

- Ambulatory Care Provider queries
- Outpatient encounter
- Member-mediated Payer-to-Payer information exchange
- Member-mediated Payer-to-Third-Party-Application information exchange

### Deferred Scope

- In Patient Care Provider queries
- Provider initiated data push

### Out of Scope

- Wearable device data

## Member Consent

Member/Patient Consent for scenarios covered in this Implementation Guide fall into two areas:

1. Provider-Health Plan Exchange
2. Member-mediated Information Exchange

### Provider to Payer Exchange

Provider-Health Plan exchange of data is covered by the Health Insurance Portability and Accountability Act (HIPAA) under the [Treatment Payment and Health Care Operations](https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/disclosures-treatment-payment-health-care-operations/index.html) provision.

### Member-mediated Information Exchange

The CMS Notice For Proposed Rule Making for Patient access and Interoperability requires that a subscriber to a new health plan **SHOULD** be able to request their information to be passed from their old health plan to their new health plan.

A Member will also be able to use APIs to share information with Third Party Applications. This includes:

- Their health history
- Healthcare network information
- Pharmacy network information
- Prescription Drug Formulary information

The Member-mediated Information Exchange method will build upon established OAuth2.0 protocols for patient access to their health and claims information that enables the sharing of information with third-party applications. The health history payload for the exchange would be the same FHIR resources that are passed to providers under the Provider-Payer exchange scenario.


## Conventions

This implementation guide (IG) uses specific terminology to flag statements that have relevance for the evaluation of conformance with the guide:

**SHALL** indicates requirements that must be met to be conformant with the specification.

**SHOULD** indicates behaviors that are strongly recommended (and which may result in interoperability issues or sub-optimal behavior if not adhered to) but which do not, for this version of the specification, affect the determination of specification conformance.

**MAY** describes optional behaviors that are free to consider but where there is no recommendation for, or against, adoption.

It is important to differentiate in the Implementation Guide between identifiers used by the Provider/EMR and those used by the Payer/Health Plan to identify the patient/subject/member.

For the purposes of this IG we will use the following terms:

* **patient** or **subject** id will be used to express the identifier used by the provider to identify a patient/subject.

* **subscriber** or **member** id will be used to express the identifier used by the payer/health plan to identify a member.

## FHIR

This implementation guide uses terminology, notations and design principles that are specific to FHIR. Before reading this implementation guide, its important to be familiar with some of the basic principles of FHIR as well as general guidance on how to read FHIR specifications. Readers who are unfamiliar with FHIR are encouraged to read (or at least skim) the following prior to reading the rest of this implementation guide.


* [FHIR overview](http://build.fhir.org/overview.html)
* [Developer's Introduction](http://build.fhir.org/overview-dev.html)
* [Clinical Introduction](http://build.fhir.org/overview-clinical.html)
* [FHIR data types](http://build.fhir.org/datatypes.html)
* [Using codes](http://build.fhir.org/terminologies.html)
* [References between resources](http://build.fhir.org/references.html)

* [How to read resource and profile
definitions](http://build.fhir.org/formats.html)
* [Base resource](http://build.fhir.org/resource.html)


## Supporting Specifications

This implementation guide is dependent on other specifications. Please submit any comments you have on these base specifications as follows:
 
- Feedback on CDS Hooks should be posted to the CDS Hooks [GitHub Issue List](https://github.com/cds-hooks/docs/issues)

- Feedback on the FHIR core specification should be submitted to the [FHIR gForge tracker](http://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemAdd&tracker_id=677) with "FHIR Core" as the specification.

- Feedback on the US core profiles should be submitted to the [FHIR gForge tracker](http://gforge.hl7.org/gf/project/fhir/tracker/?action=TrackerItemAdd&tracker_id=677) with "US Core" as the specification.

- Individuals interested in participating in Payer Data exchange (PDex) or other HL7 Da Vinci projects can find information about Da Vinci [here](http://www.hl7.org/about/davinci).

 
There are a few places in this implementation guide marked as **TODO**. All such areas represent supplementary content such as examples, additional background or context or other non-definitional content. I.e. they do not change any of the conformance expectations on implementers. Where ToDo appears, such content will be created and included in the implementation guide prior to publication as a Standard for Trial Use.

 
## Implementation Assumptions

Wherever possible, the PDex IG will use established US Core Profiles. Where information must be presented in FHIR resources that fall outside of the US Core Implementation Guide (IG) the HL7 Da Vinci Health Record exchange (HRex) IG will define the necessary Da Vinci FHIR profiles or will refer to other Implementation Guides, as necessary.


## Implementation Hierarchy and Priorities

The PDex Implementation Guide (IG) will utilize existing HL7 FHIR Profiles in the following order of descending priority:
 
1. HL7 FHIR US Core STU3 (based on FHIR R4 - https://build.fhir.org/ig/HL7/US-Core-R4/ ) 
2. Da Vinci HRex IG profiles (based on FHIR R4 - http://build.fhir.org/ig/HL7/davinci-hrex/index.html )
3. HL7 Argonaut Profiles (based on FHIR DSTU2 - http://www.fhir.org/guides/argonaut/r2/ )
4. HL7 FHIR US Core STU2 (based on FHIR STU3 - http://hl7.org/fhir/us/core/STU2/ )


This Implementation Guide recognizes that Electronic Medical Record systems used by providers may have existing FHIR APIs that are based on versions of FHIR prior to FHIR R4.

Amongst health plans there has been limited adoption of FHIR APIs. Therefore for health plan APIs identified in this IG the FHIR R4 version **SHALL** be used.

# PDex Implementation Actors, Interactions, Data Payloads and Methods

This section defines the Actors, Exchange Interactions, Data Payloads and interaction Methods covered by the PDex IG.

## Actors

The following actors are recognized in the PDex IG:

- **Health Plan**: The Insurance entity, or Payer, who handles claims for services provided to their plan members. 
- **Member**: The health plan member / patient who is, or was, a member of a health plan.
- **Provider**: The practitioner or clinician, or their representative, that initiates a data access request to retrieve member data from a health plan.
- **Third Party Application**: Health Plan Members / Patients have a right under the Health Insurance Portability and Accountability Act of 1996 (HIPAA) to direct the information held by a covered entity, such as a Hospital or Health Plan to a third party of their choosing.
 
## PDex Actor Interactions

The PDex IG is specifying three exchange interactions:
 
1. Providers and Health Plans (payers) exchanging information about the Member that a provider is caring for (P2HPX).
2. Health Plans via a Member authorized exchange when a Member has moved from enrollment in one health plan to another health plan (MauthHPX).
3. Health Plans and Third Party Applications that a Member has authorized to share the health information held by the health plan and other supporting plan information such as Network and Formulary information (Mauth3PX).


## PDex Data Payloads

The PDex IG defines four types of data payload:

1. Member Clinical and Claims-derived History
2. Healthcare Network Directory 
3. Pharmacy Network Directory
4. Medication Formulary

All resources available via a FHIR API endpoint **SHALL** be declared in a FHIR CapabilityStatement.

### 1. Member Clinical and Claims-derived History

The FHIR Resources that comprise the Member Clinical and Claims-derived history SHOULD include the following profiles:

#### US Core

- [US Core AllergyIntolerance Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-allergyintolerance.html)
- [US Core CarePlan Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-careplan.html)
- [US Core CareTeam Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-careteam.html)
- [US Core Condition Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-condition.html)
- [US Core Device Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-device.html)
- [US Core DiagnosticReport Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-diagnosticreport.html)
- [US Core Diagnostic Report Profile for Report and Note exchange](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-new-us-core-diagnosticreport.html)
- [US Core DocumentReference Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-documentreference.html)
- [US Core Encounter Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-encounter.html)
- [US Core Goal Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-goal.html)
- [US Core Immunization Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-immunization.html)
- [US Core Location Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-location.html)
- [US Core Medication Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medication.html)
- [US Core MedicationRequest Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medicationrequest.html)
- [US Core MedicationStatement Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medicationstatement.html)
- [US Core Organization Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-organization.html)
- [US Core Patient Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-patient.html)
- [US Core Pediatric BMI Observation Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-pediatric-bmi.html)
- [US Core Pediatric Weight Observation Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-pediatric-weight.html)
- [US Core Practitioner Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-practitioner.html)
- [US Core PractitionerRole Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-practitionerrole.html)
- [US Core Procedure Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-procedure.html)
- [US Core Result Observation Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-observationresults.html)
- [US Core Smoking Status Observation Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-smokingstatus.html)
In addition US Core uses the [Vital Signs Profile](http://hl7.org/fhir/R4/observation-vitalsigns.html) from the FHIR Specification.

#### Da Vinci HRex

- [ HRex Coverage](http://build.fhir.org/ig/HL7/davinci-ehrx/StructureDefinition-hrex-coverage.html)
- [HRex MedicationDispense]() **_TODO_**
- [HRex Provenance](http://build.fhir.org/ig/HL7/davinci-ehrx/StructureDefinition-hrex-provenance.html)

#### CapabilityStatement

The FHIR CapabilityStatement defines the resources and operations permitted on the resources exposed via the FHIR API.

The Permitted Operations for the FHIR Profiles covered in this payload section are defined as follows:

<table>
  <tr>
    <th> Resource Type </th>
    <th> Profile </th>
    <th> Read </th>
    <th> V-Read </th>
    <th> Search </th>
    <th> Update </th>
    <th> Create </th>
    <th> Updates </th>
    <th> History </th>
  </tr>
  <tr>
    <td>AllergyIntolerance</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-allergyintolerance.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>CarePlan</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-careplan.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>CareTeam</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-careteam.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>Condition</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-condition.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>Coverage</td>
    <td>http://build.fhir.org/ig/HL7/davinci-ehrx/StructureDefinition-hrex-coverage.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>Device</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-device.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>DiagnosticReport</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-diagnosticreport.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
   <tr>
     <td>DiagnosticReport for report and Note Exchange</td>
     <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-new-us-core-diagnosticreport.html</td>
     <td>Y</td>
     <td>Y</td>
     <td>Y</td>
     <td></td>
     <td></td>
     <td></td>
     <td>Y</td>
   </tr>  
   <tr>
      <td>DocumentReference</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-documentreference.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
   <tr>
      <td>Encounter</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-encounter.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Goal</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-goal.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Immunization</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-immunization.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Location</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-location.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Medication</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medication.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>MedicationDispense</td>
      <td></td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>MedicationRequest</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medicationrequest.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>MedicationStatement</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medicationstatement.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Organization</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-organization.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Patient</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-patient.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>
    <tr>
      <td>Pediatric BMI Observation</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-pediatric-bmi.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Pediatric Weight Observation</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-pediatric-weight.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Practitioner</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-practitioner.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>PractitionerRole</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-practitionerrole.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Procedure</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-procedure.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Provenance</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-provenance.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Result Observation</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-observationresults.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  
    <tr>
      <td>Smoking Status Observation</td>
      <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-smokingstatus.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>
    <tr>
      <td>Vital Signs</td>
      <td>http://hl7.org/fhir/R4/observation-vitalsigns.html</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Y</td>
    </tr>  

</table>


### 2. Healthcare Network Directory 

The provision of a Member-accessible Healthcare Directory API for a health plan's network **SHALL** use the profiles and other stipulations detailed in the [Validated Healthcare Directory Implementation Guide](http://build.fhir.org/ig/HL7/VhDir/index.html) (VHDir IG). The profiles defined in the VHDir IG are:

- [VhDir Care Team](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-careteam.html)
- [VhDir Endpoint](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-endpoint.html)
- [VhDir Healthcare Service](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-healthcareservice.html)
- [VhDir Insurance Plan](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-insuranceplan.html)
- [VhDir Location](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-location.html)
- [VhDir Network](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-network.html)
- [VhDir Organization](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-organization.html)
- [VhDir Organization Affiliation](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-organizationaffiliation.html)
- [VhDir Practitioner](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-practitioner.html)
- [VhDir Practitioner Role](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-practitionerrole.html)
- [VhDir Restriction](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-restriction.html)
- [VhDir Validation](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-validation.html)

#### CapabilityStatement

The [Validated Healthcare Directory Implementation Guide](http://build.fhir.org/ig/HL7/VhDir/index.html) (VHDir IG) is detailed here: [http://build.fhir.org/ig/HL7/VhDir/CapabilityStatement-vhdir-server.html](http://build.fhir.org/ig/HL7/VhDir/CapabilityStatement-vhdir-server.html)

### 3. Pharmacy Network Directory

The Pharmacy Network Directory API **SHALL** be provided as a sub-set of the Member-accessible Healthcare Directory.

#### CapabilityStatement

The Pharmacy Network Directory API can be exposed as a sub-set of the Healthcare Directory. The CapabilityStatement is detailed here: [http://build.fhir.org/ig/HL7/VhDir/CapabilityStatement-vhdir-server.html](http://build.fhir.org/ig/HL7/VhDir/CapabilityStatement-vhdir-server.html) 

### 4. Medication Formulary

When a Health Plan provides prescription drug coverage the list of covered medications is known as a "Formulary."  

The Health Plan formulary **SHALL** be provided as a Member-accessible API using the following FHIR resources:

- [MedicationKnowledge](https://build.fhir.org/medicationknowledge.html)
- [US Core Device Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-device.html)
- [VhDir Healthcare Service](http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-healthcareservice.html)
- [US Core Medication Profile](https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medication.html)

#### CapabilityStatement

The FHIR CapabilityStatement defines the resources and operations permitted on the resources exposed via the FHIR API.

The Permitted Operations for the FHIR Profiles covered in this payload section are defined as follows:

<table>
  <tr>
    <th> Resource Type </th>
    <th> Profile </th>
    <th> Read </th>
    <th> V-Read </th>
    <th> Search </th>
    <th> Update </th>
    <th> Create </th>
    <th> Updates </th>
    <th> History </th>
  </tr>
  <tr>
    <td>MedicationKnowledge</td>
    <td>https://build.fhir.org/medicationknowledge.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr> 
  <tr>
    <td>Device</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-device.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>HealthcareService</td>
    <td>http://build.fhir.org/ig/HL7/VhDir/StructureDefinition-vhdir-healthcareservice.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
  <tr>
    <td>Medication</td>
    <td>https://build.fhir.org/ig/HL7/US-Core-R4/StructureDefinition-us-core-medication.html</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
    <td></td>
    <td></td>
    <td></td>
    <td>Y</td>
  </tr>  
 
</table>

## Interaction Methods

The PDex IG specifies two interaction methods. Their use depends upon the Actors involved and the Data Payloads being exchanged.

The two interaction methods are:
1. CDS Hooks with SMART on FHIR
2. OAuth 2.0 and FHIR API

### 1. CDS Hooks with SMART on FHIR

Clinical systems will use the specification and workflows defined by [CDS Hooks](https://cds-hooks.hl7.org/) to initiate Coverage Requirements Discovery with the payers. Implementers must be familiar with all aspects of this specification.

SMART on FHIR is expected to be used in conjunction with CDS Hooks in two principle ways:

#### Ad-hoc PDex Member History Request

CDS Hooks provides a mechanism for providers/clinicians to request a medical history for their patient from the Health Plan as part of their regular workflow - when scheduling an appointment. However, sometimes clinicians may be interested updating the patient's medical history without going through the appointment booking steps within their EMR. I.e. They don’t want to actually create an appointment, they just want to ask the question “Has anything new happened to my patient at some other location?"

Sometimes clinicians want to check and update a patient's history, for example during a patient review, or responding to a question from a patient. The solution to this need it the use of a SMART on FHIR app that will invoke a CDS Hook. This is possible because many EMR systems provide support for SMART on FHIR. This use of SMART is distinct from the use of SMART in CDS Hooks. This isn't launching a SMART app based upon the contents of a returned card. Instead it is using SMART to invoke a CDS Hook in place of the EMR. It is emulating the workflow trigger that would normally trigger a hook within an EMR workflow.

The SMART on FHIR CDS Hook trigger approach was pioneered by the [Da Vinci Coverage Requirements Discovery IG](http://hl7.org/fhir/us/davinci%2Dcrd/2019May/) (CRD-IG). Developers interested in using this approach should refer to the CDS Hooks and SMART on FHIR sections of that IG for the latest guidance, exaamples and links to code samples. 

The PDex IG uses a similar approach to enable a CDS Hook. The CDS Hook used by PDex is:

- Appointment-book

 
#### Hook Actions

When a Health Plan server response to a CDS Hook, one of the possible actions is to allow the user to [invoke a SMART App](https://cds-hooks.org/specification/1.0/#link). Support for this option by Health Plan systems **SHOULD** be provided. The SMART on FHIR app provided as a link from the returned CDS Hook **SHOULD** enable a clinician to review the available Health Plan's data for their patient, select the data they want to commit to their EMR system and upon confirming their selection, enable the selected data to be written to the clinician's EMR system.

The [Da Vinci Documentation Templates and Rules Implementation Guide](http://www.hl7.org/fhir/us/davinci-dtr) (DTR-IG) provides additional guidance and expectations on the use of CDS Hook cards to launch SMART Apps and how payer-provided SMART Apps should function. 

### 2. OAuth2.0 and FHIR API

The well defined mechanism for enabling Member/Patient authorization to share information with an application using the FHIR API is to use OAuth2.0 as the Authorization protocol. The member **SHALL** authenticate using credentials they have been issued with by the Health Plan. This is typically the member's customer portal credentials.

After authenticating the Member **SHALL** be presented with an Authorization screen that enables them to approve the sharing of information with the Third Party, or new Health Plan, Application that has client application credentials registered with the Health Plan.

The Authorization screen **MAY** provide options to allow the Member to limit the information that is shared with the application. For example, this **MAY** enable the Member to withhold their demographic or behavioral health information. 

After successfully authorizing an application an Access Token and Optional Refresh Token **SHALL** be returned to the requesting application. 

The requesting application **SHALL** use the access token to access the Health Plan's secure FHIR API to download the information that the Member is allowed to access. 

## PDex Interaction and Payload Matrix

<table width="100%" cellspacing="2" cellpadding="2" border="1">
<tbody>
<tr>
<th> Interactions and Methods </th>
<th> Member History </th>
<th> Healthcare Directory </th>
<th> Pharmacy Directory </th>
<th> Medication Formulary </th>
</tr>
<tr>
<td valign="top">1. Provider and Health Plan (P2HPX) -
CDS-Hooks </td>
<td align="center" valign="top">Y<br>
</td>
<td valign="top"><br>
</td>
<td valign="top">&nbsp; </td>
<td valign="top"><br>
</td>
</tr>
<tr>
<td valign="top">2. Member-authorized Health Plan Exchange
(MauthHPX) - OAuth2.0 + FHIR </td>
<td align="center" valign="top">Y<br>
</td>
<td valign="top"><br>
</td>
<td valign="top"><br>
</td>
<td valign="top"><br>
</td>
</tr>
<tr>
<td valign="top">3. Member-authorized Health Plan to 3rd Party
Application (Mauth3PX) - OAuth2.0 + FHIR </td>
<td align="center" valign="top">Y<br>
</td>
<td align="center" valign="top">Y<br>
</td>
<td align="center" valign="top">Y<br>
</td>
<td align="center" valign="top">Y<br>
</td>
</tr>
<tr>
<td valign="top"><br>
</td>
<td valign="top"><br>
</td>
<td valign="top"><br>
</td>
<td valign="top"><br>
</td>
<td valign="top"><br>
</td>
</tr>
</tbody>
</table>


# Use Case Scenarios

This implementation guide addresses a Provider-to-Payer use cases:

- Patient at Primary Care Provider


The other use case is for Member/Patient-mediated Payer-to-Payer Exchange:

- Consumer enrolls with new health plan and accesses their prior health plan to authorize sharing of the health history that the prior health plan holds on the consumer.


The examples used in this guide are based on Payers providing claims from events where a member visits an ambulatory provider or when a member switches health plans.

 
<table style="background-color:rgb(195,231,244);width:100%">

<tr>
<td>Question_For_Comment(Q_F_02):</td>
<\tr>
<tr><td>
<i>
What other claims or categories of data available to payers should be converted to FHIR clinical resources to release to providers? <br/>
	In what sequence should these other categories of data be tackled?
</i>
</td></tr>	
</table>

 

Three example data requests from Providers to Health Plans are covered in this IG:

1. What Encounters has the patient had since mm/dd/yyyy, excluding encounters at my organization.
2. What procedures has the patient had?
3. What medications has the patient received (i.e. A claim for a medication has been settled by the health plan)

 
## Patient Personae
 
### Provider to Health Plan scenario:

Lauren Dent is a 62-year-old female, living in Wisconsin but she spends winters in Tampa Bay, FL.

Lauren works on a seasonal basis and has just accepted a new position with her employer and has moved to Madison, WI to live with her daughter, leaving her previous home in La Crosse, WI. As a result of the move she has selected a new Primary Care Provider.

Lauren is in reasonable health but is managing a number of conditions:

- She has been diagnosed as Pre-Diabetic and is being treated with medications.
- She is taking medication for hypertension.
- She had a knee replacement 5 years ago.
- She had a procedure seven years ago to correct a problem with a disc in her lower back.
- A history of a normal colonoscooy 5 years earlier
- A history of a pneumovax and zostavax 4 years earlier.

### Member/Patient-mediated Payer-to-Payer Exchange:
 
Arthur Dent is a 68 year old Male.

He has recently switched from Medicare Advantage Plan A and enrolled in Medicare Advantage Plan B.

In this scenario, Arthur has signed up for a new  Medicare advantage plan with payer C during the open enrollment period. Before the initiation of his coverage beginning January 1, payer C has established communication with the patient and has provided the patient with a secure log in to the payer C patient portal. Patient continues to have an active login to payer B patient portal.


# Provider-controlled Information Requests and Filtering

<table style="background-color:rgb(195,231,244);width:100%;">

<tr><td>Question_For_Comment (Q_F_05):</td></tr>
<tr><td>
    <i>
	How could Health Plan initiated data exchange be handled?
    </i>
</td></tr>
</table>

The Payer Data exchange Implementation Guide defines methods for Providers to request information from Payers.

This IG does not cover the Payer-initiated transfer of unsolicited information to a provider. All transfers will be initiated as part of a Provider workflow, such as when a new patient presents for an appointment, using CDS-Hooks.

All search parameters and subsequent filtering of returned information is controlled by the Provider making the information request.  The Payer does not filter information that has been requested by the provider.

# CDS Hooks

This section of the implementation guide defines the specific conformance requirements for systems wishing to conform to this Payer Data Exchange (PDex) Implementation Guide. The bulk of it focuses on the implementation of the CDS Hooks Specification to meet PDex use-cases. It also describes the use of SMART on FHIR and provides guidance on privacy, security and other implementation requirements.

The bulk of the functionality of this specification is implemented using CDS Hooks. The [Hooks specification](https://cds-hooks.org/) is small. Implementers should read and be familiar with all of it.

CDS Hooks is a relatively new technology. It is considered a Standard for Trial Use, meaning that it will continue to evolve based on implementer feedback and may change in ways that are not compatible with the current draft. As well, the initial version of the specification has focused on the core architecture and a relatively simple set of capabilities. Additional capabilities will be introduced in future versions.

To meet requirements identified by Da Vinci project participants, it is necessary to introduce some additional capabilities above and beyond what is currently found in the CDS Hooks specification. This section of the PDex implementation guide describes those additional capabilities and the mechanism the implementation guide proposes to implement them. The purpose of these customizations is to enable testing at connectathons and to support feedback into the CDS Hooks design process.

Each capability listed here has been proposed to the CDS Hooks community and may well become part of the official specification either in the initial release or in some future release. However, there is a significant likelihood that the manner in which the requirements are met may vary somewhat from a syntax or even an architectural approach. Future versions of this implementation guide will be updated to align with how these requirements are addressed in future versions of the CDS Hook specification. This implementation guide will not be able to be Normative (locked into backward compatibility mode) until the underlying CDS Hooks content is also normative.

This IG should be used in conjunction with the Da Vinci Health Record Exchange (HRex) Implementation Guide. The HRex IG defines CDS Hooks that are used across one or more Da Vinci Use Case-related IG. The PDex IG defines the payload(s) that are required to support each PDex use case using the relevant HRex defined Hooks.  

This implementation guide extends/customizes CDS Hooks in 4 ways: support for R4, extending the appointment-book hook, a hook configuration mechanism and additional response capabilities. Each are described below:

## Support for FHIR R4 

The hooks published in the CDS Hooks specification provide a list of context resources for the DSTU2 and STU3 versions of FHIR. The CDS Hook specification won't be updated to include R4 resources until after R4 is finalized. Because this implementation guide is being written to support FHIR R4 as well as STU3 and Argonaut (DSTU2), it provides guidance on what R4 resources are relevant for each hook (both pre-existing hooks as well as newly proposed hooks).

It is possible that the actual list of R4 resources provided for the hooks will differ from that proposed in this IG. Future versions of the implementation guide will adjust accordingly.

The CDS Hooks payload received from an EMR can include DSTU2, STU3 or R4 resources. The Payer's CDS Hooks service **SHALL** handle the content in the JSON hooks payload, regardless of version of FHIR used for incorporated resources.

The health plan's CDS Hooks service **SHALL** provide access to FHIR R4 resources based on Profiles identified in the US Core and Da Vinci HRex IGs.

The SMART-on-FHIR App that **MAY** be called from the returned CDS Hooks card will not translate R4 profiles to earlier versions of FHIR. When interacting with EMR systems that support FHIR versions prior to FHIR R4 the SMART App **SHALL** create a DocumentReference and encapsulate a PDF, human readable version of the records being committed, together with a document bundle that encapsulates the FHIR resources from the health plan that the provider has selected to commit to the patient's record.


## Additional Hooks

The base CDS hooks 1.0 specification defines the following hooks: 

- patient-view
- medication-prescribe
- order-review
- order-select
- order-sign
- appointment-book
- encounter-start
- encounter-discharge

The expectation is that new hooks will be defined by and eventually formally approved by the community. The formal process for this proposal and maturity development process is still evolving. Individuals interested in this process can provide feedback [here](https://cds-hooks.hl7.org).

Defining new hooks is an expected part of the CDS Hooks specification and there is no need for hooks to be officially registered with the community for them to be used. However, using registered hooks increases the likelihood of broad adoption by the community - which increases the likelihood of broad uptake of this implementation guide. The project is proposing hooks that build on proposals made in the Da Vinci CRD IG. 

## PDex Hook

Sharing of Member health information via PDex **SHALL** use the CDS Hooks specification. Connection to health plan systems **SHALL** be supported via the following hook:

- appointment-book

It is possible that this hook will change over the course of the review/approval process, including changes to the names of the hooks, their context parameters or other information. Future versions of this implementation guide will be updated to align with such changes. Additional hooks may also be added.

This IG defines an extension to the appointment-book hook. The additional optional context fields are:

- SubscirberId (optional): The number that identifies the unique person in the health plan system

NOTE: Even pre-existing hooks are not yet locked down as normative and similar changes are possible, though perhaps less likely.

A sample of the CDS Hook for appointment-book is included below:

<pre>
{
  "hookInstance": "d1577c69-dfbe-44ad-ba6d-3e05e953b2ea",
  "fhirServer": "http://fhir.example.com",
  "fhirAuthorization" : {
       "access_token" : "some-opaque-fhir-access-token",
       "token_type" : "Bearer",
       "expires_in" : 300,
       "scope" : "patient/Patient.read patient/Observation.read",
       "subject" : "cds-service4"
     },
  "hook": "appointment-book",
  "user": "Practitioner/example",
  "context": {
    "userId" : "Practitioner/A12365498",
    "patientId" : "EMR1239876",
    "encounterId" : "654",
    "appointments" : [],
    "subscriberId" : "HP567123489",
		}
  }
</pre>

## Hook Configuration

PDex supports three common scenarios:

- New Patient presents at Provider
- Patient returns to Provider
- Patient presents at Specialist

The hook interaction for these scenarios is:
* appointment-book

When a Card is returned from the CDS Hooks appointment-book service by a Health Plan it will provide the following elements:

- An Access Token for secure access to the Health Plan's FHIR API
- The URL for the Health Plan's FHIR API 
- A result code indicating the result of a Member Search
- The returned information **MAY** include a link to a SMART-on-FHIR App to enable selection of resources by the Clinician that will be written to the Clinician's EMR system
- An information card with a human readable interpretation of the Member Search Result
- The information card **MAY** include a link to launch the SMART-on-FHIR App using the Access Token and FHIR Endpoint address to enable the Clinician to query information about their patient using the Health Plan's FHIR API.
 

The SMART-on-FHIR App **MAY** be configured with default FHIR search queries that can be set by the Clinician, or their organization. 
 
 Examples of preset search queries parameters **MAY** include:
- Period (Start and optionally End date)
- Excluded Practitioner(s)
- Excluded Organization(s)
- Excluded Location(s)

The later three items are used to enable the Provider to exclude information that they may already have in their system.

## Systems

This implementation guide sets expectations for two types of systems:

- Client systems
- Payer systems

Client systems are electronic medical records, pharmacy systems and other clinical and administrative systems responsible for the ordering and execution of patient-related services. These are systems whose users have a need for discovery of patient information from health plans who have provided coverage to the patient.

Payer systems are systems run by health plans/insurers that provide insurance coverage to the patient and can provide claims history clinical information and benefits information about the patient.

The requirements and expectations described here are not intended to be exhaustive. Health plans and clients **MAY** support additional hooks, additional card patterns, additional resources, additional extensions, etc. The purpose of this implementation guide is to establish a baseline of expected behavior that communication partners can rely on and then build from. Future versions of this specification will evolve based on implementer feedback.


## Workflow Examples

### First Visit with new Provider
The patient calls their new provider to arrange for an annual physical.

The receptionist in the doctors office collects their personal information, health plan coverage information and creates an appointment, a patient record and an initial encounter record.  

The creation of an appointment activates a CDS Hook transaction: appointment-book. 

### Returning Visit with Provider

The patient calls their provider to arrange a follow-up appointment.

The receptionist in the doctors office collects their personal information, checks for any change in health plan coverage information and creates an appointment, a patient record and an initial encounter record.  

The creation of an appointment activates a CDS Hook transaction: appointment-book. 

In this scenario the Clinician that reviews the Member History is only interested in information in the Member record since their last visit and may also wnat to exclude information from their own organization, since that information will already be recorded in their EMR system.

### FHIR Profiles and CDS Hooks Context

The PDex IG makes significant use of established FHIR profiles. These **MAY** be qualified with search parameter definitions and terminology artifacts to describe the content to be shared as part of CDS Hook calls. The output from the CDS Hooks service will use FHIR R4 profiles identified in the US Core and Da Vinci HRex IGs.


The CDS Hooks Appointment-book call provides the Practitioner (UserId), Patient, Encounter identifiers and an appointments object.
Optional fields in the CDS Hooks for PDex context include:
- subscriberId
- accessJwt

The fields in the context of the CDS Hooks call are used as follows:
- userid: used to identify the provider requesting the information
- patientId: used to identify the patient/subject in the EMR system
- encounterid: used to identify the encounter in the provider's EMR
- subscriberId: used to describe the unique identifier for a health plan member. This identifier can be found in the Coverage resource as subscriber.id.
- accessJwt: Used to provide secure access into the Provider's EMR system in order to access the Patient record.

<pre>
{
  "hookInstance": "d1577c69-dfbe-44ad-ba6d-3e05e953b2ea",
  "fhirServer": "http://fhir.example.com",
  "fhirAuthorization" : {
       "access_token" : "some-opaque-fhir-access-token",
       "token_type" : "Bearer",
       "expires_in" : 300,
       "scope" : "patient/Patient.read patient/Observation.read",
       "subject" : "cds-service4"
     },
  "hook": "appointment-book",
  "user": "Practitioner/example",
  "context": {
    "userId": "Practitioner/A12365498",
    "patientId": "EMR1239876",
    "encounterId": "654",
    "appointments": [],
    "subscriberId": "HP567123489",
  }
}
</pre>


### SMART-on-FHIR app for Provider data selection

When a SMART-on-FHIR App is provided as a link in the content returned from the CDS Hooks it **SHALL** receive:

- The URL entrypoint to the Health Plan's FHIR API
- An access token to enable secure access to the Member's health history via the FHIR API
- An access token to enable the app to write data to the Provider's EMR system.


The SMART App **SHALL** retrieve the CapabilityStatement/Metadata from the Health Plan's FHIR API.
 
The SMART App **SHALL** retrieve the ConformanceStatement/CapabilityStatement/Metadata from the Provider's EMR system. 

The Provider **MAY** select records from the Health Plan's FHIR API to be committed to their EMR system.  After selecting the relevant data the provider **MAY** triggers a write of the selected data to their EMR system. 

The SMART App **SHALL** use the EMRs Metadata to determine what records **MAY** be written to the EMR system. 

The SMART App **SHALL** not convert records from one FHIR version to another.

If the Provider's EMR system does not support FHIR R4 the SMART App **MAY** create a DocumentReference record and incorporate a FHIR bundle of the selected records and a Human Readable PDF of the selected records and write the DocumentReference record to the Patient record in the EMR system, 
    
If the Provider's EMR system supports FHIR R4 the SMART App **SHALL** determine which resources may be written to the Patient's record in the EMR system. It will write these records to the EMR. Any remaining selected records, where write operations are not permitted by the EMR system's FHIR API **SHOULD** be placed in a FHIR bundle and a Human Readable PDF of those selected records **SHOULD** be generated and the bundle and PDf committed to the Patient's record in the EMR using a DocumentReference record.


## Providing Data Provenance

A Provenance resource should be provided with each resource provided by the Health Plan's FHIR API. This **SHOULD** be used to identify the source of the information. The Provenance resource **SHOULD** also identify whether the data came via a clinical record or a claim record or was subject to manual transcription or other interpretive transformation.

The Provenance record shall be populated as follows:


<table>
<tr>
	<th>Field</th>
	<th>Value</th>
</tr>
<tr>
	<td>occurredPeriod or occurredDataTime</td>	
		<td>dateTime or Period of the encounter/procedure/medication being provided</td>
</tr>
<tr>
	<td>recorded</td>
	<td>Time of this transaction</td>
</tr>
<tr>
	<td>agent.[0].type</td>
	<td>AMENDER (for conversion of claims data to clinical resources) | TRANS (for information taken from manual input)| REVIEWER (for clinical resources)</td>
</tr>
<tr>
	<td>agent.[0].role</td>
	<td>informant | custodian</td>
</tr>
<tr>
    <td>agent.[0].who</td>
	<td>Organization resource identifying the health plan</td>
</tr>
<tr>
	<td>agent.[1].type</td>	
	<td>SOURCE</td>
</tr>
<tr>
	<td>agent.[1].role</td>	
	<td>enterer | performer | author</td>
</tr>
<tr>
	<td>agent.[1].who</td>
	<td>Organization | Practitioner or other resource identifying the entity providing the source information</td>
</tr>
</table>


# Credits

Primary authors:

* Mark Scrimshire (NewWave Telecoms and Technologies)
* Tony Benson (Blue Cross Blue Shield of Alabama)

Project leads:

* Robert Dieterle (Enable Care, LLC)
* Viet Nguyen (Stratametrics, LLC)

Project management and coordination:
* Jocelyn Keegan (Point of Care Partners)
* Dana Marcalonis (Point of Care Partners)

Technical support and guidance:
* Rick Geimer (Lantana Consulting Group)

This implementation guide was the work of the Da Vinci Project PDex work group (http://www.hl7.org/about/davinci/index.cfm?ref=common) and the member organizations.

Project participants included:

* Aegis (Richard Ettema, Sandra Vance)
* Allscripts (Emma Jones, Jeffrey Danford)
* Blue Cross Blue Shield of Alabama (Tony Benson, Kevin Lambert, Gini McGlothin, Morry Payne, Clarissa Winchester)
* Cerner (Hans Buitendijk, Kevin Shekleton, Michelle Miller)
* Epic (Danielle Friend, Isaac Vetter)
* Health Care Data Standards (Mary Kay McDaniel)
* Optum (Linda Michaelsen, Nicholas Radov)
* Newwave (Mark Scrimshire, Santhi Chebrolu)

Our thanks to these and to the many others not explicitly listed who contributed their time, enthusiasm and expertise to this work.

