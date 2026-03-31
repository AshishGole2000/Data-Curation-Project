# Hyperspectral Leaf Reflectance of Grasses: Dataset Documentation

## Dataset Overview

**Title:** Data from: Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site

**Authors:** Stephanie Pau, Rachel Slapikas, Ching Ling Ho, Samantha L. J. Bayliss, Ryan C. Donnelly, Abubakarr Abdullahi, Brent R. Helliker, Jesse B. Nippert, William J. Riley, Christopher J. Still, Emily R. Wedel, Daniel M. Griffith

**Funding:** This work was supported by the U.S. National Science Foundation (NSF award identifiers associated with this research are documented in the related publication)

**Related Publication:** Pau, S., Slapikas, R., Ho, C. L., Bayliss, S. L. J., Donnelly, R. C., Abdullahi, A., Helliker, B. R., Nippert, J. B., Riley, W. J., Still, C. J., Wedel, E. R., & Griffith, D. M. (2025). Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site. *Ecosphere*, 16(3), e70257. https://doi.org/10.1002/ecs2.70257

**DOI:** 10.5061/dryad.gf1vhhn0n

**Last Updated:** [Date of deposit]

---

## Purpose and Research Context

This dataset contains hyperspectral reflectance measurements and functional trait data for grass species collected across multiple field sites. The research investigates whether grass leaf spectral signatures vary more by evolutionary lineage (C3 vs. C4 photosynthetic pathways) than by the geographic site where they were collected. Understanding these relationships is important for remote sensing applications, ecological modeling, and predicting plant functional responses to environmental change.

---

## File Inventory

This deposit contains three files:

