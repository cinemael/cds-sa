# Mapping Migratory Wader Hotspots in Denmark

**Spatial Analytics — Supplementary Subject in Cultural Data Science, Spring 2026**  
Ismael Kreie Engelbreth Larsen, 6th semester, Information Science BSc  
Aarhus University

---

## Overview

This project applies Kernel Density Estimation (KDE) to citizen science occurrence records of migratory wading birds (family Scolopacidae) in Denmark to identify spatial hotspots during peak migration periods and assess their correspondence with EU Bird Protection Areas (Natura 2000 SPAs).

**Research question:** Where do citizen science observations of migratory wading birds cluster in Denmark during peak migration periods, and to what extent do these spatial hotspots correspond to officially designated EU Bird Protection Areas?

---

## Repository structure

```
├── data/
│   ├── gbif_scolopacidae_dk.csv        # GBIF occurrence download (see Data sources)
│   └── bird_protection_areas.gpkg      # EU Bird Protection Areas (auto-downloaded if missing)
├── output/
│   ├── raw_observations.png            # Figure 1: Raw observation dot map
│   ├── kde_hotspots.png                # Figure 2: KDE hotspot surface
│   └── kde_with_protection.png         # Figure 3: KDE overlaid with protection areas
├── src/
│   └── wader_hotspots_dk.Rmd           # Main analysis script
├── README.md
└── session_info.txt                    # R session info for reproducibility
```

---

## Data sources

### GBIF occurrence data
- **Source:** Global Biodiversity Information Facility (GBIF)
- **Filter:** Family Scolopacidae, country Denmark, human observations, 2016–2025
- **DOI:** [10.15468/dl.tt323j](https://doi.org/10.15468/dl.tt323j)
- **License:** CC BY-NC 4.0
- **Downloaded:** 1 June 2026
- The CSV file must be placed in data/ before running the analysis. It is not included in the repository due to file size.

### EU Bird Protection Areas
- **Source:** Danmarks Miljøportal / Arealdata API
- **Dataset:** Natura 2000 Fuglebeskyttelse (EF-fuglebeskyttelsesområder)
- **URL:** https://arealdata.miljoeportal.dk/datasets/urn:dmp:ds:natura2000-fuglebeskyttelse
- **License:** Creative Commons CC0 1.0
- **Last updated:** 1 June 2026
- If `bird_protection_areas.gpkg` is not present in `data/`, the analysis script will download it automatically from Danmarks Miljøportal.

### Denmark boundary
- **Source:** DAWA — Danmarks Adressers Web API, maintained by Dataforsyningen
- **URL:** https://dawadocs.dataforsyningen.dk
- Retrieved programmatically at runtime via GeoJSON endpoint. No local file required.

---

## How to reproduce the analysis

### Requirements

- R version 4.5.1 or later
- RStudio (recommended for R Markdown)

### R packages

| Package | Version | Purpose |
|---------|---------|---------|
| tidyverse | 2.0.0 | Data manipulation and visualisation |
| sf | 1.1-1 | Spatial data handling |
| MASS | 7.3-65 | Kernel density estimation (kde2d) |
| ggplot2 | 4.0.2 | Map visualisation |
| lubridate | 1.9.4 | Date handling |

Install all required packages with:

```r
install.packages(c("tidyverse", "sf", "MASS", "ggplot2", "lubridate"))
```

### Steps

1. Clone or download this repository
2. Place gbif_scolopacidae_dk.csv in the data/ folder (download from DOI above)
3. Open `src/wader_hotspots_dk.Rmd` in RStudio
4. Click **Knit** or run all chunks with `Ctrl+Alt+R`
5. Output maps are saved to `output/`

---

## Output

| File | Description |
|------|-------------|
| `raw_observations.png` | 10% random sample of cleaned occurrence records plotted as points |
| `kde_hotspots.png` | KDE density surface showing observation hotspots |
| `kde_with_protection.png` | KDE surface overlaid with EU Bird Protection Areas (green) |

---

## License

This project is submitted as an academic exam project at Aarhus University. The code is made available for transparency and reproducibility. The GBIF data is licensed under CC BY-NC 4.0; the Miljøportal data under CC0 1.0.
