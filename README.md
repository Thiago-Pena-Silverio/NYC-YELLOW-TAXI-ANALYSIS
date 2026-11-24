# NYC Yellow Taxi Analysis

A data visualisation project by David Abner Zuniga Montano and Thiago Pena Silverio at City College Dublin. We used Microsoft Fabric, PySpark and Power BI to compare New York City yellow taxi journeys in 2022 and 2023.

## Results

We analysed 77,918,094 trips after cleaning 24 monthly files. Recorded trips fell by 3.4% from 2022 to 2023, while the average recorded passenger charge rose from $21.66 to $28.46. Average journey time stayed close to 17.4 minutes. The [report preview](PowerBI/Report.pdf) shows the annual comparison, pickup locations and monthly trends.

## Project files

| Component | Files |
| --- | --- |
| Data | [24 monthly Parquet files as a ZIP](https://github.com/Thiago-Pena-Silverio/NYC-YELLOW-TAXI-ANALYSIS/releases/download/data-2022-2023/nyc-yellow-taxi-2022-2023-raw.zip), [source URLs and SHA-256 checksums](Data/manifest.csv), [taxi-zone lookup](Data/reference/taxi_zone_lookup.csv) |
| PySpark notebooks | [Ingestion](Notebooks/Ingestion.ipynb) and [cleaning, validation and dimensional modelling](Notebooks/Cleaning.ipynb) |
| Power BI | [Report file](PowerBI/Yellow_Taxi.pbix), [PDF preview](PowerBI/Report.pdf) and [semantic model diagram](PowerBI/Semantic_Model.png) |
| Documentation | [Case study](Documentation/Case_Study.md), [project evidence](Documentation/Project_Evidence.pdf), [star schema](Documentation/Star_Schema.md) and [DAX measures](Documentation/DAX_Measures.md) |
| Presentation | [Yellow Taxi Trips slide deck](Presentation/Yellow_Taxi_Trips.pptx) |

## Run the analysis

1. Create a Microsoft Fabric Lakehouse. Place the 24 Parquet files in `Files/raw/yellow_taxi/` and the zone lookup in `Files/reference/taxi_zone_lookup.csv`.
2. Import the ingestion and cleaning notebooks into Fabric and attach both to the Lakehouse. Run Ingestion first in a fresh Lakehouse, then Cleaning. The expected counts are 77,966,324 input rows and 77,918,094 cleaned trips.
3. For a new semantic model, follow the relationships and DAX measures in the documentation. The supplied PBIX uses a live connection to the original Fabric model and requires access to that model. The PDF includes all three report pages and opens independently.

## Data source

The NYC Taxi and Limousine Commission publishes the monthly trip records and field definitions. Recorded charges exclude cash tips. [TLC trip record data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)


