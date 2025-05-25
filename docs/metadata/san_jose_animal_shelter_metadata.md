# Meta-Data – **San Jose Animal Shelter Outcomes (2024–2025)**

---

## 1 · Dataset Description and Summary

| Item                 | Value                                                                                                      |
|----------------------|------------------------------------------------------------------------------------------------------------|
| **Dataset name**     | San Jose Animal Shelter Outcomes (2024–2025)                                                               |
| **Source**           | City of San José Open Data Portal ([Animal Shelter Outcomes](https://data.sanjoseca.gov/dataset/animal-shelter-intake-and-outcomes/resource/f3354a37-7e03-41f8-a94d-3f720389a68a)
)                 |
| **Access method**    | Download CSV via Socrata export or API pull                                                                |
| **Local file**       | `san_jose_animal_shelter_outcomes_20250524.csv`                                                            |
| **Records**          | **16 274** (snapshot dated 24 May 2025)                                                                    |
| **Columns**          | **22**                                                                                                     |
| **Date range**       | 1 Jul 2024 → 24 May 2025 (`IntakeDate` → `OutcomeDate`)                                                     |

> **Description** – Each row represents an intake or outcome event at San José Animal Shelter, including identifiers, demographics, intake/outcome types and conditions, and timestamps for tracking outcomes and lengths of stay.

### Data completeness (top gaps)

| Field              | Null % | Action                                         |
|--------------------|--------|------------------------------------------------|
| `SecondaryColor`   | ~58%   | Keep (useful for color-based analysis)         |
| `Age`              | ~70%   | Parsed later into `age_years` in Silver layer |
| `IntakeSubtype`    | ~20%   | Keep (adds source detail)                      |
| `IntakeReason`     | ~65%   | May require further grouping                   |
| `LastUpdate`       | ~10%   | Keep for provenance, not used in analysis      |

---

## 2 · Columns – Unique Values & Sample Characteristics

| Column           | Type               | Uniques | Sample values                       |
|------------------|--------------------|---------|-------------------------------------|
| `_id`            | integer            | 10 000  | 1, 2, 3…                            |
| `AnimalID`       | string             | 10 000  | A0075579, A0081234, A0098765        |
| `AnimalType`     | string             | 5       | DOG, CAT, BIRD, OTHER, LIVESTOCK    |
| `PrimaryBreed`   | string             | ~200    | LABRADOR RETR, DOMESTIC SHORTHAIR   |
| `PrimaryColor`   | string             | ~50     | BLACK, TRICOLOR, BRINDLE            |
| `Sex`            | string             | 5       | MALE, FEMALE, NEUTERED, SPAYED, UNKNOWN |
| `DOB`            | string             | ~1 000  | 2018-06-15, 2020-01-03               |
| `Age`            | string             | ~66     | 7 MONTHS, 2 WEEKS, NO AGE           |
| `IntakeDate`     | datetime64[ns]     | —       | 2024-07-01, 2024-12-15              |
| `IntakeType`     | string             | ~12     | STRAY, OWNER SURRENDER, TRANSFER    |
| `IntakeCondition`| string             | ~10     | HEALTHY, MED EMERG, AGGRESSIVE      |
| `IntakeReason`   | string             | ~25     | BEHAVIOR, MEDICAL, OTHER            |
| `OutcomeDate`    | datetime64[ns]     | —       | 2024-07-05, 2025-05-24              |
| `OutcomeType`    | string             | ~10     | ADOPTION, TRANSFER, EUTHANIZED      |
| `OutcomeCondition`| string            | ~8      | HEALTHY, MEDICAL, DECEASED          |

---

## 3 · Key Column Definitions

| Column               | Definition                                                                             |
|----------------------|----------------------------------------------------------------------------------------|
| `_id`                | Internal record identifier                                       |
| `AnimalID`           | Unique animal identifier across all events.                                           |
| `AnimalName`         | Given or assigned name, if any.                                                       |
| `AnimalType`         | Species category (DOG, CAT, BIRD).                                             |
| `PrimaryBreed`       | Reported breed or mix.                                                                |
| `PrimaryColor`       | Dominant coat color.                                                                  |
| `Sex`                | Sex and sterilization status.                                                         |
| `DOB`                | Date of birth, as provided.                                                           |
| `Age`                | Raw age string (“7 MONTHS”), parsed later.                                      |
| `IntakeDate`         | Date when animal entered shelter.                                                     |
| `IntakeType`         | Broad intake category (STRAY, TRANSFER).                                        |
| `IntakeCondition`    | Intake health/behavior code (MED SEV).                                          |
| `IntakeReason`       | More specific intake rationale (MEDICAL, BEHAVIOR).                             |
| `OutcomeDate`        | Date when final disposition occurred.                                                 |
| `OutcomeType`        | Outcome category (ADOPTION, EUTHANIZED).                                        |
| `OutcomeCondition`   | Health/behavior at outcome (HEALTHY, DECEASED).                                 |
| `Crossing`           | Location where animal was found or intake occurred.                                    |
| `Jurisdiction`       | Geopolitical area of intake/outcome.                                                  |
| `LastUpdate`         | Timestamp of last record modification (provenance).                                   |

---

## 4 · Transformation Notes (Silver Layer)

* **Drop Unused Fields** – remove `SecondaryColor`, `LastUpdate` (provenance only).  
* **Date Parsing** – convert `IntakeDate` & `OutcomeDate` to `datetime64[ns]`.  
* **Age Parsing** – derive numeric `age_years` from `Age`.  
* **Category Mapping** – apply `VALUE_MAPPINGS` to harmonize intake/outcome codes.  
* **Text Clean-Up** – strip & title-case string columns: `AnimalType`, `PrimaryBreed`, etc.  
* **Dtype Enforcement** – cast categories to `category` and dates to `datetime64`.  
* **Schema Ordering** – enforce `FINAL_SCHEMA` order.  

---

## 5 · Ethical Considerations

Includes animal euthanasia events; analyses will contextualize these outcomes responsibly and avoid attributing judgments without operational context.  
I have