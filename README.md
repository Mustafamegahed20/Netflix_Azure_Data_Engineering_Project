# Netflix_Azure_Data_Engineering_Project
 ![How-Netflix-Changed-story-telling-Marksmen-Daily](https://github.com/user-attachments/assets/74355d28-b158-45dc-9a1e-7328dafb2e92)
 
# Project Overview
This project is designed to process and analyze Netflix Movies and TV Shows data using Azure Data Factory, Databricks, and Power BI. The pipeline ingests raw data, transforms it, and serves it in a star schema using delta live tables for analytics.

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

## Data Schema

The data is organized into the following tables:

- **Fact Table**:
  - `netflix_titles`: Contains information about Netflix titles.

- **Dimension Tables**:
  - `netflix_cast`: Contains information about the cast members.
  - `netflix_directors`: Contains information about the directors.
  - `netflix_category`: Contains information about the categories of titles.
  - `netflix_countries`: Contains information about the countries associated with titles.

## Tools Used
1. **[Azure Data Lake Storage Gen2 (ADLS)](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)** : to store data.
2. **[Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/introduction)**: used to automate the ingestion of dimension data from GitHub API into the bronze container.
3. **[Azure Databricks](https://learn.microsoft.com/en-us/azure/databricks/introduction/)**: used for data processing using PySpark and Autoloader for real-time data ingestion.
4. **[Delta Live Tables](https://learn.microsoft.com/en-us/azure/databricks/dlt/)**: Implements the star schema to serve transformed data in a structured format.

# Solution Architecture
![Azuresolution (3)](https://github.com/user-attachments/assets/84d7857d-a88d-43da-a700-9124a68e0ff3)

## Key Steps

### **1. Data Ingestion**
- **Fetch Lookup Data**:
  - Use **Azure Data Factory (ADF)** to fetch lookup data (e.g., Netflix cast, directors, categories, and countries) from the **GitHub API**.
  - Load the fetched data into the **Bronze** layer in Azure Data Lake Storage Gen2.
    
![Screenshot 2025-03-19 190125](https://github.com/user-attachments/assets/be582ccc-1186-4962-b4ff-bc3ac97cfbaa)

- **Ingest Fact Table**:
  - Manually upload the **Netflix Titles** fact table (e.g., CSV ) to the **Raw** layer.
  - Use **Databricks Autoloader** to stream the fact table data from the **Raw** layer to the **Bronze** layer.
    
![image](https://github.com/user-attachments/assets/721779ec-ef49-42db-ad0e-fb95341ccb2b)

---

### **2. Data Transformation**
- **Transform Lookup Data**:
  - Use **Databricks Workflows** to load lookup data from the **Bronze** layer.
  - Perform transformations (e.g., data cleansing, deduplication, and enrichment) using **PySpark**.
  - Load the transformed lookup data into the **Silver** layer.

![image](https://github.com/user-attachments/assets/3f2ae96f-8701-4399-8fe1-c12baf1e0159)

- **Transform Fact Table**:
  - Use **Databricks Workflows** to load the **Netflix Titles** fact table from the **Bronze** layer.
  - Perform transformations using **PySpark**.
  - Load the transformed fact table into the **Silver** layer.

![image](https://github.com/user-attachments/assets/56d0b59c-8834-4ba4-9615-7919ea3280fc)

---

### **3. Data Serving**
- **Create Star Schema**:
  - Use **Delta Live Tables (DLT)** to combine the transformed fact table and lookup data from the **Silver** layer.
  - Create a **star schema** in the **Gold** layer.
  - Ensure data quality and consistency using DLT's built-in features (e.g., schema enforcement, data lineage, and automatic scaling).
    
![Screenshot 2025-03-15 150149](https://github.com/user-attachments/assets/de5bd3d1-42d8-4087-97fc-aab26d2492a7)

---

### **4. Data Visualization**
- **Connect to Power BI**:
  - Connect **Power BI** to the **Gold** layer to visualize the star schema data.
  - Create dashboards and reports to analyze Netflix Movies and TV Shows data .

---

### **5. Data Governance**
- **Implement Unity Catalog**:
  - Use **Unity Catalog** to manage and govern data across all layers (Raw, Bronze, Silver, Gold).
  - Define access controls, data lineage, and metadata for all datasets.
 