### 1. **spectra_data.csv** (or equivalent filename)
- **Description:** Hyperspectral reflectance measurements across wavelengths from 400-2400 nm
- **Dimensions:** 426 rows × 2151 columns
- **Row structure:** Each row represents one sample (one individual plant measurement)
- **Column structure:** 
  - Column 1: `sample_id` (unique identifier linking to traits table)
  - Columns 2-2151: Reflectance values at specific wavelengths (column names format: `X###.#` where ### represents wavelength in nanometers)

### 2. **traits_data.csv** (or equivalent filename)
- **Description:** Functional trait measurements and sample metadata
- **Dimensions:** 426 rows × 23 columns
- **Row structure:** Each row represents one sample, corresponding to the same samples in spectra_data.csv
- **Column structure:** See Variable Dictionary section below

### 3. **README.txt** (this file)
- **Description:** Dataset documentation and metadata

---

## Data Collection Methods

### Study Sites
[**CURATOR NOTE:** Information about site locations, coordinates, climate, and vegetation characteristics should be added here. Current deposit lacks explicit site coordinate information.]

Samples were collected from [NUMBER] field sites representing different [environmental gradients, geographic regions, etc.]. Site codes used in the traits table are:
- [Site code 1]: [Location, coordinates, description]
- [Site code 2]: [Location, coordinates, description]
- [Add all site codes]

### Sampling Design
[**CURATOR NOTE:** Authors should clarify the sampling strategy here]
- Number of species sampled: [NUMBER]
- Samples per species per site: [NUMBER OR DESCRIPTION]
- Temporal coverage: [Dates of field collection]
- Sampling method: [Description of how individual plants were selected]

### Measurement Protocols

**Hyperspectral Reflectance:**
[**CURATOR NOTE:** Authors should provide details on:]
- Instrument used: [Make, model, specifications]
- Measurement conditions: [Lab vs. field, illumination source, viewing geometry]
- Number of measurements per sample: [If multiple scans were averaged]
- Quality control procedures: [Dark current correction, white reference calibration, etc.]

**Functional Traits:**
[**CURATOR NOTE:** Authors should describe measurement protocols for each trait, including:]
- Laboratory methods
- Instruments used
- Timing of measurements relative to spectral data collection
- Replication strategy

---

## Variable Dictionary

### Spectra File (spectra_data.csv)

| Variable Name | Description | Units | Data Type | Missing Values |
|---------------|-------------|-------|-----------|----------------|
| sample_id | Unique identifier for each sample; links to traits table | N/A | Text/Identifier | None |
| X400.0 through X2400.0 | Reflectance value at specified wavelength (nm). Column name format: X###.# indicates wavelength. For example, X650.5 is reflectance at 650.5 nm | Proportion (0-1) or Percentage (0-100) [**CURATOR NOTE: Authors should specify**] | Numeric | [Specify meaning if present] |

**Wavelength Coverage:** 
- Range: 400-2400 nm
- Spectral resolution: [**CURATOR NOTE:** Specify nm between measurements]
- Number of spectral bands: 2150

### Traits File (traits_data.csv)

| Variable Name | Description | Units | Data Type | Expected Range | Missing Values |
|---------------|-------------|-------|-----------|----------------|----------------|
| sample_id | Unique identifier linking to spectra file | N/A | Text/Identifier | N/A | None allowed |
| species | Scientific name of grass species | N/A | Text | N/A | None |
| genus | Taxonomic genus | N/A | Text | N/A | None |
| subfamily | Taxonomic subfamily | N/A | Text | N/A | None |
| lineage | Evolutionary lineage classification | N/A | Categorical | [List categories] | None |
| photosynthetic_pathway | Type of photosynthesis | N/A | Categorical | C3, C4 | None |
| site | Site code indicating collection location | N/A | Categorical | [List site codes] | None |
| SLA | Specific Leaf Area | [**CURATOR NOTE: Specify - mm²/mg? cm²/g?**] | Numeric | [Provide expected range] | NA = not measured |
| LDMC | Leaf Dry Matter Content | [**CURATOR NOTE: Specify units - mg/g? %?**] | Numeric | [Provide expected range] | NA = not measured |
| leaf_thickness | Leaf thickness | [**CURATOR NOTE: Specify - mm? μm?**] | Numeric | [Provide expected range] | NA = not measured |
| chlorophyll_content | Chlorophyll concentration | [**CURATOR NOTE: Specify units and method**] | Numeric | [Provide expected range] | NA = not measured |
| nitrogen_content | Leaf nitrogen content | [**CURATOR NOTE: Specify - % dry mass? mg/g?**] | Numeric | [Provide expected range] | NA = not measured |
| carbon_content | Leaf carbon content | [**CURATOR NOTE: Specify - % dry mass?**] | Numeric | [Provide expected range] | NA = not measured |
| [Additional traits] | [Add descriptions for all 23 variables] | [Units] | [Type] | [Range] | [Meaning] |

**Notes on Missing Values:**
- `NA` in trait columns indicates the measurement was not taken for that sample
- [**CURATOR NOTE:** Authors should clarify if missing values also represent failed measurements, values below detection limit, or other reasons]

---

## File Relationships and Usage Instructions

### Linking Files
The two CSV files are linked via the `sample_id` column, which appears in both files:
- **Join type:** One-to-one relationship (each sample_id appears exactly once in each file)
- **Join integrity:** All 426 sample_ids in spectra_data.csv have corresponding records in traits_data.csv

### Example Code for Merging Files (R)

```r
# Load data
spectra <- read.csv("spectra_data.csv")
traits <- read.csv("traits_data.csv")

# Merge files
complete_data <- merge(spectra, traits, by = "sample_id", all = TRUE)

# Verify merge success
nrow(complete_data) == nrow(spectra)  # Should return TRUE
```

### Example Code for Merging Files (Python)

```python
import pandas as pd

# Load data
spectra = pd.read_csv("spectra_data.csv")
traits = pd.read_csv("traits_data.csv")

# Merge files
complete_data = spectra.merge(traits, on='sample_id', how='outer')

# Verify merge success
print(len(complete_data) == len(spectra))  # Should print True
```

---

## Data Processing and Provenance

[**CURATOR NOTE:** This section is critical for reproducibility. Authors should document:]

### Spectral Data Processing
**Raw Data Source:** [Describe original instrument output format]

**Preprocessing Steps Applied:**
1. [Step 1: e.g., "Dark current correction using measurements taken with lens cap on"]
2. [Step 2: e.g., "White reference calibration using Spectralon panel"]
3. [Step 3: e.g., "Smoothing or noise reduction - specify algorithm and parameters"]
4. [Step 4: e.g., "Removal of atmospheric water absorption bands (if applicable)"]
5. [Step 5: e.g., "Normalization or averaging of multiple scans per sample"]

**Software Used:** [Name, version, citation if applicable]

**Quality Control:**
- [Describe any outlier removal criteria]
- [Describe quality flags or acceptance thresholds]

### Trait Data Processing
[**CURATOR NOTE:** Authors should document:]
- Any calculations or transformations applied to raw measurements
- Outlier handling
- How values were averaged if multiple measurements were taken per sample

---

## Data Quality Notes

### Known Issues or Limitations
[**CURATOR NOTE:** Authors should note:]
- Any known measurement errors or anomalies
- Environmental conditions that may have affected data quality
- Species or sites with incomplete data
- Wavelength regions with lower signal-to-noise ratios

### Data Completeness
- **Spectral data:** [Percentage complete, any systematic gaps]
- **Trait data:** Missing value patterns [describe which traits have most missingness and why]

---

## Reuse Guidance

### Suggested Citation
If you use this dataset, please cite both the data repository and the associated publication:

**Data Citation:**
Pau, S., Slapikas, R., Ho, C. L., Bayliss, S. L. J., Donnelly, R. C., Abdullahi, A., Helliker, B. R., Nippert, J. B., Riley, W. J., Still, C. J., Wedel, E. R., & Griffith, D. M. (2025). *Data from: Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site* [Dataset]. Dryad. https://doi.org/10.5061/dryad.gf1vhhn0n

**Publication Citation:**
Pau, S., et al. (2025). Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site. *Ecosphere*, 16(3), e70257. https://doi.org/10.1002/ecs2.70257

### Example Use Cases
This dataset can be used to:
1. Compare spectral signatures across photosynthetic pathways (C3 vs. C4)
2. Develop predictive models linking functional traits to spectral properties
3. Test remote sensing algorithms for grass species or functional type discrimination
4. Investigate spectral variability within and across sites
5. Validate hyperspectral vegetation indices

### Recommended Software
- **R packages:** `spectrolab`, `hsdar`, `pls`, `randomForest`
- **Python packages:** `pandas`, `numpy`, `scikit-learn`, `scipy`
- **Spectral analysis:** ENVI, VIPER Tools

---

## License and Terms of Use

[**CURATOR NOTE:** Specify license - CC0, CC-BY, etc.]

This dataset is released under [LICENSE]. Users are free to [describe permissions], provided they:
- Cite the dataset and publication as specified above
- [Any additional conditions]

---

## Contact Information

**Dataset Maintainer:** [Name, email]

**Corresponding Author:** [Name from publication]

**Institution:** [Primary affiliation]

**Questions or Issues:** 
If you encounter any problems using this dataset or have questions about the data, please contact [email] or open an issue at [repository URL if applicable].

---

## Version History

- **Version 1.0** [Date]: Initial deposit
- [Future versions would be documented here]

---

## Acknowledgments

[Include funding sources, field site access permissions, laboratory assistance, etc.]

---

**CURATOR'S NOTE TO AUTHORS:**

This README template includes placeholders marked with [**CURATOR NOTE:**] that indicate information missing from or unclear in the current deposit. Filling in these details will significantly improve the dataset's reusability. Priority items for clarification are:

1. **Units for all trait variables** (especially SLA, LDMC, leaf_thickness)
2. **Spectral preprocessing steps** and software used
3. **Site location information** (coordinates, climate data)
4. **Sampling design details** (replication, temporal coverage)
5. **Reflectance value scale** (proportion vs. percentage)
6. **Missing value explanations** (measurement failure vs. not applicable)

These additions would allow independent researchers to confidently reproduce analyses without needing to contact the authors.
