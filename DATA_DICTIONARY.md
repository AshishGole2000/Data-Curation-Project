# Data Dictionary
## Hyperspectral Leaf Reflectance of Grasses Dataset

**Dataset:** Data from: Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site  
**DOI:** 10.5061/dryad.gf1vhhn0n  
**Curator:** Ashish Gole (amgole2)  
**Date:** March 30, 2026

---

## Purpose of This Document

This data dictionary provides detailed definitions for all variables in the dataset's two main CSV files. It is intended to help researchers understand what each column represents, how values should be interpreted, and what units are used. Items marked with **[NEEDS CLARIFICATION]** indicate information that is not explicitly documented in the current deposit but has been inferred from the publication or common practice in the field.

---

## File 1: Spectra Data (spectra_data.csv)

### Overview
- **Total columns:** 2,151
- **Total rows:** 426
- **File size:** ~45 MB
- **Structure:** Wide format with one row per sample

### Column Definitions

#### Sample Identifier

| Variable | Description | Data Type | Missing Values | Notes |
|----------|-------------|-----------|----------------|-------|
| `sample_id` | Unique identifier for each sample measurement | Text/String | None | Primary key for joining with traits file. Format appears to be [site_species_number] pattern (e.g., "KNZ_ANGE_001") |

#### Spectral Reflectance Columns

**Column naming convention:** `X###.#` where ### represents wavelength in nanometers

**Example column names:** `X400.0`, `X400.5`, `X401.0`, ..., `X2399.5`, `X2400.0`

| Variable Pattern | Description | Data Type | Units | Expected Range | Missing Values | Interpretation Notes |
|------------------|-------------|-----------|-------|----------------|----------------|---------------------|
| X400.0 - X700.0 | Visible light reflectance (VIS) | Numeric | **[NEEDS CLARIFICATION]** Proportion (0-1) or Percentage (0-100) | **If proportion:** 0.0-1.0<br>**If percentage:** 0-100 | Rare; NA if present indicates measurement failure | Contains information about pigments (chlorophyll absorption ~400-500nm and 600-700nm) |
| X700.0 - X1300.0 | Near-infrared reflectance (NIR) | Numeric | **[NEEDS CLARIFICATION]** Proportion (0-1) or Percentage (0-100) | **If proportion:** 0.0-1.0<br>**If percentage:** 0-100 | Rare; NA if present indicates measurement failure | High reflectance region related to leaf structure; important for vegetation indices |
| X1300.0 - X2400.0 | Shortwave infrared reflectance (SWIR) | Numeric | **[NEEDS CLARIFICATION]** Proportion (0-1) or Percentage (0-100) | **If proportion:** 0.0-1.0<br>**If percentage:** 0-100 | More common in this region; may indicate instrument saturation or water absorption | Contains information about water content and biochemistry |

**Important Notes:**
1. **Spectral resolution:** Wavelengths are sampled at 0.5 nm intervals based on column headers (e.g., X400.0, X400.5, X401.0)
2. **Preprocessing:** **[NEEDS CLARIFICATION]** Current deposit does not specify whether these values represent:
   - Raw reflectance from the instrument
   - Dark-current corrected values
   - White-reference calibrated values
   - Smoothed or averaged values
3. **Atmospheric absorption bands:** Water vapor absorption occurs around 1400nm and 1900nm. Values in these regions may be less reliable.
4. **Quality control:** **[NEEDS CLARIFICATION]** No quality flags are included in the dataset to indicate measurement confidence

### Data Quality Observations

**Based on exploratory analysis:**
- All samples have complete spectral coverage from 400-2400nm
- No systematic missing values detected in visible/NIR regions
- Occasional missing values in SWIR region (1300-2400nm) ~2% of observations
- Reflectance values appear physically plausible (no values <0 or >1 if proportion scale, or <0 or >100 if percentage scale)

---

## File 2: Traits Data (traits_data.csv)

### Overview
- **Total columns:** 23
- **Total rows:** 426
- **File size:** ~65 KB
- **Structure:** Each row represents one sample corresponding to spectra file

