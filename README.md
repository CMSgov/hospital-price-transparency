[![CMS Transparency in Coverage](resources/images/HPT_banner.png?raw=true "Hospital Price Transparency")](https://www.cms.gov/priorities/key-initiatives/hospital-price-transparency)

# Hospital Price Transparency 
This technical implementation guide contains data dictionaries, CSV templates, and JSON schema for the machine readable files as required by the [Hospital Price Transparency](https://www.cms.gov/priorities/key-initiatives/hospital-price-transparency) final rules ([45 CFR 180](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180)).

Overview
========

The hospital price transparency requirements are codified in regulations at [45 CFR Part 180](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180) and applies to facilities that meet the definition of hospital (defined at [45 CFR § 180.20](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180/subpart-B/section-180.20)) and that are not otherwise excepted (see [45 CFR § 180.30(b)](https://www.ecfr.gov/current/title-45/part-180/section-180.30#p-180.30(b))).  Hospitals must make public their standard charges online in two ways: 

1.	A machine-readable file containing a list of all standard charges for all items and services as provided in [§ 180.50](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180/subpart-B/section-180.50), and;
1.	A consumer-friendly list of standard charges for a limited set of shoppable services as provided in [§ 180.60](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180/subpart-B/section-180.60).

This GitHub repository addresses only a subset of the requirements for the comprehensive MRF as specified at [45 CFR § 180.50](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-E/part-180/subpart-B/section-180.50), as amended by the CY2024 OPPS ASC Final Rule.

For information on the consumer-friendly display of shoppable services, refer to [10 Steps to a Consumer Friendly Display of Shoppable Services](https://www.cms.gov/files/document/steps-making-public-standard-charges-shoppable-services.pdf).

Additional Resources
====================

Users should review the final rule(s) in their entirety as well as review any clarifying guidance provided on the [Hospital Price Transparency Resources](https://www.cms.gov/hospital-price-transparency/resources) webpage to ensure compliance.

* [Github Issues](https://guides.github.com/features/issues/) - Where people discuss issues related to the project.
* [Github Discussions](https://github.com/CMSgov/hospital-price-transparency/discussions) - Use these channels for conversational topics (for example, "How do I&hellip;" or "What do you think about&hellip;" instead of bug reports or feature requests).

Before posting a comment, issue, or question, please search through existing discussions and issues. There is a good chance that the topic in questions is already being discussed.

Policy questions can be directed to: PriceTransparencyHospitalCharges@cms.hhs.gov. Hospitals undergoing an enforcement action may direct questions to: HPTCompliance@cms.hhs.gov.

CMS Template Technical Requirements
===================================

This repository houses the required CMS templates, in a CSV “tall”, CSV “wide” and JSON format, and provides the data dictionary, or technical instruction, on how hospitals must encode standard charge information into MRFs.

### Schemas
The following is the technical documentation for the allowable formats:
* [CSV](https://github.com/CMSgov/hospital-price-transparency/tree/master/documentation/CSV)
* [JSON](https://github.com/CMSgov/hospital-price-transparency/tree/master/documentation/JSON)

Implementation Timeline
====================
In the CY2024 OPPS/ASC final rule, CMS finalized a requirement for hospitals to adopt a CMS template and encode standard charge information for a subset of data elements by July 1, 2024, and all required data elements by January 1, 2025, as noted in the following tables:

#### CMS Template Required Data Elements and Enforcement Timeline

#####  MRF Information 
| Requirement | Regulation cite* | Compliance Date |
| ------------- | --------------- | --------------- |
| MRF Date | [45 CFR § 180.50 (b)(2)(i)(B)](#-cfr-timing-information) | July 1, 2024 |
| CMS Template Version | [45 CFR § 180.50 (b)(2)(i)(B)](#-cfr-timing-information) | July 1, 2024 |
| Affirmation Statement | [45 CFR § 180.50 (a)(3)(ii)](#-cfr-timing-information) | July 1, 2024 |
##### Hospital Information 
| Requirement | Regulation cite* | Compliance Date |
| ------------- | --------------- | --------------- |
| Hospital Name | [45 CFR § 180.50 (b)(2)(i)(A)](#-cfr-timing-information) | July 1, 2024 |
| Hospital Location(s) | [45 CFR § 180.50 (b)(2)(i)(A)](#-cfr-timing-information) | July 1, 2024 |
| Hospital Address(es) | [45 CFR § 180.50 (b)(2)(i)(A)](#-cfr-timing-information) | July 1, 2024 |
| Hospital Licensure Information | [45 CFR § 180.50 (b)(2)(i)(A)](#-cfr-timing-information) | July 1, 2024 |
##### Standard Charges
| Requirement | Regulation cite* | Compliance Date |
| ------------- | --------------- | --------------- |
| Gross Charge | [45 CFR § 180.50 (b)(2)(ii)](#-cfr-timing-information) | July 1, 2024 |
| Discounted Cash Price | [45 CFR § 180.50 (b)(2)(ii)](#-cfr-timing-information) | July 1, 2024 |
| Payer Name | [45 CFR § 180.50 (b)(2)(ii)(A)](#-cfr-timing-information) | July 1, 2024 |
| Plan Name | [45 CFR § 180.50 (b)(2)(ii)(A)](#-cfr-timing-information) | July 1, 2024 |
| Standard Charge Method | [45 CFR § 180.50 (b)(2)(ii)(B)](#-cfr-timing-information) | July 1, 2024 |
| Payer-Specific Negotiated Charge - Dollar Amount | [45 CFR § 180.50 (b)(2)(ii)(C)](#-cfr-timing-information) | July 1, 2024 |
| Payer-Specific Negotiated Charge - Percentage | [45 CFR § 180.50 (b)(2)(ii)(C)](#-cfr-timing-information) | July 1, 2024 |
| Payer-Specific Negotiated Charge - Algorithm | [45 CFR § 180.50 (b)(2)(ii)(C)](#-cfr-timing-information) | July 1, 2024 |
| Estimated Allowed Amount | [45 CFR § 180.50 (b)(2)(ii)(C)](#-cfr-timing-information) | January 1, 2025 |
| Additional Generic Notes | [45 CFR § 180.50 (b)(2)(ii)(C)](#-cfr-timing-information) | July 1, 2024 |
| Additional Payer-Specific Notes | [45 CFR § 180.50 (b)(2)(ii)(C)](#-cfr-timing-information) | July 1, 2024 |
| De-identified Minimum Negotiated Charge| [45 CFR § 180.50 (b)(2)(ii)](#-cfr-timing-information) | July 1, 2024 |
| De-identified Maximum Negotiated Charge| [45 CFR § 180.50 (b)(2)(ii)](#-cfr-timing-information) | July 1, 2024 |
##### Item & Service Information
| Requirement | Regulation cite* | Compliance Date |
| ------------- | --------------- | --------------- |
| General Description | [45 CFR § 180.50 (b)(2)(iii)(A)](#-cfr-timing-information) | July 1, 2024 |
| Setting | [45 CFR § 180.50 (b)(2)(iii)(B)](#-cfr-timing-information) | July 1, 2024 |
| Drug Unit of Measurement | [45 CFR § 180.50 (b)(2)(iii)(C)](#-cfr-timing-information) | January 1, 2025 |
| Drug Type of Measurement | [45 CFR § 180.50 (b)(2)(iii)(C)](#-cfr-timing-information) | January 1, 2025 |
##### Coding Information
| Requirement | Regulation cite* | Compliance Date |
| ------------- | --------------- | --------------- |
| Billing/Accounting Code | [45 CFR § 180.50 (b)(2)(iv)(A)](#-cfr-timing-information) | July 1, 2024 |
| Code Type | [45 CFR § 180.50 (b)(2)(iv)(B)](#-cfr-timing-information) | July 1, 2024 |
| Modifiers | [45 CFR § 180.50 (b)(2)(iv)(C)](#-cfr-timing-information) | January 1, 2025 |

##### * CFR Timing Information
As amended in the CY2024 OPPS ASC Final Rule, effective January 1, 2024. Links in the above table will be updated once the final rule is published in the eCFR.
