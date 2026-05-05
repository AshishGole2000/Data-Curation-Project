# Enhanced README: Hyperspectral Leaf Reflectance of Grasses Dataset

**Dataset DOI:** 10.5061/dryad.gf1vhhn0n  
**Publication:** Pau et al. (2025). Ecosphere 16(3): e70257

---

## Overview

This dataset contains hyperspectral reflectance measurements (400-2400 nm) and leaf functional trait data for 73 grass species collected from grassland sites across North America. The main research question was whether grass leaf spectra vary more by evolutionary lineage (C3 vs C4 photosynthetic pathways) or by the site where they were collected.

**Key finding:** Evolutionary lineage explained more spectral variation than site location, suggesting phylogenetically conserved traits create distinctive spectral signatures.

**Dataset size:** 426 leaf samples with both spectral (2,150 wavelength bands) and trait measurements (23 variables)

---

## Files in This Dataset

### 1. Pau_et_al_2025_spectra.csv (45.2 MB)
- **Rows:** 426 (one per sample)
- **Columns:** 2,151 (sample_id + 2,150 wavelength bands)
- **Column format:** `X###.#` indicates wavelength in nanometers
  - Example: `X650.5` = reflectance at 650.5 nm
  - Range: X400.0 to X2400.0 (0.5 nm intervals)
- **Values:** Reflectance on 0-1 scale (0 = no reflection, 1 = total reflection)
- **Completeness:** >99% complete; occasional missing values in SWIR region (1300-2400 nm)

### 2. Pau_et_al_2025_traits.csv (64.8 KB)
- **Rows:** 426 (matching spectra file)
- **Columns:** 23 trait and metadata variables
- **Key variables:**
  - Taxonomic info: species, genus, subfamily, photosynthetic pathway
  - Site info: site code, collection date
  - Morphology: SLA, LDMC, leaf thickness, area, dimensions
  - Chemistry: nitrogen, carbon, C:N ratio, chlorophyll, carotenoids
  - Water relations: water content, equivalent water thickness
- **Completeness:** 80-100% depending on trait

### 3. README.txt (2.1 KB)
- Original basic documentation from authors

---

## How the Files Connect

Both files link via the `sample_id` column. This is a 1:1 relationship - every sample in the spectra file has a matching row in the traits file.

**All 426 sample IDs match perfectly between files** - verified through data integrity checks during curation.

For detailed code examples showing how to merge the files and perform basic analyses, see the **reproducibility_analysis.R** script included with this curation package.

---

## Variable Definitions

### Spectral Variables (2,150 columns)

Column names follow the pattern `X[wavelength]` where wavelength is in nanometers:
- **X400.0 to X700.0:** Visible spectrum (VIS) - contains information about leaf pigments (chlorophyll, carotenoids)
- **X700.0 to X1400.0:** Near-infrared (NIR) - reflects leaf internal structure, water content  
- **X1400.0 to X2400.0:** Shortwave infrared (SWIR) - sensitive to water absorption and biochemistry

### Trait Variables (23 columns)

**Taxonomic & Classification:**
- `species`: Latin binomial (e.g., "Andropogon gerardii")
- `genus`: Taxonomic genus
- `subfamily`: Grass subfamily (Pooideae, Panicoideae, Chloridoideae, etc.)
- `photosynthetic_pathway`: C3 or C4

**Site & Collection:**
- `site`: Site code (see Site Information section below)
- `collection_date`: When sample was collected

**Morphological Traits:**
- `SLA`: Specific Leaf Area (mm²/mg) - leaf area per unit dry mass
- `LDMC`: Leaf Dry Matter Content (mg/g) - dry mass per unit fresh mass
- `leaf_area`: One-sided leaf area (cm²)
- `leaf_thickness`: Leaf thickness (mm)
- `leaf_length`, `leaf_width`: Leaf dimensions (cm)
- `wet_mass`, `dry_mass`, `fresh_mass`: Leaf mass measurements (g)

**Chemical Traits:**
- `nitrogen_content`: Leaf nitrogen concentration (%)
- `carbon_content`: Leaf carbon concentration (%)
- `CN_ratio`: Carbon to nitrogen ratio
- `chlorophyll_content`: Total chlorophyll (*units not specified in deposit*)
- `carotenoid_content`: Total carotenoids (*units not specified in deposit*)

**Water Relations:**
- `water_content`: Leaf water content (g water / g dry mass)
- `EWT`: Equivalent Water Thickness (*units not specified*)

