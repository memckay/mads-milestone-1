# Milestone 1 Meta-Data Document

---

## Section 1: Dataset Description and Summary

**Dataset Name:** Animal Shelter Intakes and Outcomes  
**Source:** Long Beach Animal Shelter (Outcome 2024)  
**File Name:** animal-shelter-intakes-and-outcomes.csv  
**Total Records:** 3,822  
**Total Columns:** 23  
**Date Range:** Outcome date cutoff (31-12-2024) used year 2024 as anchor instead of Intake Date.  

**Description:**  
This dataset captures detailed information about animals taken in and released by a municipal shelter. It includes characteristics of animals, geographic intake data, intake and outcome types, health conditions, and derived fields indicating life status outcomes. The data is intended for operational analysis, outcome forecasting, and program improvement, including survival analysis, seasonal trend evaluation, and geographic targeting.

**Data Completeness:**  
- Some fields such as Animal Name and DOB are partially missing.  
- The Reason for Intake field is missing in over 90% of cases and may not be reliable.  

---

## Section 2: Columns – Unique Values and Characteristics

| Column Name                   | Data Type    | Unique Values | Missing Values | Sample Values                               |
|-------------------------------|--------------|---------------|----------------|---------------------------------------------|
| Animal ID                     | String       | 3,710         | 0              | A711162, A728317                            |
| Animal Name                   | String       | 2,198         | 1,126          | ZOEY, MITZY, HIGHTOWER                      |
| Animal Type                   | String       | 8             | 0              | DOG, CAT, BIRD, RABBIT                      |
| Primary Color                 | String       | 58            | 0              | BLACK, BR BRINDLE, CALICO                   |
| Secondary Color               | String       | 27            | 2,019          | WHITE, GRAY, TAN                            |
| Sex                           | String       | 5             | 0              | SPAYED, NEUTERED, INTACT, UNKNOWN           |
| DOB                           | Date/String  | Many          | 406            | 2018-03-12, 2014-11-20                      |
| Intake Date                   | Date         | Many          | 0              | 2024-01-15, 2024-02-02                      |
| Intake Condition              | String       | Several       | 0              | HEALTHY, INJURED, SICK, AGGRESSIVE          |
| Intake Type                   | String       | 11            | 0              | STRAY, OWNER SUR, TRANSFER, FOSTER          |
| Intake Subtype                | String       | 20+           | 83             | OTC, FIELD, BITE, POLICE, FOUND             |
| Reason for Intake             | String       | Many          | 3,592          | (Sparse values)                             |
| Outcome Date                  | Date         | Many          | 0              | 2024-01-16, 2024-02-03                      |
| Crossing                      | String       | 7,421         | 0              | SENTER RD X TULLY RD, SNELL AVE             |
| Jurisdiction                  | String       | ~10           | 0              | SAN JOSE, MILPITAS                          |
| Outcome Type                  | String       | 10+           | 6              | ADOPTION, RTO, EUTH, TRANSFER               |
| Outcome Subtype               | String       | Many          | 325            | FOSTER, REQ EUTH, OTC                       |
| Latitude                      | Float        | Many          | 0              | 37.297, 37.322                              |
| Longitude                     | Float        | Many          | 0              | -121.844, -121.901                          |
| intake_is_dead                | Bool-like    | 2             | 0              | TRUE, FALSE                                 |
| outcome_is_dead               | Boolean      | 2             | 0              | TRUE, FALSE                                 |
| was_outcome_alive             | Integer      | 2             | 0              | 1, 0                                        |
| geopoint                      | String       | Many          | 0              | 37.301,-121.842                             |

---

## Section 3: Columns – Definitions

**Animal ID**  
Unique shelter-assigned ID for each animal  

**Animal Name**  
Given or known name of the animal  

**Animal Type**  
Type/species of the animal (e.g., DOG, CAT, etc.)  
- DOG: Domestic dog  
- CAT: Domestic cat  
- RABBIT: Domestic rabbit  
- BIRD: Parrot, pigeon, or other bird  
- GUINEA PIG: Small rodent  
- REPTILE: Snake, lizard, etc.  
- OTHER: Non-categorized species  

