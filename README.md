# wildfire-analysis
### Purpose
This repository contains resources and code for analyzing smoke impact on Green Bay, Wisconsin.

### Licensing
The `common_analysis.ipynb` notebook uses code adapted from example codes for [extracting wildfire geojson data and calculating distances](https://drive.google.com/file/d/1B7AGlaW7d-27bHKLVXGBwLt8T-Elx-HB/view?usp=drive_link) (Revision 1.1 - August 16, 2024) and [acquiring the AQS API data](https://drive.google.com/file/d/1fwS60QStiMDqwINvW2LEDFBX5xg6Wnmg/view?usp=drive_link) (Revision 1.2 - August 16, 2024) developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons CC-BY](https://creativecommons.org/licenses/by/4.0/) license.

The code in this repository is available under the [MIT license](https://opensource.org/license/mit).

### Data

#### Raw Data
Wildfire data - Initial wildfire dataset retrieved from [USGS here](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). We use the `USGS_Wildland_Fire_Combined_Dataset.json` file found in the GeoJSON Files zip file. This file is not included in the repository due to its size. This dataset includes metadata for wildland fires from the 1800s to present. This dataset was collected and aggregated by the US Geological Survey and provides fire polygons in a GeoJSON format.

AQI data - Daily Air Quality Index data is retrieved using the EPA's [AQS API](https://aqs.epa.gov/aqsweb/documents/data_api.html). We focus on Gaseous AQI pollutants CO, SO2, NO2, and O2 and Particulate AQI pollutants PM10, PM2.5, and Acceptable PM2.5. The API provides historical data starting in the 1980's and does not provide any data in real-time. The AQI index indicates how healthy or clean the air is on a specific day.

#### Intermediate Data
`aqi_estimates.csv` - contains the yearly AQI estimates retrieved from the AQS API in the common analysis portion of this project

Schema:
| Column Name    | Data Type |
| -------- | ------- |
| year | Date |
| aqi | Float |

`fire_distance_data.csv` - contains the year, size, and distance to Green Bay of each fire from the wildfire data, used to calculate the smoke estimates

Schema:
| Column Name   | Data Type |
| -------- | ------- |
| Fire_Year | Date |
| Fire_Size_Acres | Float |
| Average Distance to City | Float |

### Analysis Process
#### Part 1 - Common Analysis
In part 1, we start with a common analysis aiming to answer the following research question:
- What are the estimated wildfire smoke impacts on Green Bay, Wisconsin, each year for the most recent 60 years of wildfire data?

The `common_analysis.ipynb` file contains the code used to perform the initial analysis. This notebook contains wildfire data and AQI data collection and processing, as well as smoke estimate calculations and analysis. We output 3 initial visualizations in this part of the project. Detailed figure descriptions can be found in this repository.