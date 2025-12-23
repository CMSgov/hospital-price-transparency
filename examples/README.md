| **Scenario** | **Reference in [Wide CSV Format Example](./CSV/Wide%20Format%20Examples/)** | **Reference in [Tall CSV Format Example](./CSV/Tall%20Format%20Examples/)** | **Reference in [JSON Format Example](./JSON/)** |
| --- | --- | --- | --- |
| Encoding multiple hospital location names | Row 2, location_name | Row 2, location_name | Line 5 |
| Encoding multiple Type 2 NPIs | Row 2, type_2_npi | Row 2, type_2_npi | Line 14 |
| Encoding a plan’s stop loss provision for outliers that span multiple items or services using the "General Contract Provisions" data element | Row 2, general_contract_provisions | Row 2, general_contract_provisions | Lines 525-534 |
| Encoding percent of total billed charges with more than 10 allowed amounts observed during the lookback period | Row 4, Platform Health Insurance PPO | Row 4 | Lines 40-47 |
| Encoding percent of total billed charges with zero allowed amounts observed during the lookback period | Row 5, Platform Health Insurance PPO | Row 6 | Lines 82-87 |
| Encoding a dollar amount that is further modified by an algorithm with more than 10 allowed amounts observed during the lookback period | Row 4, Region Health Insurance HMO | Row 5 | Lines 50-59 |
| Encoding percent of total billed changes that is further modified by an algorithm with between 1 and 10 allowed amounts observed during the lookback period | Row 5, Region Health Insurance HMO | Row 7 | Lines 90-98 |
| Encoding a fee schedule where the standard charge is a percent of a fee schedule where the standard charge dollar amount can be calculated | Row 6, Platform Health Insurance PPO and Region Health Insurance HMO | Rows 8 - 9 | Lines 121-132 |
| Encoding a per diem where the standard charge does not vary with length of stay | Row 7, Platform Health Insurance PPO | Row 10 | Lines 155-158 |
| Encoding a per diem where the standard charge varies with length of stay | Rows 8-10, Region Health Insurance HMO | Rows 11-13 | Lines 161-179 |
| Encoding a simple case rate | Row 11, Region Health Insurance HMO | Row 16 | Lines 216-219 |
| Encoding two different case rates for the same code within a payer and plan and providing contextual information explaining why the standard charges are different | Rows 11-12, Platform Health Insurance PPO | Rows 14-15 | Lines 202-213 |
| Encoding modifier information for a single modifier in one row/object | Rows 13-14 | Rows 17-20 | Lines 476-504 |
| Encoding modifier information for multiple modifiers in one row/object | Row 15 | Rows 21-22 | Lines 509-520 |
| Encoding drug unit of measurement and drug type of measurement using the "Description" data element to provide more detail | Rows 16-22 | Rows 23-34 | Lines 226-467 |

#### Additional Notes

- To view the raw CSV file, select "Code" at the top of the example.

- The CSV examples present the data headers in row three in an order that differs from the CSV templates. Changing the order of the data headers will not generate a deficiency.
