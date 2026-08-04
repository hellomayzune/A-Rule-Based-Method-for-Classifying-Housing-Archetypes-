<p align="left">
• <a href="https://github.com/hellomayzune"><strong>GitHub</strong></a> •
<a href="https://orcid.org/0000-0003-0282-2633"><strong>ORCID</strong></a> •
<a href="https://scholar.google.com/citations?user=LmP8B_4AAAAJ&hl=en"><strong>Google Scholar</strong></a> •
<a href="https://www.researchgate.net/profile/May-Zune"><strong>ResearchGate</strong></a> •
<a href="https://www.linkedin.com/in/mayzune//"><strong>Linkedin</strong></a> •
</p>

# 🏠📊 A Rule-Based Method for Classifying Housing Archetypes 

This work offers a fast, transparent, cross-dataset way to bucket large numbers of dwellings into a consistent set of housing archetypes using simple, interpretable rules — useful for exploratory analysis and downstream applications, but acknowledged by the authors as needing further statistical validation before being treated as authoritative. Specifically, it offers:

- a scalable classification pipeline
- a transparent, auditable logic
- a bridge between two different data sources (EPC and Verisk)
- a foundation for downstream analysis
- a first-pass triage tool

📬 Contact: If you have any questions, suggestions, or would like to discuss this work, please open an issue or contact from the links above.

📖 This *README* describes the following contents.

