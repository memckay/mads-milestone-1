# MADS Milestone 1 Group Project
Welcome to our the **MADS Milestone 1 project**! 

This repository is structured around the Medallion Architecture as inspiration. We organize our work into Bronze (raw ingestion), Silver (data cleaning & enrichment), and Gold (analysis-ready summaries) layers. We apply this framework to animal shelter intake and outcome data from Dallas, San Jose, and Sonoma County.

## Research Question

**How do shelter intake characteristics (breed, age, intake condition) relate to outcome rates (adoption, transfer, euthanasia)?**  
- Which factors most strongly predict adoption success?  
- Are there seasonal or regional patterns in intake volume and outcomes?  
- How does length-of-stay vary by breed, age cohort, or intake condition?

# Local Setup

To get started, you can run the commands below to setup a Virtual Environment using the conda python package manager.

If needed, install conda below:

``` bash
# Install miniconda using homebrew (light version of conda)
brew install miniconda
# Initialize conda on your shell
conda init zsh # replace 'zsh' with your shell (bash, zsh, ...)

# Change the base python to use 3.12, as 3.13 has compatibility issues with common libraries
conda install python=3.12 -n base
# Activate the base python (3.12)
conda activate base
```

Then, you can run:

``` bash
pip install -r requirements.txt
```

This will install the `ipykernel` so that your local environment works properly. Any other virtual environment tooling can be used, if prefered. This also installs `ruff` for linting, `pre-commit` to enforce linting, and other packages for the notebooks.

Make sure your IDE/Notebook is using the conda base python's kernel.


# Docs

Below you can find the available documentation for this project:

* [Project Structure](./docs/project_structure.md): The high-level structure of the project.
* Metadata
    * [Merging DFs Planning](./docs/metadata/merging_dfs_plan.md): How we planned to merge different Dataframes together.
    * [Dallas Animal Shelter](./docs/metadata/dallas_animal_shelter_metadata.md): Background information for the Dallas Dataset.
    * [San Jose Animal Shelter](./docs/metadata/san_jose_animal_shelter_metadata.md): Background information for the San Jose Dataset.
    * [Sonoma County (SoCO) Animal Shelter](./docs/metadata/sonoma_county_animal_shelter_metadata.md): Background information for the Sonoma County (SoCo) Dataset.

---