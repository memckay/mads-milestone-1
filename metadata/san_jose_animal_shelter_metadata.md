# Milestone 1 Meta-Data Document

---

## Section 1: Dataset Description and Summary

**Dataset Name:** San Jose Animal Shelter Outcomes (2024–2025)  
**Source:** San Jose Animal Shelter  
**File Name:** san-jose-animal-shelter-outcomes.csv  
**Total Records:** 15,688  
**Total Columns:** 26  
**Date Range:** Primarily covers outcomes from 2024 to 2025  

**Description:**  
This dataset records the final outcomes of animals housed at the San Jose Animal Shelter. It includes information such as outcome type, subtype, conditions, dates, and identifiers associated with the animal. This data can support outcome analysis, policy review, mortality trend tracking, and foster/adoption program evaluation.

**Data Completeness:**  
- Some fields may contain missing or unknown values such as outcome subtype or condition.  
- Additional verification may be needed for geospatial and derived fields.  

---

## Section 2: Columns – Unique Values and Characteristics

| Column Name      | Data Type | Unique Values | Missing Values | Sample Values                               |
|------------------|-----------|---------------|----------------|---------------------------------------------|
| AnimalID         | object    | 13,558        | 0              | A0075579, A0533827, A0538570                |
| AnimalName       | object    | 3,102         | 7,413          | BAILEY, PATCHES, CARAMEL                    |
| AnimalType       | object    | 5             | 0              | DOG, CAT, OTHER, BIRD, LIVESTOCK            |
| PrimaryColor     | object    | 57            | 0              | BLACK, TRICOLOR, CALICO-TRI                 |
| SecondaryColor   | object    | 32            | 9,406          | RED, BLACK, ORANGE, WHITE, TAN              |
| PrimaryBreed     | object    | 225           | 0              | LABRADOR RETR, PARSON RUSS TER, DOMESTIC SH |
| Sex              | object    | 5             | 0              | SPAYED, NEUTERED, MALE, FEMALE, UNKNOWN     |
| DOB              | object    | 2,072         | 6,644          | 1/16/1994, 2/6/2006, 6/1/2007                |
| Age              | object    | 66            | 0              | 16 YEARS, 19 YEARS, NO AGE                  |
| IntakeDate       | object    | 315           | 0              | 10/15/2024, 8/28/2024, 9/30/2024            |
| IntakeCondition  | object    | 13            | 0              | MED R, MED SEV, DEAD, MED EMERG, HEALTHY    |
| IntakeType       | object    | 12            | 0              | STRAY, EUTH REQ, DISPO REQ, FOSTER           |
| IntakeSubtype    | object    | 22            | 3,033          | OTC, OTC OWNED, FIELD, MEDVET, FOUND        |
| IntakeReason     | object    | 27            | 14,885         | IP ADOPT, ALLERGIC, AGG PEOPLE              |
| OutcomeDate      | object    | 315           | 803            | 10/15/2024, 8/28/2024, 9/30/2024            |

---

## Section 3: Columns – Definitions

**Animal ID**  
Unique identifier for each animal  

**Animal Name**  
Known or assigned name of the animal  

**Animal Type**  
Species of the animal (e.g., DOG, CAT, RABBIT)  
- DOG: Domestic dog  
- CAT: Domestic cat  
- OTHER: Unspecified or uncategorized animal  
- BIRD: Avian species (e.g., pigeon, parrot)  
- LIVESTOCK: Farm animals such as goats or chickens  

**Primary Color**  
Main coat or body color  
- BLACK, WHITE, BROWN, GRAY, ORANGE  
- CALICO-TRI, TRICOLOR, TORTIE-BRN, BRINDLE, MERLE  

**Secondary Color**  
Secondary or accent color  
- RED, BLACK, ORANGE, WHITE, TAN, GOLD, GRAY, CREAM  

**Primary Breed**  
Recorded breed of the animal (e.g., LABRADOR RETR, DOMESTIC SH)  

**Sex**  
Sex and sterilization status (e.g., MALE, FEMALE, SPAYED, NEUTERED)  
- MALE: Intact male  
- FEMALE: Intact female  
- NEUTERED: Sterilized male  
- SPAYED: Sterilized female  
- UNKNOWN: Undetermined or not recorded  

**DOB**  
Date of birth of the animal  

**Age**  
Reported age at intake (e.g., 16 YEARS, NO AGE)  

**Intake Date**  
Date the animal was brought into the shelter  

