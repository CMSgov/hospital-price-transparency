| Scenario | Reference in [Wide CSV Format Example](CSV/Wide%20Format%20Examples) | Reference in [Tall CSV Format Example](CSV/Tall%20Format%20Examples) | Reference in [JSON Format Example](JSON/) |
| ----- | ---- | ---- | ---------- |
| Multiple hospital locations | Row 2, `hospital_location` | Row 2, `hospital_location` | Lines 5-7 |
| Case rate: MS-DRG algorithm displayed multiple ways | Rows 4-6, Platform Health Insurance PPO | Rows 4-6 | Lines 41-62 |
| Percent of total billed charges | Rows 4-6, Region Health Insurance HMO | Row 7 | Lines 65-69 |
| Fee schedule: Standard charge is a percent of a common fee schedule where the standard charge dollar amount can be calculated | Row 7, Platform Health Insurance PPO | Row 8 | Lines 92-96 |
| Fee schedule: Standard charge is a percent of a common fee schedule where the standard charge dollar amount cannot be calculated | Row 7, Region Health Insurance HMO  | Row 9 | Lines 99-104 |
| Per diem: Standard charge does not vary with length of stay | Row 8, Platform Health Insurance PPO | Row 10 | Lines 127-130 |
| Per diem: Standard charges based on length of stay | Rows 9-11, Region Health Insurance HMO | Rows 11-13 | Lines 133-151 |


#### Additional Notes
* To view the raw CSV file, select “Code” at the top of the example.
* The CSV examples present the data headers in row three in an order that differs from the CSV templates. Changing the order of the data headers will not generate a deficiency.
