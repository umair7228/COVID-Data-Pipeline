# COVID Data Pipeline: ETL with AWS Glue, Athena & Redshift

## Project Overview
This project is an end-to-end ETL (Extract, Transform, Load) pipeline designed to process COVID-19 data from multiple sources, transform it into structured formats, and load it into a cloud data warehouse for analysis. The pipeline leverages **AWS Glue**, **Amazon Athena**, and **Amazon Redshift** for efficient data processing, querying, and storage.

## Project Architecture
![Architecture-Diagram](https://github.com/user-attachments/assets/0412926d-5c73-4bce-ab82-0034dcc4fa3b)

## Architecture
1. **Data Extraction:**  
   - 10 raw datasets stored in Amazon S3.
   - AWS Glue crawlers extract metadata and create tables.

2. **Data Transformation:**  
   - Data queried in Amazon Athena to create:
     - 3 dimension tables (`dimRegion`, `dimHospital`, `dimDate`)
     - 1 fact table (`factCovid`)
   - DataFrames created using Python and Pandas.

3. **Data Loading:**  
   - Transformed data is loaded back to S3 and subsequently into Amazon Redshift using the `COPY` command.

4. **Data Analysis:**  
   - Redshift query editor is used to perform further analysis and generate insights.

## Tech Stack
- **AWS Glue**: Data extraction and transformation.
- **Amazon S3**: Data storage.
- **Amazon Athena**: Querying and creating tables.
- **Amazon Redshift**: Cloud data warehouse.
- **Python**: Data transformation and DataFrame operations.
- **VS Code**: Development environment.

## Fact and Dimension Tables
### Fact Table: `factCovid`
| Column           | Type    | Description                     |
|------------------|---------|---------------------------------|
| fips             | bigint  | FIPS code                       |
| province_state   | string  | State or province               |
| country_region   | string  | Country                         |
| confirmed        | bigint  | Confirmed cases                 |
| deaths           | bigint  | Deaths                          |
| recovered        | bigint  | Recovered cases                 |

### Dimension Table: `dimRegion`
| Column           | Type    | Description                     |
|------------------|---------|---------------------------------|
| fips             | bigint  | FIPS code                       |
| province_state   | string  | State or province               |
| country_region   | string  | Country                         |

### Dimension Table: `dimHospital`
| Column           | Type    | Description                     |
|------------------|---------|---------------------------------|
| fips             | bigint  | FIPS code                       |
| hospital_name    | string  | Name of the hospital            |

### Dimension Table: `dimDate`
| Column           | Type    | Description                     |
|------------------|---------|---------------------------------|
| date             | string  | Date of record                  |
