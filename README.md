# NYC-YELLOW-TAXI-ANALYSIS

Analysis of New York City yellow taxi trips in 2022 and 2023 using PySpark, Microsoft Fabric and Power BI.

> ⚠️ **Note:** This project was developed for academic purposes. The notebooks, report and presentation are in **English**.

---

**Name of the repository:** NYC Yellow Taxi Analysis

🎓 **Context:**

David Abner Zuniga Montano and Thiago Pena Silverio developed this project for the Data Visualization module at City College Dublin. We used [NYC Taxi and Limousine Commission trip records](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) to find out how trip volume, journey time and passenger charges changed between 2022 and 2023.

📁 **Folders:**

**[Data](Data/):** Contains the [taxi-zone lookup](Data/reference/taxi_zone_lookup.csv) and a [manifest](Data/manifest.csv) with the source URL and checksum for each of the 24 monthly Parquet files. The [raw data ZIP](https://github.com/Thiago-Pena-Silverio/NYC-YELLOW-TAXI-ANALYSIS/releases/download/data-2022-2023/nyc-yellow-taxi-2022-2023-raw.zip) is available in Releases.

**[Notebooks](Notebooks/):** [Ingestion](Notebooks/Ingestion.ipynb) combines the monthly files and aligns their schemas. [Cleaning](Notebooks/Cleaning.ipynb) checks duplicates and timestamps, then builds the trip, date and location tables.

**[PowerBI](PowerBI/):** Contains the [Power BI report](PowerBI/Yellow_Taxi.pbix), a [three-page PDF preview](PowerBI/Report.pdf) and the [semantic model diagram](PowerBI/Semantic_Model.png).

**[Documentation](Documentation/):** Includes the [case study](Documentation/Case_Study.md), [project evidence](Documentation/Project_Evidence.pdf), [star schema](Documentation/Star_Schema.md) and [DAX measures](Documentation/DAX_Measures.md).

**[Presentation](Presentation/):** The [slide deck](Presentation/Yellow_Taxi_Trips.pptx) presents the findings and explains how to interpret the charts.

🛠️ **Tech Stack:**

- Microsoft Fabric Lakehouse
- Python and PySpark
- Parquet and Delta tables
- Power BI and DAX

🎖️ **Features:**

- Monthly and annual comparisons across 77,918,094 cleaned trip records 📅
- Pickup patterns by borough, using the TLC taxi-zone lookup 🗺️
- Fare and duration analysis showing how the average recorded charge rose from $21.66 to $28.46 while average journey time stayed close to 17 minutes 📊
- Data quality checks for duplicate trips, invalid timestamps and unusual values in recorded tips 🔎

---

🖥️ **How to Run**

**Requirements:**

- To view the results, open the [PDF report](PowerBI/Report.pdf) directly on GitHub.
- To run the notebooks, use a Microsoft Fabric workspace with Spark and a Lakehouse.
- To use the supplied PBIX, Power BI Desktop needs access to the original Fabric semantic model. The [schema](Documentation/Star_Schema.md) and [measures](Documentation/DAX_Measures.md) document how to build your own model.

**Instructions:** 💾

1. Download the project using **Code → Download ZIP** and extract `NYC-YELLOW-TAXI-ANALYSIS-main.zip`.
2. Download the separate raw data ZIP linked under **Data**. In a fresh Lakehouse, place the 24 Parquet files in `Files/raw/yellow_taxi/` and the lookup CSV in `Files/reference/taxi_zone_lookup.csv`.
3. Import both notebooks into Fabric and attach them to that Lakehouse. Run `Ingestion.ipynb` first, then `Cleaning.ipynb`.
4. Check the row counts against the project results. Ingestion produced **77,966,324** rows and cleaning retained **77,918,094** trips.
