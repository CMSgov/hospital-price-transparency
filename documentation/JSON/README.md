### Hospital Machine-Readable JSON Schema
The following is documentation for those who wish to build a JSON file to satisfy [45 CFR 180.50](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180/subpart-B/section-180.50) requirements. This documentation has information in how to disclose data elements for the [JSON schema](https://github.com/CMSgov/hospital-price-transparency/blob/master/documentation/JSON/V2.0.0_Hospital_price_transparency_schema.json).

General JSON Instructions
=========================
Developers of MRFs should generally consider and adopt established standards and industry norms for JSON files when creating the MRF. For more information on the JSON schema standards visit https://www.json.org/json-en.html, https://json-schema.org/. Additional details and instructions specific to JSON may be found in the [JSON schema](https://github.com/CMSgov/hospital-price-transparency/blob/master/documentation/JSON/V2.0.0_Hospital_price_transparency_schema.json). Below are additional reminders to avoid common errors in MRFs:
* Encode valid values as instructed below. Values encoded incorrectly will generate a deficiency. For example, insert numeric values only for Payer-Specific Negotiated Charge: Dollar Amount; inserting a  dollar sign with a number will generate a deficiency.
* Hospitals are permitted to include additional information through optional data elements that are defined in the data dictionary (e.g., billing class and hospital financial aid policy) or hospital created data attributes. Follow the technical instructions for the defined optional data elements and where to insert hospital defined optional data elements.
* All "Numeric" data elements must be positive numbers. Entering a negative number or "0" will generate a deficiency.

### JSON Data Attributes
The root object contains general data attributes (meta-data) about the hospital and the data being disclosed about the hospital and MRF.

| Attribute                       | Name                           | Type   | Description                                                                                                                                                                                                     | Required |
|---------------------------------|--------------------------------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **hospital_name**               | Hospital Name                  | String | The legal business name of the hospital associated with the file.                                                                                                                                               | Yes      |
| **last_updated_on**             | MRF Date                       | Date   | Date on which the MRF was last updated. Date must be in an ISO 8601 format (i.e. YYYY-MM-DD)                                                                                                                    | Yes      |
| **version**                     | CMS Template Version           | String | The version of the schema.                                                                                                                                                                                      | Yes      |
| **hospital_location**           | Hospital Location(s)           | Array  | An array of strings of the unique name of the hospital location absent any acronyms.                                                                                                                            | Yes      |
| **hospital_address**            | Hospital Address(es)           | Array  | An array of strings of the physical address(es) of the corresponding hospital location attribute. Address(es) must be included for, at minimum, all inpatient facilities and stand-alone emergency departments. | Yes      |
| **license_information**         | Hospital Licensure Information | Object | The [hospital licensure object](#hospital-licensure-object) contains license information for the reported hospital.                                                                                             | Yes      |
| **affirmation**                 | Affirmation Statement          | Object | The [affirmation object](#affirmation-object) contains the CMS defined affirmation statement that the information displayed is true, accurate, and complete as of the date indicated in the file.               | Yes      |
| **standard_charge_information** | Standard Charge Information    | Array  | This array contains a list of the [standard charge information objects](#standard-charge-information-object) for all of the items and services that are required to be disclosed.                               | No       |
| **modifier_information**        | Modifier Information           | Array  | An array of [modifier information objects](#modifier-information-object).                                                                                                                                       | No       |

#### Affirmation Object

| Attribute               | Name                | Type    | Description                                                                          | Required |
|-------------------------|---------------------|---------|--------------------------------------------------------------------------------------|----------|
| **affirmation**         | Affirmation         | String  | This attribute is required to contain the [valid text only](#affirmation-statement). | Yes      |
| **confirm_affirmation** | Confirm Affirmation | Boolean | A "true" or "false" value to be entered by the hospital.                             | Yes      |

##### Affirmation Statement
The following object requires the following statement for the `affirmation` attribute:
> To the best of its knowledge and belief, the hospital has included all applicable standard charge information in accordance with the
 requirements of 45 CFR 180.50, and the information encoded is true, accurate, and complete as of the date indicated.

An [example](../../examples/JSON/V2.0.0_JSON_Format_Example.json) of this would be:
```json
{
 "affirmation": "To the best of its knowledge and belief, the hospital has included all applicable standard charge information in accordance with the requirements of 45 CFR 180.50, and the information encoded is true, accurate, and complete as of the date indicated.",
 "confirm_affirmation": true
 }
```

#### Hospital Licensure Object

| Attribute          | Name           | Type   | Description                                                                                       | Required |
|--------------------|----------------|--------|---------------------------------------------------------------------------------------------------|----------|
| **license_number** | License Number | String | The hospital license number. If the hospital does not have a license number, omit this attribute. | No       |
| **state**          | State          | Enum   | The two-letter state code (e.g. CA, NY).                                                          | Yes      |

#### Standard Charge Information Object

| Attribute            | Name                | Type   | Description                                                                                                                                 | Required |
|----------------------|---------------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **description**      | General Description | String | The description of the item or service that corresponds to the standard charge the hospital has established.                                | Yes      |
| **drug_information** | Rx Drug Information | Object | The [drug information object](#drug-information-object) that contains the type and units of a drug disclosure                               | No       |
| **code_information** | Code Information    | Array  | An array of [code information objects](#code-information-object) that contains information about accounting or billing codes                | Yes      |
| **standard_charges** | Standard Charges    | Array  | An array of [standard charge objects](#standard-charge-object) that contain information about the standard charge for each item and service | Yes      |

#### Drug Information Object

| Attribute | Name | Type   | Description                                                                                                                                                                                                                                                 | Required |
|-----------|------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **unit**  | Unit | String | The unit value that corresponds to the established standard charge for drugs.                                                                                                                                                                               | Yes      |
| **type**  | Type | Enum   | The measurement type that corresponds to the established standard charge for drugs as defined by either the National Drug Code or the National Council for Prescription Drug Programs. The [list](#additional-notes-for-drug-types-values) of valid values. | Yes      |

#### Code Information Object

| Attribute | Name | Type   | Description                                                                                                                               | Required |
|-----------|------|--------|-------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **code**  | Code | String | Any code used by the hospital for purposes of billing or accounting for the item or service.                                              | Yes      |
| **type**  | Type | Enum   | The associated coding type for the ‘Code’ data element. Please see a list of the [valid values](#additional-notes-concerning-code-types). | Yes      |

#### Standard Charge Object

| Attribute                    | Name                     | Type    | Description                                                                                                                                                                      | Required |
|------------------------------|--------------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **minimum**                  | Minimum                  | Numeric | De-identified minimum negotiated charge is the lowest charge that a hospital has negotiated with all third-party payers for an item or service.                                  | No       |
| **maximum**                  | Maximum                  | Numeric | De-identified maximum negotiated charge is the highest charge that a hospital has negotiated with all third-party payers for an item or service.                                 | No       |
| **gross_charge**             | Gross Charge             | Numeric | Gross charge is the charge for an individual item or service that is reflected on a hospital’s chargemaster, absent any discounts.                                               | No       |
| **discounted_cash**          | Discounted Cash          | Numeric | Discounted cash price is defined as the charge that applies to an individual who pays cash (or cash equivalent) for a hospital item or service.                                  | No       |
| **setting**                  | Setting                  | Enum    | The place where the item or service is provided for the associated standard charge amount. Valid values: "inpatient", "outpatient", "both".                                      | Yes      |
| **payers_information**       | Payer Information        | Array   | An array of [payers information objects](#payers-information-object) that describe the standard charges specific to each payer for each item and service.                        | No       |
| **additional_generic_notes** | Additional Generic Notes | String  | A free text data element to help explain any of the data including charity care policies or other contextual information that aids in the comprehension of the standard charges. | No       |

#### Modifier Information Object

| Attribute                      | Name                       | Type   | Description                                                            | Required |
|--------------------------------|----------------------------|--------|------------------------------------------------------------------------|----------|
| **description**                | Description                | String | The common name of the modifier                                        | Yes      |
| **code**                       | Code                       | String | The modifier code (e.g. 50)                                            | Yes      |
| **modifier_payer_information** | Modifier Payer Information | Array  | An array of [modifier payer information](#modifier-payer-information). | Yes      |

#### Modifier Payer Information

| Attribute       | Name        | Type   | Description                                                                                                                                                                     | Required |
|-----------------|-------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **payer_name**  | Payer Name  | String | The name of the third-party payer that is, by statute, contract, or agreement, legally responsible for payment of a claim for a healthcare item or service.                     | Yes      |
| **plan_name**   | Plan Name   | String | The name of the payer’s specific plan associated with the standard charge.                                                                                                      | Yes      |
| **description** | Description | String | Description of how the modifier(s) may change the standard charge that corresponds to hospital item or services (e.g., modifier applies 150% change to standard charge amount). | Yes      |

#### Payers Information Object

| Attribute                      | Name                                            | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                              | Required |
|--------------------------------|-------------------------------------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **payer_name**                 | Payer Name                                      | String  | The name of the third-party payer that is, by statute, contract, or agreement, legally responsible for payment of a claim for a healthcare item or service.                                                                                                                                                                                                                                              | Yes      |
| **plan_name**                  | Plan Name                                       | String  | The name of the payer’s specific plan associated with the standard charge.                                                                                                                                                                                                                                                                                                                               | Yes      |
| **additional_payer_notes**     | Additional Payer Notes                          | String  | A free text data element used to help explain data in the file that is related to a payer-specific negotiated charge.                                                                                                                                                                                                                                                                                    | No       |
| **standard_charge_dollar**     | Payer-Specific Negotiated Charge: Dollar Amount | Numeric | Payer-specific negotiated charge (expressed as a dollar amount) that a hospital has negotiated with a third-party payer for the corresponding item or service.                                                                                                                                                                                                                                           | No       |
| **standard_charge_percentage** | Payer-Specific Negotiated Charge: Percentage    | Numeric | Payer-specific negotiated charge (expressed as a percentage) that a hospital has negotiated with a third-party payer for an item or service. See [additional percentage notes](#additional-notes-for-percentage)                                                                                                                                                                                         | No       |
| **standard_charge_algorithm**  | Payer-Specific Negotiated Charge: Algorithm     | String  | Payer-specific negotiated charge (expressed as an algorithm) that a hospital has negotiated with a third-party payer for the corresponding item or service.                                                                                                                                                                                                                                              | No       |
| **estimated_amount**           | Estimated Amount                                | Numeric | Estimated allowed amount means the average dollar amount that the hospital estimates it will be paid by a third party payer for an item or service. If the standard charge is based on a percentage or algorithm, the MRF must also specify the estimated allowed amount for that item or service. See [additional estimated amount notes](#additional-notes-for-estimated_amount) for more information. | No       |
| **methodology**                | Standard Charge Methodology                     | Enum    | The type of contract arrangement associated with the payer-specific negotiated charge. See [additional standard charge methodology notes](#additional-standard-charge-methodology-notes) notes for more information on the valid values.                                                                                                                                                                 | Yes      |

##### Additional Notes for percentage

This data element should be encoded only when the payer-specific negotiated charge has been established as a percentage and no dollar amount can be calculated. This data element will contain the numeric representation of the percentage not as a decimal (70.5% is to be entered as “70.5” and not “.705”). If you encode information for this data element, you must also calculate and display the estimated allowed amount for that item or service as a separate data element.

##### Additional Notes for `estimated_amount`
CMS recommends that the hospital encode 999999999 (nine 9s) in the data element value to indicate that there is not sufficient historic claims history to derive the estimated allowed amount, and then update the file when sufficient history is available. As a guide for the threshold for sufficient history, we suggest hospitals use [the CMS Cell Suppression Policy](https://www.hhs.gov/guidance/document/cms-cell-suppression-policy) established in January, 2020. Additionally if the hospital wishes to provide further context for the lack of data they can do so in the appropriate additional notes field.

##### Additional Notes for `Drug Types` Values
The following valid values for `type` are based on two sets of industry standards; National Drug Code and National Council for Prescription Drug Programs.

| Standard Name | Reporting Value | 
| ------------- | --------------- | 
| GR | Grams |
| ME | Milligrams |
| ML | Milliliters | 
| UN | Unit | 
| F2 | International Unit | 
| EA | Each | 
| GM | Gram | 


##### Additional Notes Concerning Code Types
Hospital items and services may be associated with a variety of billing codes or accounting codes. Examples include Current Procedural Terminology (CPT), Healthcare Common Procedure Coding System (HCPCS), National Drug Code (NDC), Revenue Center (RC) code, or other common payer identifier. The list of valid values is in the following table with the name of the standard and the associated valid values.

The value "LOCAL" may be used for internal accounting codes in conjunction with another billing code for that item or service. However, if no other code types are available for a particular item or service, "LOCAL" may be used as a valid value.

| Standard Name | Reporting Value |
| ------------- | --------------- |
| Current Procedural Terminology | CPT |
| National Drug Code | NDC |
| Healthcare Common Procedural Coding System | HCPCS |
| Revenue Code | RC |
| International Classification of Diseases | ICD |
| Diagnosis Related Groups | DRG |
| Medicare Severity Diagnosis Related Groups | MS-DRG |
| Refined Diagnosis Related Groups | R-DRG |
| Severity Diagnosis Related Groups | S-DRG |
| All Patient, Severity-Adjusted Diagnosis Related Groups | APS-DRG |
| All Patient Diagnosis Related Groups | AP-DRG | |
| All Patient Refined Diagnosis Related Groups | APR-DRG |
| Ambulatory Payment Classifications | APC |
| Local Code Processing | LOCAL |
| Enhanced Ambulatory Patient Grouping | EAPG |
| Health Insurance Prospective Payment System | HIPPS |
| Current Dental Terminology | CDT |
| Charge Description Master (chargemaster) | CDM |
| TriCare Diagnosis Related Groups | TRIS-DRG |

 ##### Additional Standard Charge Methodology Notes
The `methodology` data element describes the method used by the hospital to establish a payer-specific negotiated charge. Below are descriptions for the valid values for the `methodology` data element and illustrative examples for how to represent unique contracting scenarios in combination with other data elements.

* `case rate`: A flat rate for a package of items and services triggered by a diagnosis, treatment, or condition for a designated length of time.
* `fee schedule`: The payer-specific negotiated charge is based on a fee schedule. Examples of common fee schedules include Medicare, Medicaid, commercial payer, and workers compensation. The dollar amount that is based on the indicated fee schedule should be encoded into the `Payer-specific Negotiated Charge: Dollar Amount` data element. For standard charges based on a percentage of a known fee schedule, the dollar amount should be calculated and encoded in the `Payer-specific Negotiated Charge: Dollar Amount` data element. 
* `percent of total billed charges`: The payer-specific negotiated charge is based on a percentage of the total billed charges for an item or service. This percentage may vary depending on certain pre-determined criteria being met.
* `per diem`: The per day charge for providing hospital items and services.
* `other`: If the standard charge methodology used to establish a payer-specific negotiated charge cannot be described by one of the types of standard charge methodology above, select ‘other’ and encode a detailed explanation of the contracting arrangement in the `additional_payer_notes` data attribute.

### Optional Data Attributes
Two additional data attributes: `financial_aid_policy` and `billing_class` are optional data attributes. They are not required to be included but instructions have been added to support standardization of disclosure of these data attributes for hospitals that wish to provide more contextual information about their charges. If `financial_aid_policy` is included in the MRF, it is to be included to the [root node](#json-data-attributes). If `billing_class` attribute is included in the MRF, it is to be added to the [standard charge object](#standard-charge-object).

| Attribute                | Name                          | Type   | Description                                                                                                                                   | Required |
|--------------------------|-------------------------------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **financial_aid_policy** | Hospital Financial Aid Policy | String | The hospital’s financial aid policy. See [additional financial aid policy notes](#additional-notes-on-financial_aid_policy) for more details. | No       |
| **billing_class**        | Billing Class                 | Enum   | The type of billing for the item/service at the established standard charge. The valid values are "professional", "facility", and "both".     | No       |

#### Additional Notes on `financial_aid_policy`
The hospital’s financial aid policy, also known as charity care or bill forgiveness, that a hospital may choose or be required to apply to a particular individual’s bill. This information may be displayed as either a description or as a link to the financial aid or cash price policy on the hospital’s website.