**Primary/Secondary Color**  
Observed coat or feather colors; secondary is optional  
- BLACK, WHITE, GRAY, BROWN, CALICO: Common coat colors  
- BR BRINDLE: Brown brindle pattern (streaked)  
- TORTIE: Tortoiseshell (mottled orange/black)  
- MERLE: Marbled pattern (dogs)  

**Sex**  
Biological sex and spay/neuter status  
- SPAYED: Female sterilized  
- NEUTERED: Male sterilized  
- INTACT: Not sterilized  
- UNKNOWN: Undetermined  

**DOB**  
Date of birth, if known  

**Intake Date**  
Date animal entered the shelter  

**Intake Condition**  
Physical or behavioral state at intake (e.g., HEALTHY, AGGRESSIVE)  
- HEALTHY: No apparent health or behavioral issues  
- INJURED: Obvious physical injury at intake  
- SICK: Showing signs of illness  
- AGGRESSIVE: Displays aggressive behavior  
- BEHAVIORAL: Not medically sick but showing behavioral issues  
- DEAD: Animal found deceased  

**Intake Type**  
How the animal entered the shelter (e.g., STRAY, TRANSFER, OWNER SUR)  
- STRAY: Found without owner  
- OWNER SUR: Owner surrendered  
- TRANSFER: From another shelter  
- FOSTER: From foster care  
- WILDLIFE: Wild animal  
- CONFISCATE: Legal/cruelty case  
- RETURN: Returned after adoption  
- DISPO REQ: Disposition requested  
- EUTH REQ: Euthanasia requested  
- S/N CLINIC: Spay/neuter clinic intake  

**Intake Subtype**  
Additional classification of intake (e.g., OTC = Over the Counter)  
- OTC: Over-the-counter walk-in  
- FIELD: Collected in field  
- BITE: Bite case  
- POLICE: Brought by law enforcement  
- FOUND: Public hand-in  

**Reason for Intake**  
Free-text or coded reason for surrender/intake (often missing)  

**Outcome Date**  
Date of release, transfer, adoption, or death  

**Crossing**  
Street/intersection where animal was found  

**Jurisdiction**  
City or county of record  

**Outcome Type**  
Final disposition (ADOPTION, EUTHANASIA, TRANSFER, etc.)  
- ADOPTION: Adopted out  
- RTO: Returned to owner  
- EUTH: Euthanized  
- TRANSFER: Sent to partner agency  
- DISPOSAL: Deceased body handled  
- FOSTER: Placed in foster care  
- DIED: Natural death  
- REQ EUTH: Owner-requested euthanasia  
- MISSING: Record mismatch  

**Outcome Subtype**  
Further detail on outcome (e.g., RTO, REQ EUTH, FOSTER)  
- HEALTHY: No known issues  
- MED M: Moderate health issue  
- MED SEV: Severe health condition  
- MED EMERG: Emergency health status  
- MED R: Recovering  
- BEH M: Moderate behavioral problem  
- BEH R: Resolved behavior issue  
- BEH U: Unresolved behavior  
- DEAD: Deceased  
- FERAL: Unsocialized  

**Latitude / Longitude**  
Geolocation of the intake or pickup point  

**intake_is_dead**  
Whether the animal was found dead at intake  
- TRUE: Animal deceased at intake  
- FALSE: Animal alive at intake  

**outcome_is_dead**  
Whether the animal died before or at outcome  
- TRUE: Animal deceased at outcome  
- FALSE: Animal alive at outcome  

**was_outcome_alive**  
1: Animal survived the shelter process  
0: Animal did not survive  

**geopoint**  
Combined lat/lon string format  

---

## Section 5: Known Data Quality Issues

- Reason for Intake is missing in ~94% of records.  
- Animal Name is unknown for ~30% of entries; IDs should be used for identification.  
- DOB missing in 11% of entries.  

---

## Section 6: Ethical Considerations

- This dataset includes sensitive information about animal mortality.  
- Public use should avoid identifiers or locations that could compromise individual privacy (e.g., address-level geodata).  
- Consider ethical framing when reporting on euthanasia outcomes or death trends.  