# Austin, San Jose, and SoCo Column Mapping Plan

This table outlines how fields from the **San Jose**, **Dallas**, and **SoCo** animal services datasets map to a unified **standardized schema**.  
If a value is missing in a dataset, it's marked with a dash (`-`).  
> Notes are included when special handling is needed.

| San Jose                   | Dallas                | SoCo             | Standardized Name                                      |
|----------------------------|------------------------|------------------|--------------------------------------------------------|
| AnimalID (Ex: A0075579)    | Animal_Id (Ex: A6001010) | Animal ID       | `animal_id` — handle potential duplicate IDs across datasets by generating a new `animal_pk` as the primary key and keeping `animal_id` as a logical key |
| AnimalType                 | Animal_Type           | Type             | `animal_type` — some regions include wildlife (not just cats and dogs); ensure downstream logic accounts for this variation |
| PrimaryBreed               | Animal_Breed          | Breed            | `breed`                                                |
| PrimaryColor               | -                     | Color            | `primary_color`                                        |
| Age                        | -                     | -                | `age`                                                  |
| -                          | -                     | Date Of Birth    | `date_of_birth`                                        |
| Sex                        | -                     | Sex              | `sex`                                                  |
| IntakeType                 | Intake_type           | Intake Type      | `intake_type`                                          |
| IntakeCondition            | Intake_Condition      | Intake Condition | `intake_condition`                                     |
| IntakeReason               | Reason                | -                | `intake_reason`                                        |
| IntakeDate                 | Intake_Date           | Intake Date      | `intake_date`                                          |
| OutcomeType                | Outcome_Type           | Outcome Type     | `outcome_type`                                         |
| OutcomeDate                | Outcome_Date           | Outcome Date     | `outcome_date`                                         |

These columns represent the **primary fields of interest** that we will prioritize in our analysis.

Although the three regions provide overlapping data, the column names vary across datasets. To support consistent querying and modeling, we are defining a **standardized naming convention** to be used in the **Silver Layer** of our data pipeline.

Once standardized, we will attempt to **consolidate** values across regions. For critical categorical variables such as `age`, `primary_color`, and `sex`, we will also evaluate whether **imputation** is necessary to ensure data completeness for downstream analysis.