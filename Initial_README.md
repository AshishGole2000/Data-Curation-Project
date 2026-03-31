# Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site

Dataset DOI: [10.5061/dryad.gf1vhhn0n](10.5061/dryad.gf1vhhn0n)

## Description of the data and file structure

Data for the manuscript titled "Hyperspectral leaf reflectance of grasses varies with evolutionary lineage more than with site," by Pau et. al., from the journal *Ecosphere.*

### Files and variables

#### File: GrassSpecies-Traits.csv

**Description:** 12 Structural, Biochemical, and Physiological Traits for Grass Species across Sites. Please refer to methods section of paper for full description of plant functional traits. A cell value of "null" indicates  that a measurement could not be obtained.

##### Variables

* Site: CPER (Colorado Plains Experimental Range), KONZ (Konza Prairie Biological Station), WOOD (Chase Lake National Wildlife Refuge), Jornada (Jornada Experimental Range), CDCR (Cedar Creek Ecosystem Science Reserve)
* Species: binomial Latin nomenclature
* Transect:
* Subfamily: subfamily
* Tribe: tribe
* LFT: Lineage functional types that break out Andropogoneae from the subfamily Panicoideae
* Photosynthetic Pathway: C3 or C4
* Replicate: replicate
* Leaf_Area (cm2): leaf area 
* Fresh_Thickness (cm): fresh leaf thickness, thickness of leaf in field conditions
* Wet_Thickness (cm): wet leaf thickness, thickness of leaf when fully hydrated
* Wet_Mass (g): leaf wet mass
* Dry_Mass (g): leaf dry mass
* SLA (cm2 g-1): specific leaf area = ratio of leaf area to leaf dry mass
* LDMC: Leaf dry matter content = ratio of leaf dry mass to leaf wet mass
* %C: leaf percent Carbon
* %N: leaf percent Nitrogen
* \_N15: isotopic ratio of Nitrogen-15 to Nitrogen-14
* \_C13: isotopic ratio of Carbon-13 to Carbon-12 
* C:N: ratio of carbon to nitrogen in the leaf
* Vcmax25 (_mol m_2 s_1): maximum rate of carboxylation of the enzyme Rubisco
* Jmax25 (_mol electrons): maximum rate of electron transport during light reactions of photosynthesis

#### File: GrassSpecies-Spectra.csv

**Description:** Spectral (reflectance) Measurements for Grass Species across Sites.

##### Variables

* SPECIES: binomial Latin nomenclature
* SITE: CPER (Colorado Plains Experimental Range), KONZ (Konza Prairie Biological Station), WOOD (Chase Lake National Wildlife Refuge), Jornada (Jornada Experimental Range), CDCR (Cedar Creek Ecosystem Science Reserve)
* C4_C3: Photosynthetic Pathway (C3 or C4)
* LFT: Lineage functional types that break out Andropogoneae from the subfamily Panicoideae
* SUBFAM: subfamily
* TRIBE: tribe
* X1 - X2001: reflectance values from 400nm to 2400nm, every 1nm

## Code/software

The code and software listed below are described in detail in the manuscript methods. In summary, we used:

* the "hsdar" package (Lehnert et al. 2019) in R (R Core Team 2022) to analyze spectral data.

- the "plantecophys" package (Duursma 2015) in R (R Core Team 2022) to fit A-Ci curves and to correct Vcmax25 and Jmax25 to a standard temperature of 25C.

* the  "vegan" package (Oksanen et al. 2019; version 2), including the functions "varpart" and "rda," in R (R Core Team 2022) to analyze the relative effects of tribe, photosynthetic pathway, and site on spectra.

- the "pls" package  (Mevik and Wehrens 2007) in R (R Core Team 2023) to assess how well leaf spectral reflectance could predict leaf traits.

## Access information

Other publicly accessible locations of the data:

* NA

Data was derived from the following sources:

* NA

