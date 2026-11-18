# How to Read the Data Dictionary Tables

The following language explains how to interpret the column headers in the data element tables for the [CSV Data Dictionary](./CSV/README.md) and [JSON Data Dictionary](./JSON/README.md).

**Name:** Indicates the data element or category of data you must encode in your MRF.

**Column Header (Tall Format):** Indicates how each column header must appear in the CSV 'Tall' format. Additional instructions are included in the 'description' when you must modify the header to accommodate hospital-specific information.

**Column Header (Wide Format):** Indicates how each column header must appear in the CSV 'Wide' format. Additional instructions are included in the 'description' when you must modify the header to accommodate hospital-specific information.

**Attribute:** Indicates how you must encode each attribute, that is, the exact string you must use in the JSON format for each data element.

**Description:** Explains what standard charge information is expected for the required data element and its relation to other required data elements in the MRF.
Type: Indicates the data type for the values that you may encode below the CSV header or associated with the JSON attribute including:

- "Array" indicates an ordered collection of other JSON elements that may be objects, strings, Boolean, or another array. Arrays are a method to assign multiple values to one element in JSON.
- "Boolean" indicates the allowed value is either a "true" or "false".
- "Date" indicates a date must be encoded.
- "Enum" indicates that you must choose from a set of predefined allowed values.
- "Numeric" indicates only numbers are permitted as allowed values. All "Numeric" data elements must be positive numbers. Encoding a negative number or "0" will generate a deficiency.
- "String" indicates that series of letters/characters, numbers, symbols, and spaces are allowed values.

**JSON Data Element 'Required':** Indicates if the JSON schema requires a data attribute to be encoded. Note that your hospital is required to include all applicable standard charge information in your MRF in accordance with the regulation, regardless of whether or not the JSON schema 'requires' a data attribute to be encoded.

**CSV Data Element 'Blanks Accepted':** Indicates if the CSV format accepts blanks (e.g. lack of encoded data) for the corresponding data element. Note that your hospital is required to include all applicable standard charge information in your MRF in accordance with the regulation, regardless of whether or not the CSV format will accept blanks.
