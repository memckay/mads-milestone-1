# Project Structure

The folders below contain key information for the project

## `/`

On the top-level folder, you will find the following files:

### [`.gitignore`](../.gitignore)

The `.gitignore` is used to determine what local files should not be committed into the repo. We are using a standard python gitignore.

### [`requirements.txt`](../requirements.txt)

The `requirements.txt` file defines the python packages and versions that we are using. It helps ensure we are all using the same packages and versions at all times. 

**Usage:** 

``` bash
# from the top of the repo, run:

# first create a virtual environment
pip venv .venv

# activate the virtual environment
source .venv/bin/activate

# install requirements
pip install -r requirements.txt
```

### [`README.md`](../README.md)

This file contains the README for the project.

### [`LICENSE`](../LICENSE)

This file contains the License, Terms, and Agreements for all using this project. We are using the MIT license.

## `/docs/`

This folder contains the documentation for this project.

## `/data-assets/`

This folder contains our data assets. It contains the following sub-folders:

### `/_raw/`

This folder contains raw data assets that we sourced for this project.

The links below show where we obtained these from:
* [`Dallas`](https://www.dallasopendata.com/Services/Dallas-Animal-Shelter-Data-Fiscal-Year-2023-2025/uyte-zi7f/about_data)

* [`San Jose`](https://data.sanjoseca.gov/dataset/animal-shelter-intake-and-outcomes/resource/f3354a37-7e03-41f8-a94d-3f720389a68a)

* [`Sonoma County (SoCo)`](https://data.sonomacounty.ca.gov/Government/Animal-Shelter-Intake-and-Outcome/924a-vesw/about_data)

### `/bronze/`

This folder contains the bronze data assets. These are parquet files containing the raw data from the source. Date columns are explicitely marked as dates to simplify downstream processing.


## `/notebooks/`

This folder will contain Data Cleansing notebooks, EDA notebooks, Correlation Analysis notebooks, Time series notebooks, and data visualization notebooks.

### `/elt/`

This folder contains the following Notebooks, used for our Extract, Transform, Load (ELT) process.

* [`1_bronze.ipynb`](../notebooks/elt/1_bronze.ipynb)
* [`2_silver.ipynb`](../notebooks/elt/2_silver.ipynb)

...

## `/reports/`

We will have the WIP report (observations in the analysis)
Milestone Project proposal
Milestone 1 draft report 

## `/visualizations/`

...