# Netflix_Azure_Data_Engineering_Project
 ![How-Netflix-Changed-story-telling-Marksmen-Daily](https://github.com/user-attachments/assets/74355d28-b158-45dc-9a1e-7328dafb2e92)
 
# Project Overview
This project is designed to process and analyze Netflix Movies and TV Shows data using Azure Data Factory, Databricks, and Power BI. The pipeline ingests raw data, transforms it, and serves it in a star schema for analytics.

## Data Overview 
This tabular dataset consists of listings of all the movies and tv shows available on Netflix, along with details such as - cast, directors, ratings, release year, duration, etc.

### Types of files and data used in the project are listed below:

| Data Type           | File Type                   | 
|---------------------|-------------------------|
| Netflix Titles      | CSV                     | 
| Netflix Cast        | CSV                     | 
| Netflix Directors   | CSV                     | 
| Netflix Category    | CSV                     | 
| Netflix Countries   | CSV                     | 


 
## tools Used
1. **[Azure Data Lake Storage Gen2 (ADLS)](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)** : to store data.
2. **[Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/introduction)**: Used to automate the ingestion of dimension data from GitHub API into the bronze container.
3. **[Azure Databricks](https://learn.microsoft.com/en-us/azure/databricks/introduction/)**: used for data processing using PySpark and Autoloader for real-time data ingestion.
4. **[Delta Live Tables](https://learn.microsoft.com/en-us/azure/databricks/dlt/)**: Implements the star schema to serve transformed data in a structured format.
