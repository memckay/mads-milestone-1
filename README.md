# MADS Milestone 1 Group Project
Welcome to our the **MADS Milestone 1 project**! 

This repository is structured around the Medallion Architecture as inspiration. We organize our work into Bronze (raw ingestion), Silver (data cleaning & enrichment), and Gold (analysis-ready summaries) layers. We apply this framework to animal shelter intake and outcome data from Dallas, San Jose, and Sonoma County.

## Research Question

**How do shelter intake characteristics (breed, age, intake condition) relate to outcome rates (adoption, transfer, euthanasia)?**  
- Which factors most strongly predict adoption success?  
- Are there seasonal or regional patterns in intake volume and outcomes?  
- How does length-of-stay vary by breed, age cohort, or intake condition?

# Docs

Below you can find the available documentation for this project:

* [Project Structure](./docs/project_structure.md): The high-level structure of the project.
* Metadata
    * [Merging DFs Planning](./docs/metadata/merging_dfs_plan.md): How we planned to merge different Dataframes together.
    * [Dallas Animal Shelter](./docs/metadata/dallas_animal_shelter_metadata.md): Background information for the Dallas Dataset.
    * [San Jose Animal Shelter](./docs/metadata/san_jose_animal_shelter_metadata.md): Background information for the San Jose Dataset.
    * [Sonoma County (SoCO) Animal Shelter](./docs/metadata/sonoma_county_animal_shelter_metadata.md): Background information for the Sonoma County (SoCo) Dataset.
