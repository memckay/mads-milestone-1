# Milestone 1 Meta-Data – **Austin Animal Center Intakes + Outcomes**

---

## 1 · Dataset Description and Summary

| Item | Value |
|------|-------|
| **Dataset name** | Austin Animal Center — Intakes & Outcomes |
| **Source** | City of Austin Open Data (Socrata API) – Kaggle mirror |
| **Local file** | `aac_intakes_outcomes.csv` |
| **Records** | **79 672** |
| **Columns** | **41** |
| **Date range** | 1 Oct 2013 – 3 Apr 2018 (`intake_datetime` → `outcome_datetime`) |

> **Description** – Merged table of every animal intake and its corresponding outcome at the largest U.S. no-kill shelter. Fields cover species/breed/color, age buckets, health & intake context, final outcome, timestamps, and computed length-of-stay.

### Data completeness

| Field | Null % | Action |
|-------|-------|--------|
| `outcome_subtype` | **54 %** | Drop (too sparse) |
| `outcome_type` | 0.01 % (10 rows) | Impute **“Unknown”** or drop rows |
| `sex_upon_intake` / `sex_upon_outcome` | < 0.01 % (1 row each) | Impute **“Unknown”** |
| All others | 0 % | No action |

---

## 2 · Selected Columns – Uniques & Characteristics

| Column | Type | Uniques | Sample values |
|--------|------|---------|---------------|
| `animal_type` | string | 4 | Dog, Cat, Bird, Other |
| `breed` | string | 2 155 | Labrador Retriever Mix • Domestic Shorthair |
| `color` | string | 529 | Black/White • Brown Tabby |
| `intake_type` | string | 5 | Stray • Owner Surrender |
| `intake_condition` | string | 8 | Normal • Injured • Sick |
| `sex_upon_intake` | string | 5 | Spayed Female • Neutered Male |
| `age_upon_intake_age_group` | interval | 10 | `(-0.025 , 2.5]` • `(5.0 , 7.5]` • `(12.5 , 15.0]` |
| `age_upon_intake_(years)` | float | 45 | 0.3 • 4.0 • 12.0 |
| `outcome_type` | string | 9 | Adoption • Transfer • Return to Owner |
| `time_in_shelter_days` | float | 29 319 | 0.6 • 12.3 • 134.0 |

---

## 3 · Key Column Definitions

| Column | Definition |
|--------|------------|
| `animal_id` + `intake_number` | Composite key for each intake event (repeat visits keep unique `intake_number`). |
| `animal_type` | Species (Dog, Cat, Bird, Other). |
| `breed`, `color` | Free-text primary breed & coat pattern. |
| `sex_upon_intake` / `sex_upon_outcome` | Sterilization status at entry/exit. |
| `age_upon_intake_age_group` | Pre-bucketed age at intake (10 equal-width ≈2.5-year bins). |
| `age_upon_intake_(years)` | Numeric age at intake (float). |
| `intake_type` / `intake_condition` | Source & health condition at intake. |
| `outcome_type` | Final disposition (Adoption, Transfer, Return to Owner, Euthanasia, etc.). |
| `time_in_shelter_days` | Numeric duration (days) from intake to outcome. |
| `intake_datetime`, `outcome_datetime`, `date_of_birth` | ISO timestamps for event and DOB. |
---

## 4 · Transformation Notes (Silver Layer)

### 4.1 Duplicates & Missing
* Drop **exact** duplicate rows (ingestion artefacts); keep true repeat visits.  
* Drop `outcome_subtype`; impute tiny gaps (`outcome_type`, `sex_*`) to **"Unknown"**.

### 4.2 Categorical Cleaning
* Cleaned fields → `animal_type`, `breed`, `color`, `intake_type`, `intake_condition`, `sex_upon_intake`, `sex_upon_outcome`, `outcome_type`.  
* Operations → strip whitespace, title-case, merge trivial spelling/case variants.  
* Validation → compare unique sets before/after cleaning.

### 4.3 Datetime & Numeric
* Convert `intake_datetime`, `outcome_datetime`, `date_of_birth` to `datetime`; drop helper splits (`*_month`, `*_year`, etc.).  
* Keep `time_in_shelter_days`; filter negatives.

### 4.4 `time_in_shelter_days` distribution


---

## 5 · Known Data-Quality Issues

* Sparse `outcome_subtype` column.  
* Very high cardinality in `breed` and `color`; likely need “Other” buckets.  
* `found_location` is free text; geocoding would need external service.  
* Constant column `count` always 1 (drop).
---

## 6 · Ethical Considerations

Dataset includes sensitive outcomes (Euthanasia, Died). Analyses and visuals will avoid sensationalising mortality figures.  
* Location data will **not** be mapped at street-level to protect owner privacy.  
* Comparing outcome rates by **breed** may unintentionally reinforce stereotypes (“pit bulls are less adoptable”). We will frame breed findings carefully and avoid stigmatizing language.

---

