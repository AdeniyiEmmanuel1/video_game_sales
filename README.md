# **Video Game Sales — ETL Pipeline**
Welcome to this project repository

This project demonstrates a comprehensive data engineering and analytics solution built on SQL Server, covering the full pipeline from raw CSV ingestion to a clean, query-ready star schema. It highlights industrial best practices in data extraction, transformation, quality management, and BI-ready data modelling.

---

## **Project Requirements**

### Building the Data Warehouse (Data Engineering)

## **Objective**

Develop a structured ETL data warehouse using SQL Server to consolidate video game sales data sourced from a CSV file, enabling analytical reporting and informed decision making across game titles, platforms, genres, and publishers spanning **1980 to 2020**.

#### Specifications

- **Data Sources** | Importing raw data from a flat CSV file (`vgsales.csv`) containing **11,493 game titles** across **31 platforms**, **12 genres**, and **579 publishers**
- **Data Quality** | Cleaning and resolving data quality issues prior to analysis — including NULL normalisation, type validation, year range checks, duplicate removal, and global sales recalculation from regional totals
- **Integration** | Combining all source fields into a single, user-friendly star schema (fact + dimension tables) designed for analytical queries
- **Scope** | Focus on the latest available dataset only; full historical change tracking is not required
- **Documentation** | Clear documentation of the pipeline architecture, transformation rules, and data model provided to support both business stakeholders and analytics teams

---

# **BI: Analytics & Reporting (Data Analytics)**

#### Objectives

Develop SQL-based analytics to deliver detailed insights into:

- **Game Performance** — identify top-selling titles by global and regional sales volumes
- **Platform Trends** — measure unit sales distribution across all 31 gaming platforms
- **Genre & Publisher Analysis** — rank genres and publishers by total and regional sales contribution
- **Zone Sales Over Time** — track year-on-year sales trends by region (NA, EU, JP, Other) from 1980 to 2020

These insights empower stakeholders with key business metrics enabling strategic decisions around catalogue investment, regional marketing, and platform prioritisation.

---

## **Pipeline Architecture**

```
[ vgsales.csv ]
      │
      ▼
┌──────────────────────┐
│  SECTION 1: EXTRACT  │   Schema : raw
│  raw.vgsales_import  │   All columns VARCHAR — zero-rejection landing zone
└────────┬─────────────┘
         │
         ▼
┌────────────────────────────┐
│  SECTION 2: TRANSFORM      │   Schema : staging
│  staging.vgsales_          │   Cleanse · Validate · Enrich · Deduplicate
│  clean_stage               │
└────────┬───────────────────┘
         │
         ▼
┌──────────────────────────────────────────────┐
│  SECTION 3: LOAD  (Clean Data)               │   Schema : clean
│  clean.dim_platform   clean.dim_genre        │   Star schema
│  clean.dim_publisher  clean.fact_vgsales     │   FK constraints + indexes
└──────────────────────────────────────────────┘
```

---

## **Data Model**

| Table | Schema | Type | Description |
|---|---|---|---|
| `vgsales_import` | `raw` | Landing | Raw CSV rows, all VARCHAR, no transformations |
| `vgsales_clean_stage` | `staging` | Staging | Cleansed, validated, quality-flagged rows |
| `dim_platform` | `clean` | Dimension | Unique gaming platforms (Wii, PS2, X360, etc.) |
| `dim_genre` | `clean` | Dimension | Unique genres (Action, Sports, Shooter, etc.) |
| `dim_publisher` | `clean` | Dimension | Unique publishers (Nintendo, EA, Activision, etc.) |
| `fact_vgsales` | `clean` | Fact | Sales figures in millions of units per game |

---

## **License**

This project is licensed under the MIT License. You are free to use, modify, and share this project with proper attribution.