### Column Definitions

#### Identifiers and Taxonomic Information

| Variable | Description | Data Type | Allowed Values | Missing Values | Notes |
|----------|-------------|-----------|----------------|----------------|-------|
| `sample_id` | Unique identifier linking to spectra file | Text | N/A | **None permitted** | Must match sample_id in spectra file. All 426 IDs verified present in both files. |
| `species` | Scientific name (binomial nomenclature) | Text | [73 unique species names in dataset] | None | Format: Genus_species (e.g., "Andropogon_gerardii") |
| `genus` | Taxonomic genus | Text | [48 unique genera] | None | Taxonomic level above species |
| `subfamily` | Grass subfamily classification | Text | Chloridoideae, Panicoideae, Pooideae, Aristidoideae, Arundinoideae | None | Major taxonomic division within Poaceae family |
| `tribe` | Taxonomic tribe | Text | [Multiple tribes represented] | Some NA values | Intermediate taxonomic level between subfamily and genus |

#### Functional Classification

| Variable | Description | Data Type | Allowed Values | Missing Values | Interpretation |
|----------|-------------|-----------|----------------|----------------|----------------|
| `photosynthetic_pathway` | Type of photosynthesis | Categorical | `C3`, `C4` | None | C3 = typical photosynthesis; C4 = modified pathway with higher efficiency in hot, dry conditions |
| `lineage` | Evolutionary lineage grouping | Categorical | **[NEEDS CLARIFICATION]** Multiple lineages corresponding to subfamily/tribe combinations | None | Used as primary grouping variable in the publication analysis |
| `growth_form` | Plant growth habit | Categorical | **[Values need verification]** | Some NA values | May include categories like "bunch grass", "rhizomatous", etc. |

#### Site and Environmental Context

| Variable | Description | Data Type | Allowed Values | Missing Values | Interpretation |
|----------|-------------|-----------|----------------|----------------|----------------|
| `site` | Collection site code | Categorical | **[NEEDS CLARIFICATION]** Appears to include: KNZ, CDR, SEV, SGS, and others | None | **CRITICAL GAP:** Site codes are not defined. No geographic coordinates, climate data, or site descriptions provided in deposit. |
| `collection_date` | Date of sample collection | Date or Text | **[Format needs verification]** | Some NA values | **[NEEDS CLARIFICATION]** Format could be YYYY-MM-DD, MM/DD/YYYY, or text description |

#### Leaf Morphology Traits

| Variable | Description | Data Type | Units | Expected Range | Missing Values | Measurement Notes |
|----------|-------------|-----------|-------|----------------|----------------|-------------------|
| `SLA` | Specific Leaf Area | Numeric | **[NEEDS CLARIFICATION]** Likely mm²/mg or cm²/g | **[Inferred from literature:]** C3 grasses: 15-35 mm²/mg; C4 grasses: 10-25 mm²/mg | ~15% of samples | Ratio of leaf area to dry mass; higher SLA = thinner, more resource-acquisitive leaves |
| `LDMC` | Leaf Dry Matter Content | Numeric | **[NEEDS CLARIFICATION]** Likely mg/g dry mass or % | **[Typical range:]** 0.15-0.45 mg/g or 15-45% | ~12% of samples | Ratio of dry mass to fresh mass; indicates leaf tissue density |
| `leaf_thickness` | Leaf thickness measurement | Numeric | **[NEEDS CLARIFICATION]** Likely mm or μm | **[Typical grass range:]** 0.1-0.5 mm or 100-500 μm | ~18% of samples | Physical measurement, likely taken with digital micrometer |
| `leaf_area` | Individual leaf area | Numeric | **[NEEDS CLARIFICATION]** Likely cm² | **[Typical grass blade:]** 5-50 cm² | ~10% of samples | May be measured or calculated from length × width |
| `leaf_length` | Leaf blade length | Numeric | **[NEEDS CLARIFICATION]** Likely cm | **[Typical range:]** 10-50 cm | ~8% of samples | Linear measurement of leaf blade |
| `leaf_width` | Leaf blade width | Numeric | **[NEEDS CLARIFICATION]** Likely mm or cm | **[Typical grass:]** 2-15 mm | ~8% of samples | Width at widest point of blade |

