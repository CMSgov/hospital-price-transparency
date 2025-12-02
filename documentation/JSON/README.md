# **Hospital Price Transparency JSON Data Dictionary v3.0**

The v3.0 data dictionary includes formatting updates and new regulatory requirements from the Calendar Year 2026 Hospital Outpatient Prospective Payment and Ambulatory Surgical Center Payment System final rule with comment period ([CY 2026 OPPS/ASC Final Rule](https://www.federalregister.gov/documents/2025/11/25/2025-20907/medicare-program-hospital-outpatient-prospective-payment-and-ambulatory-surgical-center-payment)) that are effective January 1, 2026, with CMS enforcement beginning April 1, 2026.

Review this entire data dictionary for how to disclose data elements in JSON and find the [JSON schemas here](./schemas) to begin building your hospital machine readable file (MRF). For an explanation of how to interpret the data element tables, review the [How to Read the Data Dictionary Tables](../HOW_TO_READ_DATA_DICTIONARY.md) information.

## **General JSON Instructions**

Developers of MRFs should generally consider and adopt established standards and industry norms for JSON files when creating the MRF. For more information on the JSON schema standards, visit <https://www.json.org/json-en.html> and <https://json-schema.org/>. Additional details and instructions specific to JSON may be found in the [JSON schema](./schemas). Below are additional reminders to avoid common errors in MRFs:

- Encode valid values as instructed below. Values encoded incorrectly will generate a deficiency. For example, insert numeric values only for Payer-Specific Negotiated Charge: Dollar Amount; inserting a dollar sign with a number will generate a deficiency.
- Hospitals are permitted to include additional information through optional data elements that are defined in the data dictionary (e.g., billing class and hospital financial aid policy) or hospital created data attributes. Follow the technical instructions for the defined optional data elements and where to insert hospital defined optional data elements.
- All "Numeric" data elements must be positive numbers unless otherwise specified. Entering a negative number or "0" will generate a deficiency for these elements.
- Ensure all [conditional requirements](#conditional-requirements) are met for an MRF to be considered valid

## **JSON Data Attributes**

The root object contains general data attributes (meta-data) about the hospital and the data being disclosed about the hospital and MRF.

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **hospital_name** | Hospital Name | String | The legal business name of the hospital associated with the file. | Yes |
| **last_updated_on** | MRF Date | Date | Date on which the MRF was last updated. Date must be in an ISO 8601 format (i.e. YYYY-MM-DD) | Yes |
| **version** | CMS Template Version | String | The version of the schema. | Yes |
| **location_name** | Hospital Location(s) | Array | An array of strings of the unique name(s) of the hospital location(s) absent any acronyms. | Yes |
| **hospital_address** | Hospital Address(es) | Array | An array of strings of the physical address(es) of the corresponding hospital location attribute. Address(es) must be included for, at minimum, all inpatient facilities and stand-alone emergency departments. | Yes |
| **license_information** | Hospital Licensure Information | Object | The [hospital licensure object](#hospital-licensure-object) contains license information for the reported hospital. | Yes |
| **attestation** | Attestation Statement | Object | The [attestation object](#attestation-object) contains the CMS defined attestation statement that the information displayed is true, accurate, and complete as of the date indicated in the file. | Yes |
| **standard_charge_information** | Standard Charge Information | Array | This array contains a list of the [standard charge information objects](#standard-charge-information-object) for all of the items and services that are required to be disclosed. | Yes |
| **modifier_information** | Modifier Information | Array | An array of [modifier information objects](#modifier-information-object). | No |
| **type_2_npi** | Type 2 Organizational NPI(s) | Array | An array for strings of the type 2 NPI(s) for all hospital locations whose data is represented in the file. Only certain type 2 NPIs are required to be reported, see [additional type 2 NPI notes](#additional-notes-for-type-2-organizational-npis). | Yes |

### Additional Notes for Type 2 Organizational NPI(s)

Include the hospital and all corresponding hospital locations represented in the MRF's Type 2 NPI(s) that are associated with the primary taxonomy code starting with '28' (indicating hospital) or '27' (indicating hospital unit) and that is active as of the date of the most recent update to the standard charge information. Primary taxonomy codes beginning with '28' represent hospitals, and primary taxonomy codes that begin with '27' represent hospital units. Hospitals are only required to report their Type 2 NPIs, not the taxonomy codes. Hospitals should include all active Type 2 NPIs meeting this criteria and exclude all type 2 NPIs with a taxonomy other than '28' and '27'.

## Attestation Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | --- |
| **attestation** | Attestation | String | > This attribute is required to contain the [valid text only](#attestation-statement). | Yes |
| **confirm_attestation** | Confirm Attestation | Boolean | > A "true" or "false" value to be entered by the hospital. | Yes |
| **attester_name** | Attester Name | String | > The first and last name of the hospital chief executive officer, president, or senior official designated to oversee the encoding of true, accurate, and complete data in the MRF. | Yes |

### Attestation Statement

Hospitals should encode the necessary information available to the hospital for the public to be able to derive the dollar amount, including, but not limited to, the specific fee schedule or components referenced in such percentage, algorithm or formula in the standard charge data elements, and the additional notes data elements.

The following object requires the following statement for the "Attestation" attribute:

> To the best of its knowledge and belief, this hospital has included all applicable standard charge information in accordance with the requirements of 45 CFR 180.50, and the information encoded is true, accurate, and complete as of the date in the file. This hospital has included all payer-specific negotiated charges in dollars that can be expressed as a dollar amount. For payer-specific negotiated charges that cannot be expressed as a dollar amount in the machine-readable file or not knowable in advance, the hospital attests that the payer-specific negotiated charge is based on a contractual algorithm, percentage or formula that precludes the provision of a dollar amount and has provided all necessary information available to the hospital for the public to be able to derive the dollar amount, including, but not limited to, the specific fee schedule or components referenced in such percentage, algorithm or formula.

While "true" or "false" is accepted from a form and manner perspective, a value of "true" is required to meet the attestation regulatory requirement (45 CFR 180.50(a)(3)).

An [example](../../examples/JSON/V3.0.0_JSON_Format_Example.json) of this would be:

    {
      "attestation": "To the best of its knowledge and belief, this hospital has included all applicable standard charge information in accordance with the requirements of 45 CFR 180.50, and the information encoded is true, accurate, and complete as of the date in the file. This hospital has included all payer-specific negotiated charges in dollars that can be expressed as a dollar amount. For payer-specific negotiated charges that cannot be expressed as a dollar amount in the machine-readable file or not knowable in advance, the hospital attests that the payer-specific negotiated charge is based on a contractual algorithm, percentage or formula that precludes the provision of a dollar amount and has provided all necessary information available to the hospital for the public to be able to derive the dollar amount, including, but not limited to, the specific fee schedule or components referenced in such percentage, algorithm or formula.",
      "confirm_attestation": true,
      "attester_name": "Leigh Attester"
    }

## Hospital Licensure Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **license_number** | License Number | String | The hospital license number. If the hospital does not have a license number, omit this attribute. | No |
| **state** | State | Enum | The two-letter state code (e.g. CA, NY). | Yes |

## Standard Charge Information Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **description** | General Description | String | The description of the item or service that corresponds to the standard charge the hospital has established. | Yes |
| **drug_information** | Rx Drug Information | Object | The [drug information object](#drug-information-object) that contains the type and units of a drug disclosure | No |
| **code_information** | Code Information | Array | An array of [code information objects](#code-information-object) that contain information about accounting or billing codes | Yes |
| **standard_charges** | Standard Charges | Array | An array of [standard charge objects](#standard-charge-object) that contain information about the standard charge for each item and service | Yes |

## Drug Information Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **unit** | Unit | Numeric | The unit value that corresponds to the established standard charge for drugs. | Yes |
| **type** | Type | Enum | The measurement type that corresponds to the established standard charge for drugs as defined by either the National Drug Code or the National Council for Prescription Drug Programs. The [list](#additional-notes-for-drug-types-values) of valid values. | Yes |

## Code Information Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **code** | Code | String | Any code used by the hospital for purposes of billing or accounting for the item or service. | Yes |
| **type** | Type | Enum | The associated coding type for the 'Code' data element. Please see a list of the [valid values](#additional-notes-concerning-code-types). | Yes |

## Standard Charge Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **minimum** | Minimum | Numeric | De-identified minimum negotiated charge is the lowest charge that a hospital has negotiated with all third-party payers for an item or service. This is determined from the set of negotiated standard charge dollar amounts. | No |
| **maximum** | Maximum | Numeric | De-identified maximum negotiated charge is the highest charge that a hospital has negotiated with all third-party payers for an item or service. This is determined from the set of negotiated standard charge dollar amounts. | No |
| **gross_charge** | Gross Charge | Numeric | Gross charge is the charge for an individual item or service that is reflected on a hospital's chargemaster, absent any discounts. | No |
| **discounted_cash** | Discounted Cash | Numeric | Discounted cash price is defined as the charge that applies to an individual who pays cash (or cash equivalent) for a hospital item or service. | No |
| **setting** | Setting | Enum | Indicates whether the item or service is provided in connection with an inpatient admission or an outpatient department visit. Valid values: "inpatient", "outpatient", "both". | Yes |
| **modifier_code** | Modifier Code | Array | An array of strings, each of which should be a modifier code present in a Modifier Information object. | No |
| **payers_information** | Payer Information | Array | An array of [payers information objects](#payers-information-object) that describe the standard charges specific to each payer for each item and service. | No |
| **additional_generic_notes** | Additional Generic Notes | String | A free text data element to help explain any of the data including, for example, lack of applicable data, charity care policies or other contextual information that aids in the comprehension of the standard charges. | No |

## Modifier Information Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | --- |
| **description** | Description | String | The common name of the modifier | Yes |
| **code** | Code | String | The modifier code (e.g. 50) | Yes |
| **modifier_payer_information** | Modifier Payer Information | Array | An array of [modifier payer information](#modifier-payer-information). | Yes |
| **setting** | Setting | Enum | The place where an item or service is provided and the modifier is applicable. Valid values: "inpatient", "outpatient", "both". | No |

## Modifier Payer Information

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **payer_name** | Payer Name | String | The name of the third-party payer that is, by statute, contract, or agreement, legally responsible for payment of a claim for a healthcare item or service. | Yes |
| **plan_name** | Plan Name | String | The name of the payer's specific plan associated with the standard charge. | Yes |
| **description** | Description | String | Description of how the modifier(s) may change the standard charge that corresponds to hospital item or services (e.g., modifier applies 150% change to standard charge amount). | Yes |

## Payers Information Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **payer_name** | Payer Name | String | The name of the third-party payer that is, by statute, contract, or agreement, legally responsible for payment of a claim for a healthcare item or service. | Yes |
| **plan_name** | Plan Name | String | The name of the payer's specific plan associated with the standard charge. | Yes |
| **additional_payer_notes** | Additional Payer Notes | String | A free text data element used to help explain data in the file that is related to a payer-specific negotiated charge. | No |
| **standard_charge_dollar** | Payer-Specific Negotiated Charge: Dollar Amount | Numeric | Payer-specific negotiated charge (encoded as a dollar amount) that a hospital has negotiated with a third-party payer for the corresponding item or service. | No |
| **standard_charge_percentage** | Payer-Specific Negotiated Charge: Percentage | Numeric | Payer-specific negotiated charge (encoded as a percentage) that a hospital has negotiated with a third party payer for an item or service. See [additional percentage notes](#additional-notes-for-standard-charge-percentage-and-algorithm) | No |
| **standard_charge_algorithm** | Payer-Specific Negotiated Charge: Algorithm | String | Payer-specific negotiated charge (encoded as an algorithm) that a hospital has negotiated with a third party payer for the corresponding item or service. | No |
| **median_amount** | Median Allowed Amount | Numeric | Median allowed amount means the median of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. If the payer-specific negotiated charge is based on a percentage or algorithm, the MRF must also specify the median allowed amount for that item or service. See additional allowed amount notes for more information. | No |
| **10th_percentile** | 10th Percentile Allowed Amount | Numeric | Tenth (10th) percentile allowed amount means the 10th percentile of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. If the payer-specific negotiated charge is based on a percentage or algorithm, the MRF must also specify the 10th percentile allowed amount for that item or service. See additional allowed amount notes for more information. | No |
| **90th_percentile** | 90th Percentile Allowed Amount | Numeric | Ninetieth (90th) percentile allowed amount means the 90th percentile of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. If the payer-specific negotiated charge is based on a percentage or algorithm, the MRF must also specify the 90th percentile allowed amount for that item or service. See additional allowed amount notes for more information. | No |
| **count** | Count of Allowed Amounts | String | Count of remittances used to calculate the allowed amounts. Allowed values are "0", "1 through 10", and whole numbers 11 and greater absent any thousands separator. See additional notes for Count of Allowed Amounts for more information. | No |
| **methodology** | Standard Charge Methodology | Enum | Method used to establish the payer-specific negotiated charge. The valid value corresponds to the contract arrangement. See [additional standard charge methodology notes](#additional-standard-charge-methodology-notes) for more information on the valid values. | Yes |

While each of the three payer-specific charge properties are optional, at least one of them must be encoded in each Payers Information object.

### Additional Notes for Standard Charge Percentage and Algorithm

If a payer-specific negotiated charge dollar can be calculated, for example if the payer-specific negotiated charge is 70% of a known fee schedule, calculate the dollar amount and encode the "Payer-Specific Negotiated Charge Dollar" data element. If the payer-specific negotiated charge is a percentage for which a dollar amount cannot be calculated or is a base rate modified by a percentage, encode the "Payer-Specific Negotiated Charge Percentage" data element. This data element will contain the numeric representation of the percentage, not as a decimal (70.5% is to be entered as "70.5" and not ".705").

If the "Payer-Specific Negotiated Charge: Percentage" or "Payer-Specific Negotiated Charge: Algorithm" data elements are encoded, then also encode the corresponding allowed amounts and count of allowed amount data elements for that item or service.

### Additional Allowed Amount Notes

If the payer-specific negotiated charge for an item or service is based on a percentage or algorithm, the MRF must also specify the median, 10th percentile, and 90th percentile allowed amounts for that item or service. Hospitals must use EDI 835 ERA transaction data or an alternative equivalent source of remittance data that includes the same information as EDI 835 ERA transaction data would include, to calculate and encode the allowed amounts.

The allowed amounts are the specified percentile (median, 10th percentile, or 90th percentile) of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. The total allowed amount should reflect the total amount the hospital was reimbursed for the item or service (or service package). The total allowed amount is derived from the gross charge minus contractual adjustments and consists of the portion billed to a payer for a particular plan and the portion, if any, billed to the patient.

When calculating the allowed amounts, if the calculated percentile falls between two observed allowed amounts (in other words, where the total count, n, is an even number), the allowed amount will be the next highest observed value. Hospitals should exclude \$0 dollar remittances when calculating and encoding the allowed amounts. If the count of allowed amounts is zero, do not encode these data elements.

### Additional Notes for Count of Allowed Amounts

Encode the total number of allowed amount remittances from the EDI 835 ERA transaction data or an alternative, equivalent source of remittance data used to calculate the median, 10th percentile, and 90th percentile allowed amounts. If the total number of remittances is 11 or greater, encode the value as digits absent any thousands separator. For example, "2,025" includes a thousands separator and is not accepted. If the number of remittances is greater than 0 but less than 11, encode "1 through 10". If there are no remittances for the time period of no less than 12 months and no more than 15 months, encode "0" in the "Count of Allowed Amounts" and in the "Additional Generic Notes" in the CSV Tall and the "Additional Payer-Specific Notes" in the CSV Wide explain why there is no remittances.

### Additional Notes for Drug Type Of Measurement Values

The following valid values for "Type" are based on two sets of industry standards; National Drug Code and National Council for Prescription Drug Programs.

| **Standard Name**  | **Valid Value** |
| ------------------ | --------------- |
| Grams              | GR              |
| Milligrams         | ME              |
| Milliliters        | ML              |
| Unit               | UN              |
| International Unit | F2              |
| Each               | EA              |
| Gram               | GM              |

### Additional Notes Concerning Code Types

Hospital items and services may be associated with a variety of billing codes or accounting codes. Examples include Current Procedural Terminology (CPT), Healthcare Common Procedure Coding System (HCPCS), National Drug Code (NDC), Revenue Center (RC) code, or other common payer identifier. The list of valid values is in the following table with the name of the standard and the associated valid values.

The value "LOCAL" may be used for internal accounting codes in conjunction with another billing code for that item or service. However, if no other code types are available for a particular item or service, "LOCAL" may be used as a valid value.

| **Standard Name**                                         | **Valid Value** |
| --------------------------------------------------------- | --------------- |
| Current Procedural Terminology                            | CPT             |
| National Drug Code                                        | NDC             |
| Healthcare Common Procedural Coding System                | HCPCS           |
| Revenue Code                                              | RC              |
| International Classification of Diseases                  | ICD             |
| Diagnosis Related Groups                                  | DRG             |
| Medicare Severity Diagnosis Related Groups                | MS-DRG          |
| Refined Diagnosis Related Groups                          | R-DRG           |
| Severity Diagnosis Related Groups                         | S-DRG           |
| All Patient, Severity-Adjusted Diagnosis Related Groups   | APS-DRG         |
| All Patient Diagnosis Related Groups                      | AP-DRG          |
| All Patient Refined Diagnosis Related Groups              | APR-DRG         |
| Ambulatory Payment Classifications                        | APC             |
| Local Code Processing                                     | LOCAL           |
| Enhanced Ambulatory Patient Grouping                      | EAPG            |
| Health Insurance Prospective Payment System               | HIPPS           |
| Current Dental Terminology                                | CDT             |
| Charge Description Master (chargemaster)                  | CDM             |
| TriCare Diagnosis Related Groups                          | TRIS-DRG        |
| Case Mix Group                                            | CMG             |
| Medicare Severity Long-Term Care Diagnosis Related Groups | MS-LTC-DRG      |

### Additional Standard Charge Methodology Notes

The "Standard Charge Methodology" data element describes the method used by the hospital to establish a payer-specific negotiated charge. Below are descriptions for the valid values for the "Standard Charge Methodology" data element and illustrative examples for how to represent unique contracting scenarios in combination with other data elements.

- `case rate`: A flat rate for a package of items and services triggered by a diagnosis, treatment, or condition for a designated length of time.
- `fee schedule`: The payer-specific negotiated charge is based on a fee schedule. Examples of common fee schedules include Medicare, Medicaid, commercial payer, and workers compensation. The dollar amount that is based on the indicated fee schedule should be encoded into the "Payer-specific Negotiated Charge: Dollar Amount" data element. For standard charges based on a percentage of a known fee schedule, the dollar amount should be calculated and encoded in the "Payer-specific Negotiated Charge: Dollar Amount" data element.
- `percent of total billed charges`: The payer-specific negotiated charge is based on a percentage of the total billed charges for an item or service. This percentage may vary depending on certain pre-determined criteria being met.
- `per diem`: The per day charge for providing hospital items and services.
- `other`: If the standard charge methodology used to establish a payer-specific negotiated charge cannot be described by one of the types of standard charge methodology above, select 'other' and encode a detailed explanation of the contracting arrangement in the "Additional Payer Notes" data attribute.

## Optional Data Attributes

"Hospital Financial Aid Policy", "General Contract Provisions", and "Billing Class" are optional data attributes. They are not required to be included but instructions have been added to support standardization of disclosure of these data attributes for hospitals that wish to provide more contextual information about their charges. If "Hospital Financial Aid Policy" or "General Contract Provisions" are included in the MRF, they are to be included to the [root node](#json-data-attributes). If "Billing Class" is included in the MRF, it is to be added to the [standard charge object](#standard-charge-object).

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **financial_aid_policy** | Hospital Financial Aid Policy | String | The hospital's financial aid policy. See [additional financial aid policy notes](#additional-notes-for-hospital-financial-aid-policy) for more details. | No |
| **general_contract_provisions** | General Contract Provisions | Array | An array of ` general`` ``contract`` ``provisions ` _objects_ for specific payer and plans or across all plans. | No |
| **billing_class** | Billing Class | Enum | The type of billing for the item/service at the established standard charge. The recommended values are "professional", "facility", and "both". | No |

### General Contract Provisions Object

| **Attribute** | **Name** | **Type** | **Description** | **Required** |
| --- | --- | --- | --- | :-: |
| **payer_name** | Payer Name | String | The name of the third-party payer associated with the contract provisions. | No |
| **plan_name** | Plan Name | String | The name of the payer's specific plan associated with the contract provisions. | No |
| **provisions** | Provisions | String | Description of contract provisions that are negotiated at an aggregate level across items and services (e.g., claim level). Examples include, but are not limited to, "stop-loss," "lesser-than," carve-outs, and outlier provisions that apply at the claim level. | Yes |

### Additional Notes for "Hospital Financial Aid Policy"

The hospital's financial aid policy, also known as charity care or bill forgiveness, that a hospital may choose or be required to apply to a particular individual's bill. This information may be displayed as either a description or as a link to the financial aid or cash price policy on the hospital's website.

### Additional Notes for "General Contract Provisions"

This data element can be used to encode payer contract provisions that are applicable at an aggregate level and may include variable items and services. Examples could be "stop-loss", "lesser than", carve-out, and outlier provisions that apply to the claim (as opposed to each item or service on the claim). Multiple general contract provisions across payer and plan combinations can be included in this data element. If a contract provision applies to a specific item or service, use the Payer-specific Negotiated Charge: Algorithm data element and encode the median, 10th percentile, and 90th percentile allowed amounts and count of allowed amounts data elements.

## **Conditional Requirements**

The following conditional requirements must be met for an MRF to be considered valid. These conditional requirements enforce regulatory rules for required data elements, provide flexibility in the development of MRFs, and ensure corresponding information is encoded for items and services to be understandable by the end user.

1. If the "Standard Charge Methodology" encoded value is "other", there must be a corresponding explanation found in the "additional notes" for the associated payer-specific negotiated charge.

2. If an item or service is encoded, a corresponding valid value must be encoded for at least one of the following: "Gross Charge", "Discounted Cash Price", "Payer-Specific Negotiated Charge: Dollar Amount", "Payer-Specific Negotiated Charge: Percentage", "Payer-Specific Negotiated Charge: Algorithm".

3. If a "Payers Information" object is encoded, then there must be a value for at least one of the following attributes in that object: "Payer-Specific Negotiated Charge: Dollar Amount", "Payer-Specific Negotiated Charge: Percentage", "Payer-Specific Negotiated Charge: Algorithm".

4. If there is "Payer-Specific Negotiated Charge: Dollar Amount" encoded, there must be a corresponding valid value encoded for the "De-identified Minimum Negotiated Charge" and "De-identified Maximum Negotiated Charge" elements.

5. If a "Payer-Specific Negotiated Charge: Percentage" or a "Payer-Specific Negotiated Charge: Algorithm" is encoded, then the "Count of Allowed Amounts" is required.

6. If a "Payer-Specific Negotiated Charge: Percentage" or a "Payer-Specific Negotiated Charge: Algorithm" is encoded, then the "10th Percentile Allowed Amount", "Median Allowed Amount", "90th Percentile Allowed Amount" are required (unless the "Count of Allowed Amounts" is "0").

7. If the "Count of Allowed Amounts" is "0", then a corresponding explanation in the "Additional Payer-Specific Notes" or "Additional Generic Notes" for the associated payer-specific negotiated charge is required.

8. If "Code Type(s)" is NDC, then the corresponding "Drug Unit of Measurement" and "Drug Type of Measurement" must be encoded.
