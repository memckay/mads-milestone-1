# Meta-Data – **Sonoma County Animal Shelter Intake & Outcome**

---

## 1 · Dataset Description and Summary

| Item | Value |
|------|-------|
| **Dataset name** | Animal Shelter Intake & Outcome |
| **Source** | Sonoma County Open Data Portal ([Animal Shelter Intake & Outcome](https://data.sonomacounty.ca.gov/Government/Animal-Shelter-Intake-and-Outcome/924a-vesw)) |
| **Access method** | Download CSV from portal |
| **Local file** | `SoCo_Animal_Shelter_Intake_and_Outcome_20250519.csv` |
| **Records** | **30 554** (pull dated 19 May 2025) |
| **Columns** | **24** |
| **Date range** | 16 Aug 2013 → 18 May 2025 (`Intake Date` → `Outcome Date`) |

> **Description** – Raw intake and outcome events for animals at the Sonoma County shelter. Each row captures a single intake or outcome event, including the animal’s ID, demographics, timestamps, location, and condition codes.

### Data completeness (top gaps)

| Field | Null % | Action |
|-------|--------|--------|
| `Date Of Birth`      | ~ 85 % | Drop or impute later for age derivation |
| `Impound Number`     | ~ 50 % | Drop (internal tracking) |
| `Kennel Number`      | ~ 40 % | Optional retention for location analyses |
| `Outcome Subtype`    | ~ 20 % | Keep (adds outcome detail) |
| Core analytical fields (`Animal ID`, `Type`, `Intake Type`, `Outcome Type`, `Intake Condition`, `Outcome Condition`) | 0 % | Fully populated |

---

## 2 · Selected Columns — Uniques & Samples

| Column            | Type    | Uniques | Sample values                  |
|-------------------|---------|---------|--------------------------------|
| `Animal ID`       | string  | 30 550  | `A12345`                       |
| `Type`            | string  | 2       | `DOG`, `CAT`                   |
| `Breed`           | string  | ~ 150   | `LABRADOR`, `DOMESTIC SHORTHAIR` |
| `Color`           | string  | ~ 30    | `BLACK`, `BROWN`, `TRICOLOR`   |
| `Sex`             | string  | 3       | `M`, `F`, `Unknown`            |
| `Size`            | string  | ~ 4     | `Small`, `Medium`, `Large`     |
| `Date Of Birth`   | date    | —       | `2019-08-15`                   |
| `Intake Date`     | date    | —       | `2025-03-01`                   |
| `Outcome Date`    | date    | —       | `2025-04-10`                   |
| `Intake Type`     | string  | ~ 8     | `STRAY`, `OWNER SURRENDER`     |
| `Outcome Type`    | string  | ~ 6     | `ADOPTION`, `TRANSFER`, `DECEASED` |

---

## 3 · Key Column Definitions

| Column                | Definition                                                                                |
|-----------------------|-------------------------------------------------------------------------------------------|
| `Animal ID`           | Unique identifier for each animal across all events.                                      |
| `Name`                | Given name of the animal (if known).                                                     |
| `Type`                | Species category (DOG, CAT).                                                       |
| `Breed`               | Primary breed or mix description.                                                        |
| `Color`               | Primary coat color.                                                                       |
| `Sex`                 | Sex of the animal (M/F) or Unknown.                                                      |
| `Size`                | Size category (Small/Medium/Large).                                                       |
| `Date Of Birth`       | Recorded birth date—used later to derive age.                                            |
| `Intake Date`         | Date when the animal entered the shelter.                                                |
| `Outcome Date`        | Date when the animal exited (adoption, transfer, etc.).                                  |
| `Intake Type`         | Reason or channel of intake (Stray, Owner Surrender, etc.).                              |
| `Intake Condition`    | Medical/behavioral shorthand at intake (APP WNL, APP INJ, etc.).                          |
| `Outcome Type`        | Final disposition (Adoption, Transfer, Euthanasia, etc.).                                |
| `Outcome Condition`   | Medical/behavioral shorthand at outcome.                                                 |
| `Location`            | Facility or jurisdiction where the intake/outcome occurred.                              |
| `Count`               | Always “1” for each record—dropped in Silver.                                            |

---

## 4 · Transformation Notes (Silver Layer)

* **Column Pruning** – drop low-value or constant fields:  
  `Count`, `Name`, `Impound Number`, `Kennel Number`, `Location`.  
* **Date Parsing** – convert `Intake Date` and `Outcome Date` to `datetime64[ns]`.  
* **Text Standardization** – strip whitespace and title-case in:  
  `type`, `breed`, `color`, `sex`, `size`, `intake_type`, `intake_condition`, `outcome_type`, `outcome_condition`.  
* **Category Mapping** – apply `VALUE_MAPPINGS` for intake/outcome fields to unify terminology.  
* **Dtype Enforcement** – cast mapped fields to `category` and dates to `datetime64` per `SILVER_DTYPES`.  
* **Schema Ordering** – reorder to `FINAL_SCHEMA` for a consistent Silver schema.  

---

## 5 · Ethical Considerations

Outcome categories include euthanasia; analyses will carefully contextualize these actions and avoid breed-based stigma by presenting aggregated rates alongside known limitations in breed identification accuracy and regional reporting variations.
