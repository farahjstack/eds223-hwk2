# Redlining's Legacy in Los Angeles: Environmental Justice and Bike/Pedestrian Crashes

## About
This repository contains Homework 2 for EDS 223: Geospatial Analysis and Remote Sensing, part of the Master of Environmental Data Science (MEDS) program at the Bren School of Environmental Science & Management, University of California, Santa Barbara.

This assignment combines historical Home Owners' Loan Corporation (HOLC) redlining maps with the U.S. Environmental Protection Agency's (EPA) 2023 EJScreen dataset and 2020-2025 SWITRS crash reports to explore how 1930s neighborhood grades relate to present-day conditions in Los Angeles County, California. Part 1 maps HOLC grades and compares socioeconomic and environmental indicators across them. Part 2 examines how bike and pedestrian crashes are distributed across HOLC grades.

The goal of this analysis is to explore whether the legacy of redlining is still visible in environmental exposure, health, and traffic safety outcomes
## Repository Contents
* `HW2.qmd`: Quarto document with R code, maps, figures, tables, and written analysis.
* `HW2.pdf`: Rendered PDF of the Quarto document.
* `.gitignore`: Excludes the locally stored `data/` folder from Git version control.
* `README.md`: Project overview, data information, and references.

## Data
The data are not stored in this repository. Download the course data bundle, unzip it, and place the folders in a `data/` directory.

**Sources** 
* U.S. Environmental Protection Agency (EPA), EJScreen 2023 (block group level).
* Digital Scholarship Lab, University of Richmond, Mapping Inequality project.
* California Statewide Integrated Traffic Records System (SWITRS), hosted on UC Berkeley SafeTREC's Transportation Injury Mapping System (TIMS).

**Files used:**
* `ejscreen/EJSCREEN_2023_BG_StatePct_with_AS_CNMI_GU_VI.gdb`: Geodatabase of environmental and demographic indicators, filtered to Los Angeles County.
* `ejscreen/EJSCREEN_2023_BG_Columns.xlsx`: Dataset column descriptions.
* `ejscreen/ejscreen-tech-doc-version-2-2.pdf`: EJScreen technical documentation.
* `mapping-inequality/mapping-inequality-los-angeles.json`: Digitized HOLC grade (A-D) polygons for Los Angeles.
* `SWITRS_LA/Crashes.csv`: Crash reports from 2020-2025, filtered to pedestrian and bicycle crashes

## Reproducing the Analysis
1. Clone or download this GitHub repository.
2. Download the course data and place the folders in `data/` (`data/ejscreen`, `data/SWITRS_LA`, `data/mapping-inequality`).
3. Install the required R packages.
4. Open `HW2.qmd` in RStudio or another R-compatible environment.
5. Check that the file paths in the data-loading chunk match your local folder names.
6. Render the Quarto document to PDF to generate the maps, figures, tables, and written analysis.

## Methods
Spatial data were processed and visualized in R using the following packages:

* `tidyverse`
* `sf`
* `here`
* `tmap`
* `gt`

**Part 1:** EJScreen block groups were filtered to Los Angeles County and spatially joined to HOLC polygons. The percent of block groups in each HOLC grade (including those outside any graded area) was summarized in a table. Mean percent low income, PM2.5 percentile, and low life expectancy percentile were calculated by HOLC grade and plotted with `ggplot2`. A `tmap` map shows HOLC grades over an OpenStreetMap basemap.

**Part 2:** Crashes with missing `POINT_X`/`POINT_Y` coordinates were removed, and the rest were converted to points. Crashes were filtered to `PEDESTRIAN_ACCIDENT` or `BICYCLE_ACCIDENT`, kept if they fell within Los Angeles County, and spatially joined to HOLC polygons. The percent of crashes in each grade was then plotted.

All layers were transformed to a common coordinate reference system, with checks that print a warning if they do not match.

## Author
Farah Stack

## References

- U.S. Environmental Protection Agency. (2023). _EJScreen: Environmental Justice Screening and Mapping Tool._ https://www.epa.gov/ejscreen

- Nelson, R. K., Winling, L., et al. _Mapping Inequality: Redlining in New Deal America._ Digital Scholarship Lab, University of Richmond. https://dsl.richmond.edu/panorama/redlining/

- UC Berkeley SafeTREC. _Transportation Injury Mapping System (TIMS)_ and _SWITRS Codebook._ https://tims.berkeley.edu/

- UCSB Master of Environmental Data Science. *_DS 223: Geospatial Analysis and Remote Sensing._ https://eds-223-geospatial.github.io

## Acknowledgements
Special thanks to Professor Annie Adams and Teaching Assistant Mary Salami for their instruction and guidance throughout EDS 223. Additional appreciation goes to the UCSB MEDS cohort for their collaboration, shared learning, and support.
