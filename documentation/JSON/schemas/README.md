### Guidance related to JSON schema 2.0 and versions

#### [V2.0.0](./V2.0.0_Hospital_price_transparency_schema.json) – CY24 OPPS/ASC FR Version​
This version of the JSON schema includes data dictionary technical specifications related to data elements and value encoding that are required beginning on 7/1/2024 and 1/1/2025. However, this version of the JSON schema does not include ‘conditional’ checks that are required as of 7/1/2004 and 1/1/2025. Therefore, users of this schema are responsible for ensuring that their file meets all the data dictionary technical specifications, including the ‘conditional’ checks that become effective on 7/1/2024 and 1/1/2025. Users should check for errors using the validator tool found here: https://cmsgov.github.io/hpt-tool/
​
#### [V2.1.0](./V2.1.0_Hospital_price_transparency_schema.json) – July 1, 2024 Implementation date *New – 3/28/2024* ​
This version of the JSON schema includes data dictionary technical specifications related to data elements and value encoding that are required beginning on 7/1/2024. Additionally, this version of the JSON schema embeds the ‘conditional’ checks that align with the July 1, 2024 implementation date. Users of this schema will be responsible for ensuring the file meets all the data dictionary technical specifications (including the data elements and ‘conditional’ checks) that become effective 1/1/2025. Users should check for errors using the validator tool found here: https://cmsgov.github.io/hpt-tool/
​

#### [V2.2.0](./V2.2.0_Hospital_price_transparency_schema.json) – January 1, 2025 Implementation date *New – 3/28/2024* ​
This version of the JSON schema includes all data dictionary technical specifications related to data elements, value encoding, and conditional checks that are required for implementation beginning 7/1/2024 and 1/1/2025. Users of this schema will not have to perform any additional manual changes to their file to meet all data dictionary technical specifications that become effective beginning 7/1/2024 and 1/1/2025. Users should check for errors using the validator tool found here: https://cmsgov.github.io/hpt-tool/

### JSON 2.0 Version differences

| Version/Data dictionary requirements | Data elements and value encoding specifications effective 7/1/2024 | Conditional checks effective 7/1/2024 | Data elements and value encoding specifications effective 1/1/2025 | Conditional checks effective 1/1/2025 | 
| ------------- | --------------- |  --------------- |  --------------- |  --------------- | 
| 2.0.0 | Includes | X | Includes | X |
| 2.1.0 | Includes | Includes | X | X |
| 2.2.0 | Includes | Includes | Includes | Includes |