- [Project information](#-project-information)
    - [Methodological information and source database](#-methodological-information-and-source-database)
    - [Database information](#️-database-information)
- [Methods](#️-methods)
    - [Archetype classification scheme](#-archetype-classification-scheme)
    - [Thresholds](#-thresholds)
    - [Data differences](#-data-differences)
    - [Share methods](#-share-methods)
    - [Distinct methods](#️-distinct-methods)
    - [Limitations](#️-limitations)
- [Example Python codes](#-example-python-codes)


# 📌 Project information
-   *Project Title*: Regional Retrofit, Net-Zero Aspirations, and their Whole Life Carbon Burden
- *Notebook Author*: May Zune
- *Funder*: This research was financially supported by Research England through the South Yorkshire Sustainability Centre. DDT and HA also acknowledge support from EPSRC through the BuildZero research program (EP/Y530578/1)
- *Project website*: [South Yorkshire Sustainability Centre](https://www.sysustainabilitycentre.org)


## 📚 Methodological information and source database

This work is currently under peer review. The citation and publication details will be updated once the manuscript is published. In the meantime, methodological information is available in:

> Zune, M., Arbabi, H., Densley Tingley, D. (November 26, 2025). Regional Retrofit, Net-Zero Aspirations, and their Whole Life Carbon Burden. Available at SSRN: https://ssrn.com/abstract=5909647. doi: [10.2139/ssrn.5909647](http://dx.doi.org/10.2139/ssrn.5909647)

The source database of this work can be found in:

> Get Energy Performance of Buildings Data 2026 [cited 2026 May 14]. Available from: [GOV.UK.](https://get-energy-performance-data.communities.gov.uk)

>3D Visual Intelligence: UKBuildings, Verisk. 2024 [cited 2024 November 1]. Available from:  [Verisk](https://www.verisk.com/en-gb/3d-visual-intelligence/products/ukbuildings/)


## 🗂️ Database information
- Source Data: EPC and Verisk
- Format of database: *.csv*, *.xlsx* and *.ipynb*
- Language: English
- Required data space: Less than 150 MB
- README file date created: 14 May 2026.
- README file date modified: To update 
- Programming language: The code is written in `Python` using `Pandas` version 2.2.3.
- License: *MIT open source*

[Back To The Top](#-project-information)

---

# ⚙️ Methods
## 🏠 Archetype classification scheme

| Code | Description |
|------|-------------|
| **SD-V** | Large and complex footprint semi-detached house (e.g., Victorian design style) |
| **SD-R** | Small and rectangular footprint semi-detached house |
| **SD-S** | Small and complex footprint semi-detached house |
| **B-SD** | Small rectangular or complex footprint semi-detached bungalow |
| **B-DT** | Large and complex footprint detached bungalow |
| **DT-V** | Large and complex footprint detached house (e.g., Victorian design style) |
| **DT-R** | Small and rectangular footprint detached house |
| **DT-L** | Large and complex footprint detached house (e.g., fewer than two storeys) |
| **T-GM** | Large and complex footprint mid-terrace (e.g., Georgian design style) |
| **T-GE** | Large and complex footprint end-terrace (e.g., Georgian design style) |
| **T-VM** | Small and complex footprint mid-terrace (e.g., Victorian design style) |
| **T-VE** | Small and complex footprint end-terrace (e.g., Victorian design style) |
| **T-RM** | Small and rectangular footprint mid-terrace |
| **T-RE** | Small and rectangular footprint end-terrace |


## 🎯 Thresholds

| Code | Threshold |
|------|-----------|
| SD-R | Area ≤ **100 m²** |
| SD-S | **100 m²** < Area < **150 m²** |
| SD-V | Area ≥ **150 m²** |
| TR-E, TR-M | Area ≤ **110 m²** |
| TV-E, TV-M | **110 m²** < Area < **200 m²** |
| TG-E, TG-M | Area ≥ **200 m²** |

[Back To The Top](#-project-information)

## 🔍 Data differences
- File name: **EPC_SouthYorkshire_Clean_202604.csv** 
    - This file is created from the EPC database for South Yorkshire. The shape of the original database is *528925, 94*
    - Data fields used in the *SY_domestic_EPC_Archetypes_ERIS.ipynb*
        - certificate_number (to link with original EPC database)
        - property_type
        - built_form
        - construction_age_band
        - floor_height
        - flat_storey_count
        - total_floor_area

- File name: **Verisk_SouthYorkshire_Correct_premise_floor_count.csv** 
    - This file is exported from the Verisk database for South Yorkshire. The shape of the original database is *614589, 32*
    - Data fields used in the *SY_domestic_Verisk_Archetype_ERIS.ipynb*
        - fid (to link with original GIS database)
        - id (to link with original GIS database)
        - premise_type
        - premise_age 
        - height
        - premise_floor_count
        - premise_area 
        - building_area 
        - gross_area 


[Back To The Top](#-project-information)

## 🚀 Share methods
- **Tools**: pandas, numpy, matplotlib/seaborn imported identically; sns.barplot used to visualize archetype counts at the end.
- **Workflow**: load CSV → inspect unique values/counts of key categorical fields → split into sub-dataframes by dwelling type → apply np.where/np.select with floor-area thresholds → recombine with pd.concat → tabulate final archetype counts → write a "Limitations" markdown section critiquing the same rule-based approach.
- **Bungalow logic**: np.where(... == 'Detached', 'B-DT', 'B-SD').
- **Identical threshold logic and cutoffs**: For Detached (≤150 vs >150), Semi-Detached (≤100 / 100–150 / ≥150), End-Terrace and Mid-Terrace (≤110 / 110–200 / ≥200) — same breakpoints, same np.select pattern, same archetype code naming (DT-R, DT-L or DT-V, SD-R/S/V, TR/TV/TG + -E/-M).
- **Limitation**: Added the limitation section calling out fixed/unvalidated thresholds, hard boundaries, inconsistent inequality operators, and single-variable proxies for archetype.

[Back To The Top](#-project-information)

## ⚖️ Distinct methods

| Aspect | EPC notebook | Verisk notebook |
|--------|--------------|-----------------|
| **Source file** | `EPC_SouthYorkshire_Clean_202604.csv` | `Verisk_SouthYorkshire_Correct_premise_floor_count.csv` |
| **Key columns used** | `property_type`, `built_form`, `total_floor_area`, `construction_age_band`, `floor_height`, `flat_storey_count` | `premise_type`, `premise_floor_count`, `gross_area` *(no age or height fields used)* |
| **Bungalow identification** | Filtered by `property_type == "Bungalow"` *(explicit category)* | Filtered by `premise_floor_count == 1` *(inferred from storey count, as Verisk has no explicit bungalow type)* |
| **House/storey filtering** | No storey-count filter applied to houses | Additional filter: only houses with `1 < premise_floor_count < 4` are classified as Detached, Semi-Detached, or Terrace types |
| **Data cleaning** | Minimal—mainly column subsetting | Excludes *Domestic outbuilding*, *Flat*, and *Maisonette* records, renames *Enclosed end/mid-terrace* to *End/Mid-terrace*, and manually corrects malformed floor-count values (e.g., `"3,5"` → integer) |
| **Extra archetype category** | Five dwelling groups: **Bungalow, Detached, Semi-Detached, End-Terrace, Mid-Terrace** | Adds a sixth group: **Terrace** (`TR`, `TV`, `TG`), which is not present in the EPC workflow |
| **Imports** | Standard libraries only | Also imports `Decimal` and `ROUND_HALF_UP` from the `decimal` module *(not clearly used in the classification logic)* |
| **Limitations** | Highlights unused EPC fields (`construction_age_band`, `floor_height`, and `flat_storey_count` for `DT-L`/`DT-V` separation) and excludes flats/maisonettes without reporting counts | Highlights manual floor-count corrections, unclassified high-rise properties (7–15, 18, and 32 storeys labelled `Not_Bungalow` without further classification), and excluded domestic outbuildings |

[Back To The Top](#-project-information)

## ⚠️ Limitations

- This study classifies buildings using fixed gross floor area thresholds combined with premise type and floor count, offering a reproducible way to categorise large property datasets—but with notable limitations. 
- The thresholds (e.g. 150 m² for detached, 100–150 m² for semi-detached) are heuristic rather than statistically derived or validated, so classification accuracy is unquantified and borderline properties may be misclassified. 
- Bungalows are treated inconsistently: classified by floor count and premise type alone, without area, unlike other archetypes that rely primarily on area. Properties with seven or more storeys remain uncategorised. 
- Floor count data also required manual, expert-judgement corrections lacking a documented protocol, potentially affecting bungalow/house assignment, while domestic outbuildings were excluded entirely, limiting coverage of the building stock. 
- The method further relies on only two variables—floor area and premise type—ignoring other factors shaping true archetype, such as footprint shape, roof design, bedroom count, construction age, and later extensions. 
- Thresholds are applied uniformly with no regional adjustment, and area data reflect a single point in time. Properties failing to meet any archetype's conditions default to "Unknown," a group whose size and causes remain unexamined. 
- Overall, the method is a useful first-pass tool, but results should be seen as indicative, with further validation against verified property types recommended.

[Back To The Top](#-project-information)

# 🔧 Example Python codes

- File name: **SY_domestic_EPC_Archetypes_ERIS.ipynb** 
- Import file: **EPC_SouthYorkshire_Clean_202604.csv** 

- Example coldes for Bungalow
```js
// Dataframe for Bungalow Only
dfb = dfALL[(dfALL.property_type == "Bungalow")]
// Define archetype codes
dfb['Archetype'] = np.where(dfb['built_form'] == 'Detached', 'B-DT', 'B-SD')
```

- Example coldes for Detached Houses
```js
// Dataframe for House Only
df = dfALL[(dfALL.property_type == "House")]
// Select "Detached" under Houses
dfd = df[(df.built_form == "Detached")]
// Define code
cond_DT = [dfd['total_floor_area'] <= 150, dfd['total_floor_area'] > 150]
choice_DT = ['DT-R', 'DT-L or DT-V']
dfd['Archetype'] = np.select(cond_DT, choice_DT, default='Unknown')

// We considered DT-L has 1~2 storey, and DT-V has more than 2 storey.
// Get to know storey count
flat_storey_count_list = dfd['flat_storey_count'].unique()
print("\nflat_storey_count with index numbers:")
for i, N_flat_storey_count in enumerate(flat_storey_count_list):
    count_FSC = len(dfd[dfd['flat_storey_count'] == N_flat_storey_count ])
    print(f"{i}: {N_flat_storey_count} ({count_FSC} records)")
```

- Example coldes for Semi-detached Houses

```js
// Select "Semi-Detached" under Houses
dfs = df[(df.built_form == "Semi-Detached")]
cond_SD = [
    dfs['total_floor_area'] <= 100,
    (dfs['total_floor_area'] > 100) & (dfs['total_floor_area'] < 150),
    dfs['total_floor_area'] >= 150
]
choice_SD = ['SD-R', 'SD-S', 'SD-V']
dfs['Archetype'] = np.select(cond_SD, choice_SD, default='Unknown')
```

- Example coldes for Terrace Houses

```js
// Select "End-Terrace" under Houses
dfe = df[(df.built_form == "End-Terrace")]
cond_TE = [
    dfe['total_floor_area'] <= 110,
    (dfe['total_floor_area'] > 110) & (dfe['total_floor_area'] < 200),
    dfe['total_floor_area'] >= 200
]
choice_TE = ['TR-E', 'TV-E', 'TG-E']
dfe['Archetype'] = np.select(cond_TE, choice_TE, default='Unknown')
```

- Example coldes for Terrace Houses

```js
// Select "Mid-Terrace" under Houses
dfm = df[(df.built_form == "Mid-Terrace")]
cond_TM = [
    dfm['total_floor_area'] <= 110,
    (dfm['total_floor_area'] > 110) & (dfm['total_floor_area'] < 200),
    dfm['total_floor_area'] >= 200
]
choice_TM = ['TR-M', 'TV-M', 'TG-M']
dfm['Archetype'] = np.select(cond_TM, choice_TM, default='Unknown')
```
[Back To The Top](#-project-information)
