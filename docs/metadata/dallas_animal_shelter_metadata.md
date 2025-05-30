# Meta-Data – **Dallas Animal Shelter (FY 2023-2025)**

---

## 1 · Dataset Description and Summary

| Item | Value |
|------|-------|
| **Dataset name** | Dallas Animal Shelter – Fiscal Years 2023-2025 |
| **Source** | City of Dallas Open Data Portal ([Dallas Animal Shelter Data – FY 2023-2025](https://www.dallasopendata.com/Services/Dallas-Animal-Shelter-Data-Fiscal-Year-2023-2025/uyte-zi7f/about_data)) |
| **Access method** | Download CSV from portal |
| **Local file** | `Dallas_Animal_Shelter_Data_Fiscal_Year_2023-2025_20250514.csv` |
| **Records** | **65063** (pull dated 14 May 2025) |
| **Columns** | **34** |
| **Date range** | 1 Oct 2023 → 14 May 2025 (`Intake_Date` → `Outcome_Date`) |

> **Description** – Raw “movement” feed from Dallas Animal Services’ database. Each row is for a single animal, with species/breed/colour, condition codes, timestamps, location fields, and staff identifiers.

### Data completeness (top gaps)

| Field | Null % | Action |
|-------|--------|--------|
| `Tag_Type`                | **100 %** | Constant → drop |
| `Service_Request_Number`  | 99.9 %     | Drop |
| `Additional_Information`  | 75.9 %     | Retain as free-text note (optional) |
| `Activity_Number`         | 64.7 %     | Drop – internal audit field |
| `Outcome_Subtype`         | 43 %       | Keep (still informative) |
| Core analytical fields (`Animal_Type`, `Intake_Type`, `Outcome_Type`, `Intake_Condition`, `Outcome_Condition`) | 0 % | Fully populated |

---

## 2 · Selected Columns — Uniques & Samples

| Column                      | Type       | Uniques | Sample values                         |
|-----------------------------|------------|---------|---------------------------------------|
| `Animal_Type`               | string     | 3       | `DOG`, `CAT`, `WILDLIFE`              |
| `Animal_Breed`              | string     | 278     | `PIT BULL`, `ROTTWEILER`, `MIXED BREED` |
| `Color` (from `Primary_Color`) | string | 180     | `BROWN/WHITE`, `BLACK`, `TAN/BLACK`   |
| `Intake_Type`               | string     | 11      | `STRAY`, `OWNER SURRENDER`, `TREATMENT` |
| `Intake_Condition`          | string     | 5       | `APP WNL`, `APP INJ`, `APP SICK`      |
| `Outcome_Type`              | string     | 16      | `TRANSFER`, `ADOPTION`, `EUTHANIZED`  |
| `Intake_Date` + `Intake_Time`   | date/HHMM | —   | `2024-03-05`, `14:27`                 |
| `Outcome_Date` + `Outcome_Time` | date/HHMM | —   | `2024-03-12`, `09:18`                 |

---

## 3 · Key Column Definitions

| Column                            | Definition                                                                          |
|-----------------------------------|-------------------------------------------------------------------------------------|
| `Animal_Id`                       | Unique identifier used across all movements for the same animal.                    |
| `Activity_Number` / `Activity_Sequence` | Internal event counters – dropped in Silver.                                |
| `Intake_Type`, `Intake_Subtype`   | Source and finer reason for arrival.                                              |
| `Intake_Condition` / `Outcome_Condition` | Medical shorthand (APP WNL = within normal limits, APP INJ = injured, APP SICK = sick). |
| `Outcome_Type`, `Outcome_Subtype` | Final disposition after this movement (Adoption, Transfer, Euthanized…).          |
| `Intake_Date` + `Intake_Time`      | Arrival timestamp – combined in Silver.                                            |
| `Outcome_Date` + `Outcome_Time`    | Exit timestamp – combined in Silver.                                               |

---

## 4 · Transformation Notes (Silver Layer)

* **Column Pruning** – drop low-value or constant fields:  
  `Tag_Type`, `Service_Request_Number`, `Activity_Number`, `Additional_Information`.

* **Datetime Consolidation** – merge date + time into unified timestamp fields:  
  - Create `intake_datetime` from `Intake_Date` + `Intake_Time`  
  - Create `outcome_datetime` from `Outcome_Date` + `Outcome_Time`  
  - Cast both to `datetime64[ns]`

* **Text Clean-Up** – strip whitespace and apply title-case to key string columns:  
  `animal_type`, `breed`, `primary_color`, `intake_type`, `intake_condition`, `outcome_type`.

* **Category Mapping** – standardize raw codes into unified categories using `VALUE_MAPPINGS` for:  
  `intake_type`, `intake_condition`, `intake_reason`, and `outcome_type`.

* **Dtype Enforcement** – cast mapped categorical fields to `category` and timestamp columns to `datetime64[ns]` per `SILVER_DTYPES`.

* **Schema Ordering** – reorder to the agreed `FINAL_SCHEMA` list for a consistent Silver schema.

---

## 5 · Ethical Considerations

Outcome categories include euthanasia; results will be framed responsibly. We will avoid breed-based stigma when analysing `Outcome_Type` by `Animal_Breed`, presenting grouped statistics with context.