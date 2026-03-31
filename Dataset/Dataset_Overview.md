# Grass Species Hyperspectral Dataset
## Dataset Overview

---

## Description

This dataset contains hyperspectral reflectance measurements and functional trait data for grass species collected across multiple grassland sites in North America. The data supports research on plant spectral ecology, photosynthetic pathways, and the relationship between leaf traits and optical properties.

---

## Dataset Composition

**Spectra File (GrassSpecies-Spectra.csv):**

* 650 samples × 2,007 columns
* Contains: Species name, site code, photosynthetic pathway (C3/C4), taxonomic classification, and 2,000 spectral bands (X1-X2000)
* Spectral measurements represent leaf reflectance values across the electromagnetic spectrum

**Traits File (GrassSpecies-Traits.csv):**

* 293 samples × 22 columns
* Contains: Site, species, taxonomic info, photosynthetic pathway, leaf morphology (area, thickness), chemistry (carbon, nitrogen, C:N ratio), and physiological measurements (SLA, LDMC, Vcmax, Jmax)

---

## Key Statistics

* **Species coverage:** 66 grass species
* **Sites:** 5 grassland locations (CDCR, CPER, JORN, KONZ, WOOD)
* **Taxonomic groups:** Multiple grass subfamilies including Pooideae, Panicoideae, Chloridoideae
* **Photosynthetic pathways:** Both C3 and C4 grasses represented

---

## Primary Variables

**Spectral data:** 2,000 reflectance bands capturing leaf optical properties across visible, near-infrared, and shortwave infrared regions

**Functional traits:** Leaf area, thickness, specific leaf area (SLA), leaf dry matter content (LDMC), carbon and nitrogen content, photosynthetic capacity (Vcmax, Jmax)

---

## File Relationship

The two files can be linked using the **Species** and **Site** columns present in both datasets. Note that the spectra file contains more samples (650) than the traits file (293), indicating that not all spectral measurements have corresponding trait data.

---

## Potential Uses

* Comparing spectral signatures between C3 and C4 photosynthetic pathways
* Developing predictive models linking leaf traits to spectral properties
* Remote sensing algorithm development and validation for grassland monitoring
* Investigating spectral variability across species, sites, and functional groups
