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

---

## 📊 Architecture Diagram

![Architecture](assets/architecture.png)

---

## 🔄 Data Flow

1. Raw data ingested into Azure Blob Storage
2. ADF copies raw data to a staging zone
3. Databricks cleans and transforms the data
4. Clean data stored in Azure SQL DB or Synapse
5. Power BI connects to SQL/Synapse for reporting

---

## 📁 Folder Structure

| Folder       | Description                             |
|--------------|-----------------------------------------|
| `data/`      | Sample datasets                         |
| `src/`       | Scripts for transformation in Databricks|
| `pipeline/`  | ADF JSON pipeline definitions           |
| `assets/`    | Diagrams and visuals                    |
| `sql/`       | SQL queries for validation or reports   |
| `notebooks/` | Databricks notebooks                    |

---

## 📦 Setup Instructions

1. Clone this repo  
   ```bash
   git clone https://github.com/YOUR_USERNAME/azure-end-to-end-data-pipeline.git
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
