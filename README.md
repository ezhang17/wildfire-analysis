# wildfire-analysis
## Purpose
This repository contains resources and code for analyzing smoke impact on Green Bay, Wisconsin for the last 60 years. We start with a common analysis and formulation of a smoke estimate using wildfire data.

## Licensing
The `common_analysis.ipynb` notebook uses code adapted from example codes for [extracting wildfire geojson data and calculating distances](https://drive.google.com/file/d/1B7AGlaW7d-27bHKLVXGBwLt8T-Elx-HB/view?usp=drive_link) (Revision 1.1 - August 16, 2024) and [acquiring the AQS API data](https://drive.google.com/file/d/1fwS60QStiMDqwINvW2LEDFBX5xg6Wnmg/view?usp=drive_link) (Revision 1.2 - August 16, 2024) developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons CC-BY](https://creativecommons.org/licenses/by/4.0/) license.

The code in this repository is available under the [MIT license](https://opensource.org/license/mit).

## Analysis Process
### Part 1 - Common Analysis
In part 1, we start with a common analysis aiming to answer the following research question:
- What are the estimated wildfire smoke impacts on Green Bay, Wisconsin, each year for the most recent 60 years of wildfire data?

#### Code
The `common_analysis.ipynb` file contains the code used to perform the initial analysis. This notebook contains wildfire data and AQI data collection and processing, as well as smoke estimate calculations and analysis. The notebook requires the following packages:

**Standard Python modules**: os, json, time

**Other Python modules**: pyproj, requests, dotenv, pandas, numpy, matplotlib, statsmodels, wildfire*

*The 'wildfire' module is a user module created by Dr. David W. McDonald for student use in solving the DATA 512 class project. This module is not for reuse without express permissions.

#### Output Files
The visualizations created in this part can be found in the `common_analysis_visualizations` folder of this repository. A detailed description of each visualization as well as a reflection on collaboration is also included in the `common_analysis_visualizations` folder of this repository (`Common Analysis Visualization Descriptions and Reflection.pdf`).

The intermediate data files, `aqi_estimates.csv` and `fire_distance_data.csv`, are included in the `intermediate_data` folder of the repository. More details are included in the Data section below.

### Part 2 - Asthma Analysis
!!!!!!!!!!!!!!!!!!!!!! need to fill in
#### Code
`asthma_analysis.ipynb`
#### Output Files


## Data

### Raw Data
**Wildfire data** - Initial wildfire dataset retrieved from [USGS here](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). We use the `USGS_Wildland_Fire_Combined_Dataset.json` file found in the GeoJSON Files zip file. This file is not included in the repository due to its size. This dataset includes metadata for wildland fires from the 1800s to present. This dataset was collected and aggregated by the US Geological Survey and provides fire polygons in a GeoJSON format. Note that this data cuts off at 2020, so we use 1964-2020 data to represent the past 60 years.

**AQI data** - Daily Air Quality Index data is retrieved using the [US EPA Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html). We focus on Gaseous AQI pollutants CO, SO2, NO2, and O2 and Particulate AQI pollutants PM10, PM2.5, and Acceptable PM2.5. The API provides historical data starting in the 1980's and does not provide any data in real-time. The AQI index indicates how healthy or clean the air is on a specific day. Due to the formation of the EPA in the 1970's and installation of stations in the 1980's, AQI data for Green Bay is only available starting from 1985. More details on how AQI is calculated can be found [here](https://document.airnow.gov/technical-assistance-document-for-the-reporting-of-daily-air-quailty.pdf).

**Asthma data** - Asthma emergency room visit and hospitalization age-adjusted rates per 10,000 people were retrieved from the [Environmental Public Health Tracking: Asthma Data dashboard](https://www.dhs.wisconsin.gov/epht/asthma.htm) provided by the Wisconsin Department of Health Services. We use asthma metrics to investigate the impact of smoke on those most at-risk of health impacts from exposure to wildfire smoke. Wildfire smoke has been [shown](https://doi.org/10.1007/s11882-023-01090-1) to have a clear association with acute effects on asthma. The emergency room visit data is available from 2002 through 2023, and hospitalization data is available from 2000 through 2022. Datasets were obtained by filtering the interactive dashboard to Brown County and downloading from the county-specific trend view. As outlined in the [Wisconsin.Gov Privacy Policy](https://www.wisconsin.gov/Pages/Policies.aspx), material on the website is available for noncommercial use by the general public under fair use guidelines. The data itself follows HIPAA guidelines by retaining the data anonymously. Counts less than five but more than zero are suppressed to protect confidentiality.

These datasets were first cleaned in Excel by simply deleting unneeded columns and retaining only the county and state age-adjusted rates. The files created from the simple deletion are in the `asthma_data` folder in the repository. Further cleaning and manipulation code can be found in the `asthma_analysis.ipynb` Notebook.

`Brown County Asthma Emergency Visit Rates.csv` - contains the county-level and state-level age-adjusted asthma emergency room visit rates per 10,000 people from 2002 through 2023 for Brown County, WI

`Brown County Asthma Emergency Visit Rates.csv` sample data:
| Year   | 2002 | 2003 | 2004 | ... |
| -------- | ------- | ------- | ------- | ------- |
| County rate | 43.4 | 46.6 | 46.2 | ... |
| State rate | 48.21 | 50.27 | 46.32 | ... |

`Brown County Asthma Hospitalization Rates.csv` - contains the county-level and state-level age-adjusted asthma hospitalization rates per 10,000 people from 2002 through 2023 for Brown County, WI

`Brown County Asthma Hospitalization Rates.csv` sample data:
| Year   | 2000 | 2001 | 2002 | ... |
| -------- | ------- | ------- | ------- | ------- |
| County rate | 9.1 | 8.8 | 8.8 | ... |
| State rate | 10.72 | 10.23 | 9.73 | ... |

### Intermediate Data
`aqi_estimates.csv` - contains the yearly AQI estimates retrieved from the AQS API in the common analysis portion of this project

`aqi_estimates.csv` schema:
| Column Name    | Data Type |
| -------- | ------- |
| year | Date |
| aqi | Float |

`fire_distance_data.csv` - contains the year, size, and distance to Green Bay of each fire from the wildfire data, used to calculate the smoke estimates. Note that this data contains the full set of years available in the wildfire data, including those before 1964

`fire_distance_data.csv` schema:
| Column Name   | Data Type |
| -------- | ------- |
| Fire_Year | Date |
| Fire_Size_Acres | Float |
| Average Distance to City | Float |

`smoke_estimates.csv` - contains the smoke estimates calculated in `common_analysis.ipynb` using fire distance and size from 1964 through 2020

`smoke_estimates.csv` schema:
| Column Name   | Data Type |
| -------- | ------- |
| Fire_Year | Date |
| Agg_Smoke_Estimate | Float |
| Smoke_Estimate | Float |

`smoke_predictions.csv` - contains the smoke estimate predictions for 2025-2050 created in `common_analysis.ipynb` using the exponential smoothing model fitted to the historical smoke estimates

`smoke_predictions.csv` schema:
| Column Name   | Data Type |
| -------- | ------- |
| Year | Date |
| Forecast | Float |
| Upper CI | Float |
| Lower CI | Float |