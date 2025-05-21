# Meta-Data – **Dallas Animal Shelter (FY 2023-2025)**

---

## 1 · Dataset Description and Summary

| Item | Value |
|------|-------|
| **Dataset name** | Dallas Animal Shelter – Fiscal Years 2023-2025 |
| **Source** | City of Dallas Open Data (Socrata portal ID `uyte-zi7f`) |
| **Local file** | `Dallas_Animal_Shelter_Data_Fiscal_Year_2023-2025_20250514.csv` |
| **Records** | **64 780** (pull dated 14 May 2025) |
| **Columns** | **34** |
| **Date range** | 1 Oct 2023 → 14 May 2025 (`Intake_Date` → `Outcome_Date`) |

> **Description** – Raw “movement” feed from Dallas Animal Services’ Chameleon database. Each row is an intake or follow-up outcome for a single animal, with species/breed/colour, condition codes, timestamps, location fields, and staff identifiers.

### Data completeness (top gaps)

| Field | Null % | Action |
|-------|-------|--------|
| `Tag_Type` | **100 %** | Constant → drop |
| `Service_Request_Number` | 99.9 % | Drop |
| `Additional_Information` | 75.9 % | Retain as free-text note (optional) |
| `Activity_Number` | 64.7 % | Drop – internal audit field |
| `Outcome_Subtype` | 43 % | Keep (still informative) |
| Core analytical fields (`Animal_Type`, `Intake_Type`, `Outcome_Type`, `Intake_Condition`, `Outcome_Condition`) | 0 % | Fully populated |

---

## 2 · Selected Columns — Uniques & Samples

| Column | Type | Uniques | Sample values |
|--------|------|---------|---------------|
| `Animal_Type` | string | 3 | `DOG`, `CAT`, `WILDLIFE` |
| `Animal_Breed` | string | 278 | `PIT BULL`, `ROTTWEILER`, `MIXED BREED` |
| `Color` (from `Primary_Color`) | string | 180 | `BROWN/WHITE`, `BLACK`, `TAN/BLACK` |
| `Intake_Type` | string | 11 | `STRAY`, `OWNER SURRENDER`, `TREATMENT` |
| `Intake_Condition` | string | 5 | `APP WNL`, `APP INJ`, `APP SICK` |
| `Outcome_Type` | string | 16 | `TRANSFER`, `ADOPTION`, `EUTHANIZED` |
| `Outcome_Condition` | string | 5 | `APP SICK`, `APP WNL` |
| `Council_District` | string | 15 | `1`, `5`, `14` |
| `Intake_Date` + `Intake_Time` | date/HHMM | — | `2024-03-05`, `14:27` |
| `Outcome_Date` + `Outcome_Time` | date/HHMM | — | `2024-03-12`, `09:18` |

---

## 3 · Key Column Definitions

| Column | Definition |
|--------|------------|
| `Animal_Id` | Unique identifier used across all movements for the same animal. |
| `Activity_Number` / `Activity_Sequence` | Internal event counters – dropped in Silver. |
| `Intake_Type`, `Intake_Subtype` | Source and finer reason for arrival. |
| `Intake_Condition` / `Outcome_Condition` | Medical shorthand (APP WNL = within normal limits, APP INJ = injured, APP SICK = sick). |
| `Outcome_Type`, `Outcome_Subtype` | Final disposition after this movement (Adoption, Transfer, Euthanized…). |
| `Intake_Date` + `Intake_Time` | Arrival timestamp – combined in Silver. |
| `Outcome_Date` + `Outcome_Time` | Exit timestamp – combined in Silver. |
| `Time_in_Shelter_Days` | To be computed: `(Outcome - Intake) / 86 400`. |


---

## 4 · Transformation Notes (Silver Layer)

* **Drop constants / sparse** – `Tag_Type`, `Service_Request_Number`, `Activity_Number`, `Additional_Information` (optional).  
* **Datetime build** – combine date + time columns, convert to UTC; compute `time_in_shelter_days`, flag negatives.  
* **Text standardisation** – title-case & strip whitespace in:  
  `Animal_Type • Animal_Breed • Color • Intake_Type • Intake_Condition • Outcome_Type • Outcome_Condition`.  
* **Outcome grouping** – map 16 Dallas `Outcome_Type` values to five shared classes (Adoption, Return, Transfer, Euthanasia, Other).  
* **Age handling** – no explicit age column; will derive later via DOB once available, else treat as missing.  
* **Keep key** – `Animal_Id` + `Intake_Date` acts as event key; drop only exact duplicates.  

---

## 5 · Known Data-Quality Issues

* Multiple **timestamp formats** (`HH:MM` vs `H:MM`) – normalised in Silver.  
* Medical abbreviations (`APP WNL`, `APP INJ`) require decoding for readability in Gold.  
* No explicit age field – limits age-based adoption analysis unless DOB is provided in a future FY feed.

---

## 6 · Ethical Considerations

Outcome categories include euthanasia; results will be framed responsibly. We will avoid breed-based stigma when analysing `Outcome_Type` by `Animal_Breed`, presenting grouped statistics and context.


