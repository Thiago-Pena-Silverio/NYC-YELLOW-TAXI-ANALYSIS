# Semantic Model and DAX Measures

## Model status

The current Fabric model is `SM_YellowTaxiTrips_2022_2023`. The model view shows `fact_trips`, `dim_date`, `dim_pickup_location`, and `dim_dropoff_location`, connected through three active many-to-one relationships. Six measures are visible in the `fact_trips` table. A DAX query directly confirmed `Total Trips = 77,918,094`, which matches the Silver row count.

The current report and final client brief show the summary values below. Only the total-trip query result is separately confirmed in the project evidence; the other values should be understood as report results from the current project export rather than independent DAX query validation.

## DAX measures

| Measure | DAX | Meaning |
|---|---|---|
| Total Trips | `Total Trips = COUNTROWS(fact_trips)` | Counts the cleaned trip rows. |
| Total Revenue | `Total Revenue = SUM(fact_trips[total_amount])` | Sums the source's recorded passenger charge amount. |
| Total Tips | `Total Tips = SUM(fact_trips[tip_amount])` | Sums tips recorded in TLC data (credit-card tips). |
| Average Revenue per Trip | `Average Revenue per Trip = DIVIDE([Total Revenue], [Total Trips])` | Average recorded charge per trip. |
| Average Trip Distance | `Average Trip Distance = CALCULATE(AVERAGE(fact_trips[trip_distance]), fact_trips[trip_distance] > 0)` | Average distance for positive-distance trips. |
| Average Trip Duration (Minutes) | `Average Trip Duration (Minutes) = AVERAGEX(fact_trips, DATEDIFF(fact_trips[pickup_datetime], fact_trips[dropoff_datetime], SECOND) / 60.0)` | Mean duration in minutes. |

## Reported values by year

| Year | Trips | Recorded charges | Recorded tips | Average charge/trip | Average distance | Average duration |
|---|---:|---:|---:|---:|---:|---:|
| 2022 | 39,623,537 | $858,415,969.74 | $286,884,631.35 | $21.66 | 6.04 mi | 17.33 min |
| 2023 | 38,294,557 | $1,089,870,328.96 | $134,920,017.83 | $28.46 | 4.17 mi | 17.46 min |

By year, trips fell 3.4%, recorded charges rose 27%, distance declined, and average duration remained near 17.4 minutes. These patterns do not show what caused the changes.

## Interpretation

TLC defines `tip_amount` as credit-card tips; cash tips are not included. `total_amount` also excludes cash tips (New York City Taxi and Limousine Commission, 2025). Use “recorded revenue/charges” and “recorded tips,” not “total driver income.” Fare-component mismatches were profiled but no values were recalculated or overwritten.

## PBIX report connection

Fabric allowed the report to be downloaded as a `.pbix` with a live connection. The semantic model with imported data cannot be downloaded because it is Direct Lake and configured for large datasets (Microsoft, n.d.). The PBIX needs access to the online Fabric model and does not contain a copy of the data.

## References

Microsoft (n.d.) [Power BI PBIX export guidance](https://learn.microsoft.com/power-bi/create-reports/service-export-to-pbix).

New York City Taxi and Limousine Commission (2025) [Yellow Taxi data dictionary](https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf).
