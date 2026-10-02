# **Hospital Price Transparency CSV Data Dictionary v3.0**

The v3.0 data dictionary includes formatting updates and new regulatory requirements from the Calendar Year 2026 Hospital Outpatient Prospective Payment and Ambulatory Surgical Center Payment System final rule ([CY 2026 OPPS/ASC Final Rule](https://www.federalregister.gov/documents/2025/11/25/2025-20907/medicare-program-hospital-outpatient-prospective-payment-and-ambulatory-surgical-center-payment)) that are effective January 1, 2026, with CMS enforcement beginning April 1, 2026.

Review this entire data dictionary for how to disclose data elements in CSV and find the [CSV "Tall" template here](./templates/V3.0.0_Tall_CSV_Format_Template.csv) and [CSV "Wide" template here](./templates/V3.0.0_Wide_CSV_Format_Template.csv) to begin building your hospital MRF. For an explanation of how to interpret the data element tables, review the [How to Read the Data Dictionary Tables](../HOW_TO_READ_DATA_DICTIONARY.md) information.

## **General CSV Instructions**

Developers of machine-readable files (MRFs) should generally consider and adopt established standards and industry norms for CSV files when creating the MRF. For more information on CSV standards visit <https://www.rfc-editor.org/rfc/rfc4180>.

For CSV, hospitals may choose either a "wide" or "tall" layout. The CSV MRF must be saved as plaintext data separated only by commas (",") and not use other delimiters. Below are additional reminders to avoid common errors in MRFs:

- Do not insert a value or any type of indicators (e.g., "N/A") if the hospital does not have applicable data to encode. If you would like to include an explanation for the blanks, you may do so using "Additional Generic Notes" or "Additional Payer-Specific Notes".
- Encode valid values as instructed below. Values encoded incorrectly will generate a deficiency.
  - For example, if the valid value is 'numeric' (such as for "Payer-Specific Negotiated Charge: Dollar Amount"), inserting anything other than a number (such as inserting a dollar sign with a number) will generate a deficiency. Similarly, if the valid value is 'enum' (such as for "Code Type"), inserting anything other than the values indicated (such as inserting 'other') will generate a deficiency.
  - All "Numeric" data elements must be positive numbers unless otherwise specified. Entering a negative number or "0" will generate a deficiency for these elements.
- While [GitHub examples](../../examples/CSV) exclude leading and trailing spaces in headers, valid values, and around pipes, inadvertently inserting spaces will not generate a deficiency. Similarly, while [GitHub examples](../../examples/CSV) may use capital and lower-case letters, valid values are case-insensitive and changes in capital vs lower-case letters will not generate a deficiency.
- Hospitals are permitted to include additional optional information through optional data elements that are defined in the data dictionary (e.g., "Billing Class" and "Hospital Financial Aid Policy") or hospital created data elements. Follow the technical instructions for including the defined optional data elements.
- Ensure all [conditional requirements](#conditional-requirements) are met for an MRF to be considered valid.
- Do not repeat column headers in row 1 and 3. Ensure each header is unique.

Encode the headers and valid values according to the data element implementation timeline in the HPT regulation ([45 CFR § 180.50](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180/subpart-B/section-180.50)) as finalized in the CY2026 OPPS/ASC final rule.

## **General Data Elements**

These required general data elements about the MRF must be stated once at the top of the file (i.e. the first row).

| **Column Header (Tall format)** | **Column Header (Wide format)** | **Name** | **Type** | **Description** | **Blanks Accepted** |
| --- | --- | --- | --- | --- | :-: |
| **hospital_name** | **hospital_name** | Hospital Name | String | The legal business name of the hospital associated with the file. | No |
| **last_updated_on** | **last_updated_on** | MRF Date | Date | Date on which the MRF was last updated. Date must be in an ISO 8601 format (i.e. YYYY-MM-DD). See [additional notes for MRF Date](#additional-notes-for-mrf-date). | No |
| **version** | **version** | CMS Template Version | String | The version of the CMS Template used. | No |
| **location_name** | **location_name** | Hospital Location(s) | String | The unique name(s) of the hospital location(s) absent any acronyms. | No |
| **hospital_address** | **hospital_address** | Hospital Address(es) | String | The physical address(es) of the corresponding hospital location(s). See [additional notes for hospital address(es)](#additional-notes-for-hospital-addresses). | No |
| **type_2_npi** | **type_2_npi** | Type 2 Organizational NPI(s) | String | The associated type 2 NPI(s) for the hospital and all hospital locations whose data is represented in the file. If there are multiple type 2 NPIs in the MRF, separate each NPI with a "\|" when encoding these values into the MRF. Only certain type 2 NPIs are required to be reported, see [additional notes for type 2 Organizational NPI(s)](#additional-notes-for-hospital-addresses). | No |
| **license_number \| \[state\]** | **license_number \| \[state\]** | Hospital Licensure Information | String | The hospital license number and the licensing state or territory's two-letter abbreviation for the hospital location(s) indicated in the file. If the hospital does not have a license number, leave the row 2 cell blank but encode the state in the header. See [additional csv placeholder notes](#additional-csv-placeholder-notes) for encoding the state abbreviation. | Yes |
| **attester_name** | **attester_name** | Attester Name | String | The first and last name of the hospital chief executive officer, president, or senior official designated to oversee the encoding of true, accurate, and complete data in the MRF. | No |
| **Header is [Attestation Statement](#additional-notes-for-attestation-statement)** | **Header is [Attestation Statement](#additional-notes-for-attestation-statement)** | Attestation Statement | Boolean | The required CMS defined attestation statement that the information displayed is true, accurate, and complete as of the date indicated in the file. Valid values: `true` and `false`. See [additional notes for attestation statement](#additional-notes-for-attestation-statement) for more details. | No |

### Additional Notes for MRF Date

ISO 8601 is the required format but the M/D/YYYY (e.g., 7/1/2024) or MM/DD/YYYY (e.g., 07/01/2024) formats are also accepted for the "MRF Date" data element in CSV "Tall" or "Wide" MRFs.

### Additional Notes for Hospital Address(es)

If the MRF contains identical standard charges for multiple hospital locations, separate the address of each location in the "Hospital Address(es)" element with a "\|". List the addresses in the same sequential order as the "Hospital Location(s)" values for the data element above . Address(es) must be included for, at a minimum, all inpatient facilities and stand-alone emergency departments. Each hospital location operating under a single hospital license (or approval) that has a different set of standard charges than the other location(s) operating under the same hospital license (or approval) must separately make public the standard charges applicable to that location.

### Additional Notes for Type 2 Organizational NPI(s)

Include the hospital and all corresponding hospital locations represented in the MRF's Type 2 NPI(s) that are associated with the primary taxonomy code starting with '28' (indicating hospital) or '27' (indicating hospital unit) and that is active as of the date of the most recent update to the standard charge information. If there are multiple Type 2 NPIs associated with the hospital, then separate each NPI with a "\|" when encoding these values into the MRF. Primary taxonomy codes beginning with '28' represent hospitals, and primary taxonomy codes that begin with '27' represent hospital units. Hospitals are only required to report their Type 2 NPIs, not the taxonomy codes. Hospitals should include all active Type 2 NPIs meeting this criteria and exclude all type 2 NPIs with a taxonomy other than '28' and '27'.

### Additional Notes for Attestation Statement

Hospitals should encode the necessary information available to the hospital for the public to be able to derive the dollar amount, including, but not limited to, the specific fee schedule or components referenced in such percentage, algorithm or formula in the standard charge data elements, and the additional notes data elements.

The "Attestation Statement" data element for CSV will require the following text in the column header:

> To the best of its knowledge and belief, this hospital has included all applicable standard charge information in accordance with the requirements of 45 CFR 180.50, and the information encoded is true, accurate, and complete as of the date in the file. This hospital has included all payer-specific negotiated charges in dollars that can be expressed as a dollar amount. For payer-specific negotiated charges that cannot be expressed as a dollar amount in the machine-readable file or not knowable in advance, the hospital attests that the payer-specific negotiated charge is based on a contractual algorithm, percentage or formula that precludes the provision of a dollar amount and has provided all necessary information available to the hospital for the public to be able to derive the dollar amount, including, but not limited to, the specific fee schedule or components referenced in such percentage, algorithm or formula.

While "true" or "false" is accepted from a form and manner perspective, a value of "true" is required to meet the attestation regulatory requirement (45 CFR 180.50(a)(3)). Please see the column header in the CSV template [here](./templates/V3.0.0_Tall_CSV_Format_Template.csv).

## **Required Standard Charge, Item/Service, and Coding Data Elements**

After the general data elements have been disclosed, the disclosure of required standard charges, item/service, and coding data elements will begin on row 3.

If a `--` is encountered in the following table, then the instruction does not apply to the specific CMS template selected. You can view both [CSV templates here](./templates).

| **Column Header (Tall format)** | **Column Header (Wide format)** | **Name** | **Type** | **Description** | **Blanks Accepted** |
| --- | --- | --- | --- | --- | --- |
| **description** | **description** | General Description | String | Description of each item or service provided by the hospital that corresponds to the standard charge the hospital has established. | No |
| **code \| \[i\]** | **code \| \[i\]** | Billing/Account Code(s) | String | Any code(s) used by the hospital for purposes of billing or accounting for the item or service. See [additional csv placeholder notes](#additional-csv-placeholder-notes) for implementation details. | Yes |
| **code \| \[i\] \| type** | **code \| \[i\] \| type** | Code Type(s) | Enum | The corresponding coding type for the `code` data element. Please see a list of the [valid values](#additional-notes-concerning-code-types) and [additional csv placeholder notes](#additional-csv-placeholder-notes) for implementation details. | Yes |
| **setting** | **setting** | Setting | Enum | Indicates whether the item or service is provided in connection with an inpatient admission or an outpatient department visit. Valid values: "inpatient", "outpatient", "both". | No |
| **drug_unit_of_measurement** | **drug_unit_of_measurement** | Drug Unit of Measurement | Numeric | If the item or service is a drug, indicate the unit value that corresponds to the established standard charge. | Yes |
| **drug_type_of_measurement** | **drug_type_of_measurement** | Drug Type of Measurement | Enum | The measurement type that corresponds to the established standard charge for drugs as defined by either the National Drug Code or the National Council for Prescription Drug Programs. See the [list](#additional-notes-for-drug-type-of-measurement-values) of valid values. | Yes |
| **standard_charge \| gross** | **standard_charge \| gross** | Gross Charge | Numeric | Gross charge is the charge for an individual item or service that is reflected on a hospital's chargemaster, absent any discounts. | Yes |
| **standard_charge \| discounted_cash** | **standard_charge \| discounted_cash** | Discounted Cash Price | Numeric | Discounted cash price is defined as the charge that applies to an individual who pays cash (or cash equivalent) for a hospital item or service. | Yes |
| **payer_name** | \-- | Payer Name | String | The name of the third party payer that is, by statute, contract, or agreement, legally responsible for payment of a claim for a healthcare item or service. | Yes |
| **plan_name** | \-- | Plan Name | String | The name of the payer's specific plan associated with the standard charge. | Yes |
| **modifiers** | **modifiers** | Modifier(s) | String | Include any modifier(s) that may change the standard charge that corresponds to hospital items or services. | Yes |
| **standard_charge \| negotiated_dollar** | **standard_charge \| \[payer_name\] \| \[plan_name\] \| negotiated_dollar** | Payer-specific Negotiated Charge: Dollar Amount | Numeric | Payer-specific negotiated charge (encoded as a dollar amount) that a hospital has negotiated with a third party payer for the corresponding item or service. See [additional csv placeholder notes](#additional-csv-placeholder-notes) for implementation details. | Yes |
| **standard_charge \| negotiated_percentage** | **standard_charge \| \[payer_name\] \| \[plan_name\] \| negotiated_percentage** | Payer-specific Negotiated Charge: Percentage | Numeric | Payer-specific negotiated charge (encoded as a percentage) that a hospital has negotiated with a third party payer for an item or service. See [additional csv placeholder notes](#additional-csv-placeholder-notes) for implementation details and [additional notes for percentage](#additional-notes-for-standard-charge-percentage-and-algorithm) for disclosure details. | Yes |
| **standard_charge \| negotiated_algorithm** | **standard_charge \| \[payer_name\] \| \[plan_name\] \| negotiated_algorithm** | Payer-specific Negotiated Charge: Algorithm | String | Payer-specific negotiated charge (encoded as an algorithm) that a hospital has negotiated with a third party payer for the corresponding item or service. See [additional csv placeholder notes](#additional-csv-placeholder-notes) for implementation details. | Yes |
| **median_amount** | **median_amount \| \[payer_name\] \| \[plan_name\]** | Median Allowed Amount | Numeric | Median allowed amount means the median of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. If the payer-specific negotiated charge is based on a percentage or algorithm, the MRF must also specify the median allowed amount for that item or service. See [additional allowed amount notes](#additional-allowed-amount-notes) for more information. | Yes |
| **10th_percentile** | **10th_percentile \| \[payer_name\] \| \[plan_name\]** | 10th Percentile Allowed Amount | Numeric | Tenth (10th) percentile allowed amount means the 10th percentile of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. If the payer-specific negotiated charge is based on a percentage or algorithm, the MRF must also specify the 10th percentile allowed amount for that item or service. See [additional allowed amount notes](#additional-allowed-amount-notes) for more information. | Yes |
| **90th_percentile** | **90th_percentile \| \[payer_name\] \| \[plan_name\]** | 90th Percentile Allowed Amount | Numeric | Ninetieth (90th) percentile allowed amount means the 90th percentile of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. If the payer-specific negotiated charge is based on a percentage or algorithm, the MRF must also specify the 90th percentile allowed amount for that item or service. See [additional allowed amount notes](#additional-allowed-amount-notes) for more information. | Yes |
| **count** | **count \| \[payer_name\] \| \[plan_name\]** | Count of Allowed Amounts | String | Count of remittances used to calculate the allowed amounts. Allowed values are "0", "1 through 10", and whole numbers 11 and greater absent any thousands separator. See [additional notes for count of allowed amount](#additional-allowed-amount-notes) for more information. | Yes |
| **standard_charge \| min** | **standard_charge \| min** | De-identified Minimum Negotiated Charge | Numeric | De-identified minimum negotiated charge is the lowest charge that a hospital has negotiated with all third party payers for an item or service. This is determined from the set of negotiated standard charge dollar amounts. | Yes |
| **standard_charge \| max** | **standard_charge \| max** | De-identified Maximum Negotiated Charge | Numeric | De-identified maximum negotiated charge is the highest charge that a hospital has negotiated with all third party payers for an item or service. This is determined from the set of negotiated standard charge dollar amounts. | Yes |
| **standard_charge \| methodology** | **standard_charge \| \[payer_name\] \| \[plan_name\] \| methodology** | Standard Charge Methodology | Enum | Method used to establish the payer-specific negotiated charge. The valid value corresponds to the contract arrangement. See [additional standard charge methodology notes and valid values](#additional-standard-charge-methodology-notes) for more information and [additional csv placeholder notes](#additional-csv-placeholder-notes) for implementation details. | Yes |
| **additional_generic_notes** | **additional_generic_notes** | Additional Generic Notes | String | A free text data element that is used to help explain any of the data including, for example, blanks due to no applicable data, charity care policies, or other contextual information that aids in the public's understanding of the standard charges. See [Additional Notes for Additional Generic Notes](#additional-notes-for-additional-generic-notes) for more details. | Yes |
| \-- | **additional_payer_notes \| \[payer_name\] \| \[plan_name\]** | Additional Payer-Specific Notes | String | A free text data element used to help explain data in the file that is related to a payer-specific negotiated charge. See [additional csv placeholder notes](#additional-csv-placeholder-notes) for implementation details. | Yes |

### Additional Notes for Standard Charge Percentage and Algorithm

If a payer-specific negotiated charge dollar can be calculated, for example if the payer-specific negotiated charge is 70% of a known fee schedule, calculate the dollar amount and encode the "Payer-Specific Negotiated Charge Dollar" data element. If the payer-specific negotiated charge is a percentage for which a dollar amount cannot be calculated or is a base rate modified by a percentage, encode the "Payer-Specific Negotiated Charge Percentage" data element. This data element will contain the numeric representation of the percentage, not as a decimal (70.5% is to be entered as "70.5" and not ".705").

If the "Payer-Specific Negotiated Charge: Percentage" or "Payer-Specific Negotiated Charge: Algorithm" data elements are encoded, then also encode the corresponding allowed amounts and count of allowed amount data elements for that item or service.

### Additional Allowed Amount Notes

If the payer-specific negotiated charge for an item or service is based on a percentage or algorithm, the MRF must include the "Median Allowed Amount", "10th Percentile Allowed Amount", and "90th Percentile Allowed Amount" elements for that item or service. Hospitals must use EDI 835 ERA transaction data or an alternative equivalent source of remittance data that includes the same information as EDI 835 ERA transaction data would include, to calculate and encode the allowed amounts.

The allowed amounts are the specified percentile (median, 10th percentile, or 90th percentile) of the total allowed amounts the hospital has historically received from a third party payer for an item or service for a time period no less than 12 months and no longer than 15 months prior to posting the machine-readable file. The total allowed amount should reflect the total amount the hospital was reimbursed for the item or service (or service package). The total allowed amount is derived from the gross charge minus contractual adjustments and consists of the portion billed to a payer for a particular plan and the portion, if any, billed to the patient.

When calculating the allowed amounts, if the calculated percentile falls between two observed allowed amounts (in other words, where the total count, n, is an even number), the allowed amount will be the next highest observed value. Hospitals should exclude \$0 dollar remittances when calculating and encoding the allowed amounts. If the count of allowed amounts is zero, do not encode these data elements.

### Additional Notes for Count of Allowed Amounts

Encode the total number of allowed amount remittances from the EDI 835 ERA transaction data or an alternative, equivalent source of remittance data used to calculate the median, 10th percentile, and 90th percentile allowed amounts. If the total number of remittances is 11 or greater, encode the value as whole numbers absent any thousands separator. For example, "2,025" includes a thousands separator and is not accepted. If the number of remittances is greater than 0 but less than 11, encode "1 through 10". If there are no remittances for the time period of no less than 12 months and no more than 15 months, encode "0" in the "Count of Allowed Amounts" and in the "Additional Generic Notes" in the CSV Tall and the "Additional Payer-Specific Notes" in the CSV Wide explain why there is no remittances.

### Additional Notes for Drug Type Of Measurement Values

The following valid values for "Drug Type Of Measurement" are based on two sets of industry standards; National Drug Code and National Council for Prescription Drug Programs.

| **Standard Name**  | **Valid Value** |
| ------------------ | --------------- |
| Grams              | GR              |
| Milligrams         | ME              |
| Milliliters        | ML              |
| Unit               | UN              |
| International Unit | F2              |
| Each               | EA              |
| Gram               | GM              |

### Additional Notes for Additional Generic Notes

If using the CSV Tall template, this data element can be used for both additional payer-specific and general information about the standard charge for an item or service.

If using the CSV Wide template, use the "Additional Generic Notes" data element for additional general information and use the "Additional Payer-Specific Notes" data element for additional payer-specific information.

### Additional CSV Placeholder Notes

There are a few CSV data elements that have placeholders that must be updated by the developer of the MRF or it will generate a validator error. Placeholders can be identified as an item in brackets `[ ]` and are found in column headers (rows 1 and 3). For example, both data elements `standard_charge | [payer_name] | [plan_name] | algorithm` and `code | [i]` on row 3 contain placeholders that must be replaced with valid values.

There are four different types of placeholders in the MRF: `[state]`, `[i]`, `[plan_name]`, and `[payer_name]`.

- `[state]` must be replaced by the 2-letter state code such as CA or NY. For example, the column header on row 1, `license_number|[state]` would be updated to `license_number|CA` for a hospital licensed by the state of California.
- `[i]` is a CSV header placeholder that must be replaced with numbers starting at "1", increasing by one to however many columns of codes are needed, and matching the associated code type header. For example, if two code and code type combinations are needed, the first header is `code|1` and the second header is `code|2`.
- `[plan_name]` must be replaced by the specific plan name for the payer with whom the hospital has negotiated a payer-specific negotiated charge.
- `[payer_name]` must be replaced by the name of the payer with whom the hospital has negotiated a payer-specific negotiated charge.
- See examples of how to update [placeholders here](../../examples/CSV).

Note: Nine standard charge data elements in the CSV "Wide" template contain payer name and plan name placeholders (specifically: "Payer-specific Negotiated Charge: Dollar Amount", "Payer-specific Negotiated Charge: Percentage", "Payer-specific Negotiated Charge: Algorithm", "Median Allowed Amount", "10th Percentile Allowed Amount", "90th Percentile Allowed Amount", "Count of Allowed Amounts", "Standard Charge Methodology", and "Additional Payer-Specific Notes"). If a hospital encodes one payer and plan combination into any of the nine standard charge data element headers, the remaining payer-specific headers for that payer and plan combination are also required to be included in row 3, regardless of whether the hospital has applicable standard charge information to encode for the remaining headers.

### Additional Standard Charge Methodology Notes

The "Standard Charge Methodology" data element describes the method used by the hospital to establish a payer-specific negotiated charge. Below are definitions for the valid values for the "Standard Charge Methodology" data element and illustrative examples for how to represent unique contracting scenarios in combination with other data elements.

Encode the value that most closely represents the standard charge methodology for the payer-specific negotiated charge for an associated item or service. If the standard charge methodology the hospital has used isn't represented in the definitions, encode `other` along with a detailed explanation of the contracting arrangement in the "Additional Generic Notes" for the CSV Tall template or the "Additional Payer-Specific Notes" for the CSV Wide template.

- `case rate`: A flat rate for a package of items and services triggered by a diagnosis, treatment, or condition for a designated length of time.
- `fee schedule`: The payer-specific negotiated charge is based on a fee schedule. Examples of common fee schedules include Medicare, Medicaid, commercial payer, and workers compensation. The dollar amount that is based on the indicated fee schedule should be encoded into the "Payer-specific Negotiated Charge: Dollar Amount" data element. For standard charges based on a percentage of a known fee schedule, the dollar amount should be calculated and encoded in the "Payer-specific Negotiated Charge: Dollar Amount" data element.
- `percent of total billed charges`: The payer-specific negotiated charge is based on a percentage of the total billed charges for an item or service. This percentage may vary depending on certain pre-determined criteria being met.
- `per diem`: The per day charge for providing hospital items and services.
- `other`: If the standard charge methodology used to establish a payer-specific negotiated charge cannot be described by one of the types of standard charge methodology above, select 'Other' and encode a detailed explanation of the contracting arrangement in the "Additional Generic Notes" for the CSV Tall template or the "Additional Payer-Specific Notes" for the CSV Wide template.

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

## Optional Column Headers

"Hospital Financial Aid Policy", "General Contract Provisions", and "Billing Class" are optional data element headers. They are not required to be included, but instructions have been added to support standardization of disclosure of these data elements for hospitals that wish to provide more contextual information about their charges. If "Hospital Financial Aid Policy" or "General Contract Provisions" is included in the MRF, we recommend it be included with the **General Data Elements** on the first row. If "Billing Class" header is included in the MRF, we recommend it be included on the third row.

| **Column Header (Tall format)** | **Column Header (Wide format)** | **Name** | **Type** | **Description** | **Blanks Accepted** |
| --- | --- | --- | --- | --- | --- |
| **financial_aid_policy** | **financial_aid_policy** | Hospital Financial Aid Policy | String | The hospital's financial aid policy. See [additional financial aid policy notes](#additional-notes-for-hospital-financial-aid-policy) for more details. | Yes |
| **general_contract_provisions** | **general_contract_provisions** | General Contract Provisions | String | Payer contract provisions that are negotiated at an aggregate level across items and services (e.g., claim level). Examples include, but are not limited to, "stop-loss," "lesser-than," carve-outs, and outlier provisions that apply at the claim level. | Yes |
| **billing_class** | **billing_class** | Billing Class | Enum | The type of billing for the item/service at the established standard charge. The recommended values are "professional", "facility", and "both". | Yes |

### Additional Notes for Hospital Financial Aid Policy

The hospital's financial aid policy, also known as charity care or bill forgiveness, that a hospital may choose or be required to apply to a particular individual's bill. This information may be displayed as either a description or as a link to the financial aid or cash price policy on the hospital's website.

### Additional Notes for General Contract Provisions

This data element can be used to encode payer contract provisions that are applicable at an aggregate level and may include variable items and services. Examples could be "stop-loss," ,"lesser than," carve-out, and outlier provisions that apply to the claim (as opposed to each item or service on the claim). Multiple general contract provisions across payer and plan combinations can be included in this data element. If a contract provision applies to a specific item or service, use the Payer-specific Negotiated Charge: Algorithm data element and encode the median, 10th , and 90th percentile allowed amounts and count of allowed amounts data elements.

## **Conditional Requirements**

The following conditional requirements must be met for an MRF to be considered valid. These conditional requirements enforce regulatory rules for required data elements, provide flexibility in the development of MRFs, and ensure corresponding information is encoded for items and services to be understandable by the end user.

1.  If a "Payer Specific Negotiated Charge" is encoded as a dollar amount, percentage, or algorithm, then a corresponding valid value for the payer name, plan name, and standard charge methodology must also be encoded. Conversely, if values are encoded in the "Payer Name" or "Plan Name" columns in the CSV tall format, at least one of the three payer-specific charge properties must also be encoded: "Payer-specific Negotiated Charge: Dollar Amount", "Payer-specific Negotiated Charge: Percentage", or "Payer-specific Negotiated Charge: Algorithm".
2.  If a standard charge is encoded, there must be a corresponding code and code type pairing. The code and code type pairing do not need to be in the first code and code type columns (i.e., `code|1` and `code|1|type`).
3.  If a value is encoded in the "Billing/Account Code(s)", a value must also be encoded in the corresponding "Code Type(s)". Conversely, if a value is encoded in the "Code Type(s)", a value must be encoded in the corresponding "Billing/Account Code(s)" (e.g., if a value is encoded in `code|2|type`, then a value must be encoded in `code|2`).
4.  If the "Standard Charge Methodology" encoded value is "other", there must be a corresponding explanation found in the "Additional Payer-Specific Notes" or "Additional Generic Notes" for the associated payer-specific negotiated charge.
5.  If an item or service is encoded, a corresponding valid value must be encoded for at least one of the following: "Gross Charge", "Discounted Cash Price", "Payer-Specific Negotiated Charge: Dollar Amount", "Payer-Specific Negotiated Charge: Percentage", "Payer-Specific Negotiated Charge: Algorithm".
6.  If there is "Payer-Specific Negotiated Charge: Dollar Amount" encoded, there must be a corresponding valid value encoded for the "De-identified Minimum Negotiated Charge" and "De-identified Maximum Negotiated Charge" elements.
7.  If a "Payer-Specific Negotiated Charge: Percentage" or a "Payer-Specific Negotiated Charge: Algorithm" is encoded, then the "Count of Allowed Amounts" is required.
8.  If a "Payer-Specific Negotiated Charge: Percentage" or a "Payer-Specific Negotiated Charge: Algorithm" is encoded, then the "10th Percentile Allowed Amount", "Median Allowed Amount", "90th Percentile Allowed Amount" are required (unless the "Count of Allowed Amounts" is "0").
9.  If the "Count of Allowed Amounts" is "0", then a corresponding explanation in the "Additional Payer-Specific Notes" or "Additional Generic Notes" for the associated payer-specific negotiated charge is required.
10. If "Code Type(s)" is NDC, then the corresponding "Drug Unit of Measurement" and "Drug Type of Measurement" must be encoded.
11. If a modifier is encoded without an item or service, then a "Description" and one of the following is the minimum information required: "Payer-specific Negotiated Charge: Dollar Amount", "Payer-specific Negotiated Charge: Percentage", "Payer-specific Negotiated Charge: Algorithm", "Additional Generic Notes", or "Additional Payer-Specific Notes".
12. If a value is encoded in the "Drug Unit of Measurement", a value must also be encoded in the "Drug Type of Measurement". Conversely, if a value is encoded in the "Drug Type of Measurement", a value must be encoded in the "Drug Unit of Measurement".