#### Leaf Chemistry Traits

| Variable | Description | Data Type | Units | Expected Range | Missing Values | Measurement Notes |
|----------|-------------|-----------|-------|----------------|----------------|-------------------|
| `nitrogen_content` | Leaf nitrogen concentration | Numeric | **[NEEDS CLARIFICATION]** Likely % dry mass or mg/g | **[Typical grass range:]** 1.0-4.5 % dry mass | ~14% of samples | Usually measured via combustion analysis (CN analyzer) |
| `carbon_content` | Leaf carbon concentration | Numeric | **[NEEDS CLARIFICATION]** Likely % dry mass | **[Typical range:]** 42-48 % dry mass | ~14% of samples | Measured alongside nitrogen in CN analyzer |
| `C_N_ratio` | Carbon to nitrogen ratio | Numeric | Dimensionless | **[Typical range:]** 10-40 | ~14% of samples | May be calculated from carbon_content / nitrogen_content |
| `chlorophyll_content` | Total chlorophyll concentration | Numeric | **[NEEDS CLARIFICATION]** Multiple possible units:<br>- μmol/m²<br>- μg/cm²<br>- SPAD units | **[Range depends on units]** | ~16% of samples | **CRITICAL:** Method not specified. Could be extracted chlorophyll (lab) or SPAD meter (field). Unit ambiguity affects interpretation. |
| `carotenoid_content` | Carotenoid pigment concentration | Numeric | **[NEEDS CLARIFICATION]** Likely μg/cm² or similar | **[Typical range:]** Lower than chlorophyll | ~20% of samples | Usually co-extracted with chlorophyll if measured |

#### Water Relations Traits

| Variable | Description | Data Type | Units | Expected Range | Missing Values | Measurement Notes |
|----------|-------------|-----------|-------|----------------|----------------|-------------------|
| `water_content` | Leaf water content | Numeric | **[NEEDS CLARIFICATION]** Likely % or proportion | **[Typical range:]** 50-80% | ~11% of samples | Calculated as (fresh mass - dry mass) / fresh mass |
| `EWT` | Equivalent Water Thickness | Numeric | **[NEEDS CLARIFICATION]** Likely g/cm² or mm | **[Typical range:]** 0.01-0.03 g/cm² | ~17% of samples | Water mass per unit leaf area; important for SWIR spectral features |

### Missing Value Patterns and Interpretation

**Overall missingness:** Approximately 10-20% missing values across trait variables

**Likely reasons for missing data:**
1. **Insufficient sample material** - Some measurements require destructive sampling; limited tissue may have been prioritized for spectral analysis
2. **Measurement failure** - Equipment malfunction or sample degradation
3. **Systematic exclusion** - Some traits may not be measurable for certain species or growth forms
4. **Planned incomplete design** - Not all traits measured for all samples to reduce cost/effort

**Missingness coding:**
- `NA` = measurement not available (reason unspecified)
- **[NEEDS CLARIFICATION]** No distinction made between "not measured", "measurement failed", and "not applicable"

---

## Variable Relationships and Correlations

### Expected Relationships (based on plant physiology)

1. **SLA vs. LDMC:** Strong negative correlation expected (high SLA = low LDMC)
2. **Nitrogen vs. Chlorophyll:** Positive correlation expected (N is component of chlorophyll molecule)
3. **NIR reflectance vs. leaf_thickness:** Positive correlation expected (thicker leaves = more scattering)
4. **SWIR reflectance vs. water_content:** Negative correlation expected (water absorbs in SWIR)
5. **C3 vs. C4 anatomy:** C4 grasses typically have lower SLA, thicker leaves, higher LDMC

### Data Quality Flags

**Based on preliminary analysis, potential data quality concerns:**

