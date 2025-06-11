# Project Structure

The folders below contain key information for the project.


On the top-level folder, you will find the following file:

### [`.gitignore`](../../.gitignore)

The `.gitignore` is used to determine what local files should not be committed into the repo. We are using a standard python gitignore.


### [`README.md`](../../README.md)

This file contains the README for the project.

### [`LICENSE`](../../LICENSE)

This file contains the License, Terms, and Agreements for all using this project. We are using the MIT license.

## [`docs`](../../docs/project_structure.md)

This folder contains the documentation for this project.

---

## `src/`

This folder contains all of our source code files:

This folder contains the following Notebooks, used for our Extract, Transform, Load (ELT) process.

* [`1_bronze.ipynb`](../../src/1_bronze.ipynb)
* [`2_silver.ipynb`](../../src/2_silver.ipynb)
* [`3_gold.ipynb`](../../src/3_gold.ipynb)


<div>

```mermaid
flowchart LR
    A([Bronze])
    %% Bronze styling - brown/bronze color
    style A fill:#cd7f32,stroke:#8b4513,stroke-width:3px,color:#fff
    B([Silver])
    %% Silver styling - silver/gray color
    style B fill:#c0c0c0,stroke:#708090,stroke-width:3px,color:#000
    C([Gold])
    %% Gold styling - gold/yellow color
    style C fill:#ffd700,stroke:#b8860b,stroke-width:3px,color:#000

    A --> B
    B --> C
```
<div>

It also contains the following file for tracking project dependencies.

* [`requirements.txt`](../requirements.txt)

    The `requirements.txt` file defines the python packages and versions that we are using. It helps ensure we are all using the same packages and versions at all times. 

    **Usage:** 

    ``` bash
    pip install -r requirements.txt
    ```

### `data/`

This folder contains all of our data assets. Some of the raw files are provided as samples only.

#### `_raw/`

This folder contains raw data assets that we sourced for this project.

The links below show where we obtained these from:
* [`Dallas`](https://www.dallasopendata.com/Services/Dallas-Animal-Shelter-Data-Fiscal-Year-2023-2025/uyte-zi7f/about_data)

* [`San Jose`](https://data.sanjoseca.gov/dataset/animal-shelter-intake-and-outcomes/resource/f3354a37-7e03-41f8-a94d-3f720389a68a)

* [`Sonoma County (SoCo)`](https://data.sonomacounty.ca.gov/Government/Animal-Shelter-Intake-and-Outcome/924a-vesw/about_data)

#### [`bronze/`](./data/bronze/dallas_df.parquet)

This folder contains the bronze data assets. These are parquet files containing the raw data from the source. Date columns are explicitely marked as dates to simplify downstream processing.


#### [`silver/`](./data/silver/silver.parquet)

This folder contains the silver data asset. This is a parquet file which contains cleaned and transformed data from bronze. 

#### [`gold/`](./data/gold/gold.parquet)

This folder contains the gols data assets. This is a parquet file which contains transformed data from silver. 

---