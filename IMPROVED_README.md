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

**To merge in R:**
```r
spectra <- read.csv("Pau_et_al_2025_spectra.csv")
traits <- read.csv("Pau_et_al_2025_traits.csv")
data <- merge(spectra, traits, by = "sample_id")
```

**To merge in Python:**
```python
import pandas as pd
spectra = pd.read_csv("Pau_et_al_2025_spectra.csv")
traits = pd.read_csv("Pau_et_al_2025_traits.csv")
data = pd.merge(spectra, traits, on='sample_id')
```

---

## Variable Definitions

### Spectral Variables

Each wavelength column contains reflectance values at that specific wavelength. The spectrum is divided into three main regions:

- **Visible (VIS): 400-700 nm** - Pigment absorption, especially chlorophyll
- **Near-Infrared (NIR): 700-1300 nm** - Leaf structure and scattering
- **Shortwave Infrared (SWIR): 1300-2400 nm** - Water content and biochemistry

### Trait Variables

**Identifiers:**
- `sample_id` - Unique sample identifier (links to spectra file)
- `species` - Scientific name (73 species total)
- `genus` - Taxonomic genus
- `subfamily` - Grass subfamily (5 categories)
- `photosynthetic_pathway` - C3 or C4
- `site` - Collection site code (11 sites)

**Morphological Traits:**
- `SLA` - Specific Leaf Area (mm²/mg) - leaf area per unit mass
- `LDMC` - Leaf Dry Matter Content (mg/g) - tissue density
- `leaf_thickness` - Thickness in mm
- `leaf_area` - Individual leaf area (cm²)
- `leaf_length` - Blade length (cm)
- `leaf_width` - Blade width (mm)

**Chemical Traits:**
- `nitrogen_content` - Leaf N concentration (% dry mass)
- `carbon_content` - Leaf C concentration (% dry mass)
- `C_N_ratio` - Carbon to nitrogen ratio
- `chlorophyll_content` - Chlorophyll concentration (units vary, likely μmol/m² or SPAD)
- `carotenoid_content` - Carotenoid pigments (μg/cm²)

**Water Relations:**
- `water_content` - Leaf water content (%)
- `EWT` - Equivalent water thickness (g/cm²)

**Missing values:** Coded as `NA`. About 10-20% of trait measurements are missing depending on the variable. Nitrogen and carbon have identical missing patterns because they're measured together.

---

## Study Sites

Samples were collected from grassland research sites across North America during peak growing season. The dataset includes 11 site codes:

- **KNZ** - Konza Prairie, Kansas (tallgrass prairie)
- **CDR** - Cedar Creek, Minnesota (tallgrass prairie)
- **SEV** - Sevilleta, New Mexico (desert grassland)
- **SGS** - Shortgrass Steppe, Colorado (shortgrass prairie)
- **HYS** - Hays, Kansas (mixed-grass prairie)
- Plus 6 additional grassland sites

Full site details and coordinates are available in the publication.

---

## Data Collection Methods

**Spectral measurements:**
Hyperspectral reflectance was measured from the upper leaf surface using a spectroradiometer. The data have been processed to:
- Remove dark current (instrument background)
- Calibrate to white reference standard
- Correct for detector transitions
- Average multiple scans per sample

The deposited values are calibrated reflectance on a 0-1 scale.

**Trait measurements:**
Traits were measured following standard protocols:
- Morphology: Leaf area scanners, digital calipers/micrometers
- Chemistry: CN elemental analyzer for N and C, spectrophotometric extraction for chlorophyll
- Water: Fresh and dry mass measurements

All destructive measurements were taken after spectral scans to avoid damaging leaves.

---

## Data Quality Notes

**What's good:**
- High spectral completeness (>99%)
- All 426 samples have matching trait records
- Values fall within expected biological ranges
- Standard measurement protocols followed

**What to watch out for:**
- Some missing trait data (10-20% depending on variable)
- Higher noise in SWIR region around water absorption bands (~1400nm, 1900nm)
- A few potential outliers flagged:
  - 3 samples with very high SLA (>40 mm²/mg) - check if analyzing extremes
  - 2 samples with unusually high chlorophyll values

**Limitations:**
- Samples from peak growing season only (no seasonal variation)
- Healthy leaves only (no stress or damage)
- Sites concentrated in central/western North America

---

## Example Uses

This dataset is useful for:

1. **Comparing C3 vs C4 grass spectra** - Clear spectral differences between photosynthetic pathways
2. **Predicting traits from spectra** - Use PLSR or machine learning to predict leaf N, chlorophyll, etc.
3. **Developing vegetation indices** - Test or create indices for grassland remote sensing
4. **Phylogenetic analysis** - Examine evolutionary patterns in leaf optical properties
5. **Trait ecology** - Investigate leaf economics relationships in grasses

**Quick example - Plot mean spectra by photosynthetic pathway:**

```r
library(tidyverse)

# Load and merge data
spectra <- read.csv("Pau_et_al_2025_spectra.csv")
traits <- read.csv("Pau_et_al_2025_traits.csv")
data <- merge(spectra, traits, by = "sample_id")

# Get wavelength columns and convert to numeric wavelengths
wl_cols <- grep("^X[0-9]", names(data), value = TRUE)
wavelengths <- as.numeric(gsub("X", "", wl_cols))

# Calculate mean spectra
c3_mean <- data %>% filter(photosynthetic_pathway == "C3") %>%
  select(all_of(wl_cols)) %>% colMeans(na.rm = TRUE)
c4_mean <- data %>% filter(photosynthetic_pathway == "C4") %>%
  select(all_of(wl_cols)) %>% colMeans(na.rm = TRUE)

# Plot
plot(wavelengths, c3_mean, type = "l", col = "blue", lwd = 2,
     xlab = "Wavelength (nm)", ylab = "Reflectance",
     main = "C3 vs C4 Grass Spectra")
lines(wavelengths, c4_mean, col = "red", lwd = 2)
legend("topleft", legend = c("C3", "C4"), col = c("blue", "red"), lwd = 2)
```

---

## Citation

**If you use this dataset, please cite both:**

**Dataset:**  
Pau, S., Slapikas, R., Ho, C. L., Bayliss, S. L. J., Donnelly, R. C., Abdullahi, A., Helliker, B. R., Nippert, J. B., Riley, W. J., Still, C. J., Wedel, E. R., & Griffith, D. M. (2025). Data from: Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site [Dataset]. Dryad. https://doi.org/10.5061/dryad.gf1vhhn0n

**Paper:**  
Pau, S., et al. (2025). Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site. Ecosphere 16(3): e70257. https://doi.org/10.1002/ecs2.70257

---

## Useful Software

**R packages:**
- `spectrolab`, `hsdar` - spectral analysis
- `pls` - partial least squares regression
- `tidyverse` - data manipulation and plotting

**Python packages:**
- `pandas`, `numpy` - data handling
- `scikit-learn` - machine learning
- `matplotlib` - plotting

---

## Contact

For questions about the dataset or methods, see contact information in the Ecosphere publication. For download issues, contact Dryad support.

---

## License

CC0 (Public Domain) - Free to use for any purpose. Please cite as shown above.

---

## Notes

This enhanced README was created to improve documentation and usability of the dataset. It supplements the original README.txt file included in the deposit. Information is based on the dataset files, publication, and standard spectroscopy/trait measurement protocols.

Some details (like exact spectral processing software or specific site coordinates) are not explicitly documented in the deposit. These details are available in the publication or by contacting the authors.

**Created by:** Ashish Gole (amgole2)  
**Course:** IS547 Data Curation, Spring 2026  
**Last updated:** March 30, 2026
