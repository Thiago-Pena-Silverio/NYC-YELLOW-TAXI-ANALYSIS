# Star Schema and Relationships

## Fact table grain

`fact_trips` contains one row per cleaned Yellow Taxi trip. Trip dates, pickup/drop-off locations, distance, duration, and recorded amounts are kept at this grain.

## Model tables

| Table | Role | Key / useful fields | Rows |
|---|---|---|---:|
| `fact_trips` | Trip facts | `date_key`, `pickup_location_id`, `dropoff_location_id`, trip and fare fields | 77,918,094 |
| `dim_date` | Calendar dimension | `date_key`, date, month, year | 730 |
| `dim_pickup_location` | Pickup zone labels | `location_id`, Borough, Zone, service_zone | 265 |
| `dim_dropoff_location` | Drop-off zone labels | `location_id`, Borough, Zone, service_zone | 265 |

## Relationships

Each relationship is active, many-to-one from the fact to its dimension, and filters from the dimension to the fact:

- `dim_date[date_key]` → `fact_trips[date_key]`
- `dim_pickup_location[location_id]` → `fact_trips[pickup_location_id]`
- `dim_dropoff_location[location_id]` → `fact_trips[dropoff_location_id]`


The pickup and drop-off tables are two role-playing copies of the same 265-row TLC zone lookup. They allow analysis of each end of a trip without creating two paths through one location table.

## Validation notes

The source lookup contained 265 distinct `LocationID` values, with zero null IDs or duplicate-ID groups. Profiling found no unmatched pickup or drop-off IDs. The date dimension has one row for each calendar day in the two-year period (730 rows).

The Fabric model view on 20 November 2026 showed these four tables and all three many-to-one relationships. The fact table contains the six measures documented in `Semantic_Model_and_DAX_Measures`.

## Reference

New York City Taxi and Limousine Commission (n.d.) *TLC Trip Record Data*. Available at: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page (Accessed: 20 November 2026).

