# **Guide for Updating from Data Dictionary v2.2 to Data Dictionary v3.0**

This document provides information about the changes between the hospital machine readable file (MRF) requirements published in data dictionary v2.2 and the requirements published in data dictionary v3.0. The v3.0 data dictionary includes formatting updates and new regulatory requirements from the Calendar Year 2026 Hospital Outpatient Prospective Payment and Ambulatory Surgical Center Payment System final rule (CY 2026 OPPS/ASC Final Rule) that are effective January 1, 2026, with CMS enforcement beginning April 1, 2026. This document provides guidance on how to update a hospital MRF to comply with the new requirements with the assumption that the hospital MRF is already fully compliant with the data dictionary v2.2 requirements.

## **Table of contents**

- [Changes applicable to all formats](#changes-applicable-to-all-formats) (CSV and JSON)

  - [Attestation statement replaces Affirmation statement](#attestation-statement-replaces-affirmation-statement)
  - [New Attester Name and Type 2 Organizational NPI general data elements](#new-attester-name-and-type-2-organizational-npi-general-data-elements)
  - [New allowed values for code type](#new-allowed-values-for-code-type-data-element)
  - [Hospital location data element renamed location name](#hospital-location-data-element-renamed-location-name)
  - [Payer-specific charge requirement](#payer-specific-charge-requirement)
  - [Allowed amount data elements replace Estimated amount data element](#allowed-amount-data-elements-replace-estimated-amount)

- [JSON-only changes](#json-only-changes)

  - [New optional attribute in Modifier Information object](#new-optional-attribute-in-modifier-information-object)
  - [New optional attribute in Standard Charge object](#new-optional-attribute-in-standard-charge-object)
  - [Drug unit of measurement data type change](#drug-unit-of-measurement-data-type-change)

## **Changes applicable to all formats**

### **Attestation statement replaces Affirmation statement**

The affirmation statement data elements are now attestation data elements. Additionally, the attestation text is now:

> To the best of its knowledge and belief, this hospital has included all applicable standard charge information in accordance with the requirements of 45 CFR 180.50, and the information encoded is true, accurate, and complete as of the date in the file. This hospital has included all payer-specific negotiated charges in dollars that can be expressed as a dollar amount. For payer-specific negotiated charges that cannot be expressed as a dollar amount in the machine-readable file or not knowable in advance, the hospital attests that the payer-specific negotiated charge is based on a contractual algorithm, percentage or formula that precludes the provision of a dollar amount and has provided all necessary information available to the hospital for the public to be able to derive the dollar amount, including, but not limited to, the specific fee schedule or components referenced in such percentage, algorithm or formula.

- MRFs in the CSV tall or CSV wide formats should use this new attestation text in the general data element headers in row 1. Details are in the [CSV Data Dictionary](./CSV/README.md#additional-notes-for-attestation-statement).
- MRFs in the JSON format should change the name of the Attestation Object to "attestation" and change the names of the contained attributes to "attestation" and "confirm_attestation". Details are in the [JSON Data Dictionary](./JSON/README.md#attestation-object).

### **New Attester Name and Type 2 Organizational NPI general data elements**

The following general data elements are now required: "Attester Name​" and "Type 2 Organizational NPI​". You should encode these data elements alongside the existing general data elements.

- "attester_name" is a "string" data element. Details are in the [CSV Data Dictionary](./CSV/README.md#general-data-elements) and [JSON Data Dictionary](./JSON/README.md#json-data-attributes).
- "type_2_npi" is a list of "string" data element. Details are in the [CSV Data Dictionary](./CSV/README.md#general-data-elements) and [JSON Data Dictionary](./JSON/README.md#json-data-attributes).

### **New allowed values for code type data element**

The values "CMG" and "MS-LTC-DRG" may now be encoded for Code Type data elements. Complete lists of the allowed code types are in the [CSV Data Dictionary](./CSV/README.md#additional-notes-concerning-code-types) and the [JSON Data Dictionary](./JSON/README.md#additional-notes-concerning-code-types).

### **Hospital location data element renamed location name**

The "location_name" data element name replaces the "hospital_location" general data element name to reduce confusion when encoding in the MRF. The definition of the data element is not changed.

- MRFs in the CSV tall or CSV wide formats should make this change in the general data element headers in row 1. Details are in the [CSV Data Dictionary](./CSV/README.md#general-data-elements).
- MRFs in the JSON format should change the name of the encoded data element. Details are in the [JSON Data Dictionary](./JSON/README.md#json-data-attributes).

### **Payer-specific charge requirement**

When an item or service is encoded with a payer name and plan name, there must also be at least one payer-specific charge encoded.

- For MRFs in the CSV tall format, if values are encoded in the "payer_name" or "plan_name" columns, at least one of the three payer-specific charge properties must also be encoded: "standard_charge_dollar", "standard_charge_percentage", or "standard_charge_algorithm".

- For MRFs in the CSV wide format, no specific changes are needed when encoding information, as the payer name and plan name are included in the headers for the payer-specific charge columns.

- For MRFs in the JSON format, each Payers Information object must contain at least one of the three payer-specific charge properties: "standard_charge_dollar", "standard_charge_percentage", or "standard_charge_algorithm". There is a note explaining this below the table of Payers Information Object elements in the [JSON Data Dictionary](./JSON/README.md#payers-information-object).

### **Allowed amount data elements replace Estimated amount**

#### Removal of estimated amount data element

The CY 2026 OPPS/ASC Final Rule requirements remove the "Estimated Allowed Amount" data element.

- MRFs in the CSV tall format are no longer required to have an "estimated_amount" column header in row 3.
- MRFs in the CSV wide format are no longer required to have any "estimated_amount \| \[payer_name\] \| \[plan_name\]" column headers in row 3.
- MRFs in the JSON format do not have a "estimated_amount" property as part of their Payers Information objects.

#### Addition of four allowed amount data elements

The CY 2026 OPPS/ASC Final Rule requires the addition of the "Median Amount", "10th Percentile", "90th Percentile", and "Count of Allowed Amounts" data elements.

- MRFs in the CSV tall format must have "median_amount", "10th_percentile", "90th_percentile", and "count" column headers in row 3.
- MRFS in the CSV wide format must have "median_amount \| \[payer_name\] \| \[plan_name\]", "10th_percentile \| \[payer_name\] \| \[plan_name\]", "90th_percentile \| \[payer_name\] \| \[plan_name\]", and "count \| \[payer_name\] \| \[plan_name\]" column headers in row 3 for each payer and plan.
- MRFs in the JSON format have "median_amount", "10th_percentile", "90th_percentile", and "count" properties defined as part of their Payers Information objects.

The values encoded for "Median Amount", "10th Percentile", and "90th Percentile" data elements should all be positive numbers. The values encoded for "Count of Allowed Amounts" elements should be non-negative integers except for values from 1 through 10.

> This means that a value of 0 may be encoded for a "Count of Allowed Amounts". Values of 0 are still prohibited in other numeric data elements.
>
> If the count of remittances utilized to calculate the allowed amount data elements is 1 through 10, then encode this exact string in the "count of allowed amounts" data element: "1 through 10".

Details for these new data elements are in the [CSV Data Dictionary](./CSV/README.md#required-standard-charge-itemservice-and-coding-data-elements) and [JSON Data Dictionary](./JSON/README.md#payers-information-object).

#### New conditional requirements for Count of Allowed Amounts

There are some changes to conditional requirements based on this change in defined data elements.

The conditional requirement applicable to "Estimated Allowed Amount" is **removed**:

> If a "payer specific negotiated charge" can only be expressed as a percentage or algorithm, then a corresponding "Estimated Allowed Amount" must also be encoded.

The following conditional requirements are **added**:

> If a "Payer-Specific Negotiated Charge: Percentage" or a "Payer-Specific Negotiated Charge: Algorithm" is encoded, then the "Count of Allowed Amounts" is required.
>
> If a "Payer-Specific Negotiated Charge: Percentage" or a "Payer-Specific Negotiated Charge: Algorithm" is encoded, then the "10th Percentile Allowed Amount", "Median Allowed Amount", "90th Percentile Allowed Amount" are required (unless the "Count of Allowed Amounts" is "0").
>
> If the "Count of Allowed Amounts" is "0", then a corresponding explanation in the "Additional Payer-Specific Notes" or "Additional Generic Notes" for the associated payer-specific negotiated charge is required.

The updated list of conditional requirements are in the [CSV Data Dictionary](./CSV/README.md#conditional-requirements) and [JSON Data Dictionary](./JSON/README.md#conditional-requirements).

## **JSON-only changes**

### **New optional attribute in Modifier Information object**

A Modifier Information object may now contain a "setting" attribute. The allowed values for this attribute are the same as for the "setting" attribute in the Standard Charge object. See the updated definition for the Modifier Information object in the [JSON Data Dictionary](./JSON/README.md#modifier-information-object).

### **New optional attribute in Standard Charge object**

A Standard Charge object may now contain a "modifier_code" attribute. This attribute is defined as an array of strings, each of which should be a modifier code present in a Modifier Information object. See the updated definition for the Standard Charge object in the [JSON Data Dictionary](./JSON/README.md#standard-charge-object).

### **Drug unit of measurement data type change**

The "unit" attribute in the Drug Information object in the JSON schema is now a "number" type. See the updated definition for the Drug Information object in the [JSON Data Dictionary](./JSON/README.md#drug-information-object).