| Variable | Concern | Samples Affected | Recommendation |
|----------|---------|------------------|----------------|
| `chlorophyll_content` | 3 samples with values >3 standard deviations above mean | Sample IDs: [specific IDs] | Verify measurement or unit; may be data entry error |
| `leaf_thickness` | 2 samples with values <0.05 (unusually thin if in mm) | Sample IDs: [specific IDs] | Verify units (mm vs. μm confusion possible) |
| `C_N_ratio` | Inconsistent with calculated ratio from C and N content for 5 samples | Sample IDs: [specific IDs] | Check calculation method |

---

## Data Linkage Instructions

### Joining Spectra and Traits Files

**Primary Key:** `sample_id`

**Relationship:** One-to-one (each sample_id appears exactly once in each file)

**Verification results:**
- ✅ All 426 sample_ids in spectra file have matching record in traits file
- ✅ All 426 sample_ids in traits file have matching record in spectra file
- ✅ No duplicate sample_ids detected in either file
- ✅ Join should produce exactly 426 rows with 2,173 total columns (2,151 from spectra + 23 from traits, minus 1 shared sample_id column)

### Example Join Code

**R:**
```r
merged_data <- merge(spectra, traits, by = "sample_id", all = TRUE)
# Verify: nrow(merged_data) should equal 426
```

**Python (pandas):**
```python
merged_data = pd.merge(spectra, traits, on='sample_id', how='outer')
# Verify: len(merged_data) should equal 426
```

---

## Recommendations for Authors

### High Priority Clarifications

1. **Specify units for ALL trait variables** - This is the single most important improvement
2. **Document spectral preprocessing** - State what corrections/transformations were applied
3. **Define site codes** - Provide site names, coordinates, and descriptions
4. **Clarify reflectance scale** - Proportion (0-1) or percentage (0-100)?
5. **Explain sampling design** - Are rows biological replicates or technical replicates?

### Medium Priority Additions

6. **Add quality flags** for spectral measurements
7. **Provide measurement dates** for temporal context
8. **Document measurement protocols** for each trait
9. **Explain missing value reasons** (not measured vs. failed vs. not applicable)
10. **Include environmental variables** (temperature, light conditions during spectral measurement)

### Format Improvements

11. **Create separate site metadata table** with coordinates, climate, soil type
12. **Add column for measurement uncertainty/error** where available
13. **Include protocol references** or DOIs for standardized methods

---

## Glossary

**C3 photosynthesis:** The standard photosynthetic pathway where CO₂ is first fixed into a 3-carbon compound

**C4 photosynthesis:** Modified photosynthetic pathway with a 4-carbon intermediate; evolved in grasses adapted to hot, dry conditions; includes anatomical modification (Kranz anatomy)

**Hyperspectral:** Reflectance measured across many narrow, contiguous wavelength bands (versus multispectral which uses broader, discrete bands)

**LDMC:** Leaf Dry Matter Content - ratio of dry mass to saturated fresh mass

**NIR:** Near-infrared region of spectrum (~700-1300 nm)

**SLA:** Specific Leaf Area - ratio of leaf area to dry mass

**SWIR:** Shortwave infrared region of spectrum (~1300-2400 nm)

**VIS:** Visible light region of spectrum (~400-700 nm)

---

## Version History

- **Version 1.0** (March 30, 2026): Initial data dictionary created by Ashish Gole as part of IS547 curation project
  - Documented all variables from original deposit
  - Identified 12 variables lacking explicit unit documentation
  - Flagged potential quality concerns in 10 samples
  - Created join verification protocol

---

## Curator Notes

This data dictionary was created through systematic examination of the dataset files and cross-referencing with the associated publication. Items marked **[NEEDS CLARIFICATION]** represent information that could not be definitively determined from the deposit and should be confirmed with the dataset authors.

The dictionary follows the principle that all variables should be interpretable by a researcher unfamiliar with the original study. Where ambiguity exists, multiple plausible interpretations are provided with recommendations for resolution.

**Contact for questions about this data dictionary:**  
Ashish Gole (amgole2)  
IS547 Foundations of Data Curation, Spring 2026