**Intake Condition**  
Health or behavioral state at intake (e.g., HEALTHY, MED R, DEAD)  
- HEALTHY: No known medical issues  
- MED R: Recovering medical condition  
- MED SEV: Severe medical condition  
- DEAD: Found deceased at intake  
- BEH M: Moderate behavioral issue  
- BEH R: Resolved behavior issue  
- BEH U: Unresolved behavior  
- FERAL: Unsocialized, not suitable for handling  
- AGGRESSIVE: Displaying aggression  
- MED EMERG: Emergency-level condition  

**Intake Type**  
Type of intake event (e.g., STRAY, OWNER SUR, DISPO REQ, EUTH REQ)  
- STRAY: Found loose or wandering  
- OWNER SUR: Voluntarily surrendered by owner  
- EUTH REQ: Euthanasia requested by owner  
- DISPO REQ: Disposition requested (e.g., drop-off)  
- TRANSFER: From another shelter or jurisdiction  
- CONFISCATE: Taken by animal control/legal case  
- RETURN: Returned post-adoption  
- FOSTER: Returned from foster placement  
- WILDLIFE: Native wild animal  
- S/N CLINIC: Intake related to spay/neuter program  

**Intake Subtype**  
Specific method or agency source of intake (e.g., OTC, FIELD, MEDVET)  
- OTC: Over-the-counter walk-in  
- OTC OWNED: Walk-in for a known owned pet  
- FIELD: Collected by field services  
- MEDVET: Brought from medical vet  
- FOUND: Found by member of public  
- POLICE: Transferred by law enforcement  
- HSSV: Humane Society of Silicon Valley transfer  
- EVICTION: Seized following eviction of owner  

**Intake Reason**  
Stated reason for intake (e.g., ALLERGIC, AGG ANIMAL, HOUSING)  
- IP ADOPT: Pre-adoption intake  
- ALLERGIC: Owner reported allergies  
- AGG PEOPLE: Aggressive toward people  
- AGG ANIMAL: Aggressive toward other animals  
- HOUSING: Owner unable to secure animal housing  
- TOO MANY: Owner has too many animals  
- FINANCIAL: Unable to afford pet  
- MOVING: Relocation-related surrender  

**Outcome Date**  
Date of final outcome (e.g., adoption, euthanasia, transfer)  

**Outcome Type**  
Type of outcome (ADOPTION, RTO, EUTH, etc.)  
- ADOPTION: Animal adopted into a new home  
- RTO: Returned to owner  
- EUTH: Euthanized by shelter decision  
- DISPOSAL: Animal was deceased, body disposed  
- TRANSFER: Transferred to another organization  
- FOSTER: Moved to foster care  
- REQ EUTH: Owner-requested euthanasia  
- DIED: Natural death while in care  
- SPAY / NEUTER: Surgical procedure with release  
- MISSING: No outcome found; record mismatch  
- LOST EXP: Lost animal, hold expired  
- FOUND ANIM: Previously lost animal found  
- RTF: Return-to-field, commonly for feral cats  

**Outcome Subtype**  
Additional information related to outcome type  

**Outcome Condition**  
Status of the animal at the time of outcome (e.g., HEALTHY, DEAD)  
- HEALTHY: No observed health/behavioral issues  
- MED M: Moderate health issue  
- MED SEV: Severe condition  
- MED EMERG: Emergency condition  
- MED R: Recovering from condition  
- DEAD: Animal deceased  
- FERAL: Not socialized  
- BEH M: Behavioral issue (moderate)  
- BEH R: Resolved behavioral issue  
- BEH U: Unresolved behavior  

**Jurisdiction**  
Local jurisdiction (e.g., SAN JOSE, MILPITAS)  

**Crossing**  
Location (street or area) where animal was found  

**Latitude / Longitude**  
Geolocation of pickup or shelter activity  

**intake_is_dead**  
TRUE if animal was dead upon arrival  

**outcome_is_dead**  
TRUE if animal was dead at the time of outcome  

**was_outcome_alive**  
1 if animal survived; 0 if not  
- 1: Animal was alive at outcome (e.g., adopted, returned)  
- 0: Animal did not survive the shelter process  

**geopoint**  
Combined latitude/longitude format  

---

## Section 4: Known Data Quality Issues

- Some Outcome Subtype and Outcome Condition values are missing or coded inconsistently.  
- Location (Crossing) may include ambiguous or multi-format entries.  
- DOB values may be absent or estimated in some cases.  

---

## Section 5: Ethical Considerations

- The dataset includes sensitive information regarding animal death and euthanasia.  
- Any public use should remove potentially identifiable location information.  
- Interpretations should avoid drawing conclusions about staff performance without context.  
