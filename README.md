# wildfire-analysis
### Purpose

### Licensing

### Data

#### Raw Data
Wildfire data - Initial wildfire dataset retrieved from [USGS here](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). We use the `USGS_Wildland_Fire_Combined_Dataset.json` file found in the GeoJSON Files zip file. This file is not included in the repository due to its size.

AQI data - Daily Air Quality Index data is retrieved using the EPA's [AQS API](https://aqs.epa.gov/aqsweb/documents/data_api.html).

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