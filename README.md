# Azure End-to-End Data Engineering Project 🚀

This project demonstrates an end-to-end Azure data pipeline using various Azure services. It covers data ingestion, transformation, storage, and visualization.

---

## 🧠 Tech Stack

- **Azure Data Factory**
- **Azure Blob Storage**
- **Azure SQL Database**
- **Azure Databricks (PySpark)**
- **Azure Synapse Analytics**
- **Power BI**
- **Azure Key Vault**

## Architecture
The project follows the **Medallion Architecture**, which organizes data into three distinct layers to maintain quality, scalability, and accessibility:

Bronze (Raw) Layer
Purpose: To store raw data exactly as received from the source, without any transformations.

Source: GitHub APIs

Tools Used: Azure Data Factory

Silver (Transformed) Layer
Purpose: To clean, transform, and enrich the raw data, making it suitable for analytical use.

Tools Used: Azure Databricks

Gold (Serving) Layer
Purpose: To deliver refined, analysis-ready data to stakeholders through a data warehouse.

Tools Used: Azure Synapse Analytics, Power BI


## Prerequisites
Azure Account: An active Azure subscription. Create a free Azure account if you don't have one.
GitHub Account: To access and interact with GitHub APIs.
Basic Knowledge: Familiarity with Azure services, SQL, Spark, and data engineering concepts.


## Setup Instructions


1. Create an Azure Data Factory Instance
Navigate to Azure Portal:

Log in to the Azure Portal.
Create Data Factory:

Click on "Create a resource".
Search for "Data Factory" and select it.
Click "Create" and fill in the required details:
Subscription: Choose your Azure subscription.
Resource Group: Create a new resource group or select an existing one.
Name: Enter a unique name (e.g., ADF-Project-YourName).
Region: Select your preferred region.
Click "Review + create" and then "Create".


2. Set Up Azure Data Lake Storage Gen2
Create Storage Account:

In the Azure Portal, click on "Create a resource".
Search for "Storage account" and select it.
Click "Create" and fill in the details:
Subscription: Your Azure subscription.
Resource Group: Same as Data Factory.
Storage account name: Unique name (e.g., datalakeyourname).
Performance: Standard.
Account kind: StorageV2 (general-purpose v2).
Replication: Locally-redundant storage (LRS) or as per your preference.
Data Lake Storage Gen2: Enable hierarchical namespace.
Click "Review + create" and then "Create".
Create Containers:

Navigate to your storage account.
Under "Data storage", click on "Containers".
Create three containers named:
bronze
silver
gold


3. Configure Linked Services in Azure Data Factory
Access ADF Studio:

Navigate to your Data Factory instance.
Click on "Launch Studio" to open Azure Data Factory Studio.
Create Linked Services:

Go to the "Manage" tab.
Under "Connections", select "Linked services".
Click "+ New" and create the following linked services:
HTTP Linked Service:
Connector: HTTP
Name: HTTP_LinkedService
Base URL: https://raw.githubusercontent.com/YourGitHubUsername/YourRepoName/main/
Authentication Type: Anonymous
Test Connection and Create.
Azure Data Lake Storage Gen2 Linked Service:
Connector: Azure Data Lake Storage Gen2
Name: ADLS_LinkedService
Storage Account Name: Select your storage account.
Test Connection and Create.


4. Create Datasets
Source Dataset (HTTP):

Go to the "Author" tab.
Under "Datasets", click "+ New".
Select "HTTP" as the data source.
Name: DS_HTTP
Linked Service: HTTP_LinkedService
File Format: DelimitedText (CSV)
Relative URL: Leave blank for parameterization.
Schema: Import schema from a sample file if available.
Parameters: Add a parameter for relativeURL.
Dynamic Content: Use the relativeURL parameter in the dataset.
Sink Dataset (ADLS Gen2):

Click "+ New" under "Datasets".
Select "Azure Data Lake Storage Gen2".
Name: DS_ADLS
Linked Service: ADLS_LinkedService
File Format: DelimitedText (CSV)
Folder Path: Parameterized for Bronze, Silver, and Gold layers.
Parameters: Add parameters for folderPath and fileName.
Dynamic Content: Use the parameters in the dataset.


5. Build Pipelines
Static Pipeline (Initial Setup):

Under "Pipelines", click "+ New pipeline".
Name: CopyRawData
Activities:
Copy Activity:
Name: Copy_Raw_Data
Source: DS_HTTP with the specific relativeURL.
Sink: DS_ADLS pointing to the bronze container.
Debug and Publish: Test the pipeline and publish your changes.
Dynamic Pipeline:

Name: Dynamic_Copy_Pipeline
Parameters: Add parameters for file names and paths.
Activities:
ForEach Activity:
Items: Array of file names (e.g., ["products.csv", "customers.csv"]).
Inside ForEach:
Copy Activity: Use parameters to dynamically set relativeURL and sink paths.
Debug and Publish: Test the dynamic pipeline with multiple files.
6. Transform Data with Azure Databricks


Create Databricks Workspace:

In the Azure Portal, create an Azure Databricks workspace.
Launch the workspace and create a new cluster.
Develop Transformation Scripts:

Import data from the silver layer.
Perform data cleaning, enrichment, and transformations using Spark.
Write transformed data to the gold layer.


7. Set Up Azure Synapse Analytics
Create Synapse Workspace:

In the Azure Portal, create an Azure Synapse Analytics workspace.
Set up necessary SQL pools.
Ingest Data:

Load transformed data from the gold layer into Synapse.
Create necessary tables and views for analysis.


8. Integrate with Power BI
Connect Synapse to Power BI:

Open Power BI Desktop.
Connect to Azure Synapse Analytics.
Import data and create interactive dashboards.
Publish Dashboards:

Publish your Power BI reports to the Power BI service for sharing with stakeholders.
---

## 🔄 Data Flow

1. Raw data ingested into Azure Blob Storage
2. ADF copies raw data to a staging zone
3. Databricks cleans and transforms the data
4. Clean data stored in Azure SQL DB or Synapse
5. Power BI connects to SQL/Synapse for reporting

![image](https://github.com/user-attachments/assets/cb44d301-e05e-4375-acf7-4c2176a8bce7)

---

## 📦 Setup Instructions

1. Clone this repo  
   ```bash
   git clone https://github.com/sriPravallika0110/azure-end-to-end-data-pipeline.git
   ```

2. Upload data to Azure Blob Storage

3. Import ADF pipeline JSON

4. Upload notebooks to Databricks

5. Run the pipeline and validate data

---

## 📈 Output Example

- ✅ Transformed CSV files
- ✅ Processed tables in Synapse
- ✅ Interactive Power BI reports

---