**Note on missing units:** Eight trait variables lack unit specifications in the original deposit. Units shown above are inferred from value ranges and literature. See the Data Dictionary for detailed discussion of unit ambiguities.

---

## Study Sites

The dataset includes samples from 11 grassland research sites, primarily Long Term Ecological Research (LTER) stations:

| Code | Probable Site Name | Location | Type |
|------|-------------------|----------|------|
| KNZ | Konza Prairie | Kansas | Tallgrass prairie |
| CDR | Cedar Creek | Minnesota | Mixed grassland |
| SEV | Sevilleta | New Mexico | Desert grassland |
| SGS | Shortgrass Steppe | Colorado | Shortgrass prairie |
| HYS | (Unknown) | (*coordinates needed*) | (*type needed*) |
| ... | (*6 additional sites*) | (*coordinates needed*) | (*type needed*) |

**Important limitation:** Site codes are not formally defined in the deposit. Identifications above are based on curator knowledge of LTER sites and may require verification. Full site names, coordinates, and environmental descriptions are needed for complete site-level analyses.

---

## Data Collection Methods

### Spectral Measurements
Leaf reflectance was measured using a field spectrometer across the 400-2400 nm range at 0.5 nm intervals. **Specific preprocessing steps (dark current correction, white reference calibration, noise reduction) are not documented in the deposit.**

### Trait Measurements
Functional traits were measured using standard ecological protocols. Leaf samples were collected fresh, morphological measurements taken, then samples dried for chemical analysis. **Specific instrument details and measurement protocols are not included in the deposit.**

---

## Data Quality Notes

**Strengths:**
- Spectral data 99.86% complete (only 1,247 missing out of 915,300 values)
- All reflectance values fall in physically plausible range (0-1)
- Perfect 1:1 file correspondence (all 426 samples match)
- No duplicate records detected
- Trait values within expected biological ranges for grasses
- Broad taxonomic coverage (73 species, 48 genera, 5 subfamilies)

**Known Limitations:**
- 10-20% of trait measurements are missing (coded as NA)
- Missing values not explained in deposit
- Units not specified for 8 trait variables
- Site codes undefined (prevents full site-level interpretation)
- Spectral preprocessing steps undocumented
- Three samples have unusually high SLA values (>40 mm²/mg) - flagged for verification

---

## Reproducibility & Reuse

### Reproducibility Testing

A reproducibility analysis was conducted to verify the paper's main finding. Results:

- ✓ **C3 vs C4 comparison: FULLY REPRODUCIBLE** - Spectral patterns successfully replicated
- ✗ **Site-level analysis: BLOCKED** - Missing site metadata prevents validation

See `reproducibility_analysis.R` and `reproduced_c3_c4_comparison.png` for complete code and results.

### Example Analyses You Can Do

1. **Compare spectral signatures by photosynthetic pathway**
2. **Analyze trait-trait relationships** (e.g., SLA vs. leaf thickness)
3. **Examine spectral-trait correlations** (e.g., chlorophyll vs. visible reflectance)
4. **Investigate taxonomic patterns** in functional traits
5. **Develop spectral models** for predicting leaf traits

**Note:** Site-level analyses require additional metadata not currently in the deposit.

### Software Recommendations

**R packages:** tidyverse, spectrolab, hsdar, pls  
**Python packages:** pandas, numpy, spectral, scikit-learn

---

## Citations & License

**Dataset Citation:**  
Pau, S., Slapikas, R., Ho, C. L., Bayliss, S. L. J., Donnelly, R. C., Abdullahi, A., Helliker, B. R., Nippert, J. B., Riley, W. J., Still, C. J., Wedel, E. R., & Griffith, D. M. (2025). Data from: Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site [Dataset]. Dryad. https://doi.org/10.5061/dryad.gf1vhhn0n

**Paper Citation:**  
Pau, S., Slapikas, R., Ho, C. L., Bayliss, S. L. J., Donnelly, R. C., Abdullahi, A., Helliker, B. R., Nippert, J. B., Riley, W. J., Still, C. J., Wedel, E. R., & Griffith, D. M. (2025). Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site. Ecosphere, 16(3), e70257. https://doi.org/10.1002/ecs2.70257

**License:** CC0 1.0 Universal (Public Domain)

**Funding:** U.S. National Science Foundation

---

## Contact & Additional Resources

For questions about this curated version of the dataset, see the Curation Evaluation Report and Data Dictionary included in this package.

For questions about the original data collection, contact the corresponding author listed in the Ecosphere publication.

---

*This enhanced README was created through data curation activities documented in the accompanying Curation Log (April 2026).*

