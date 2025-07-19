# CST8917 – Assignment 1  

---

##  Objective  
Build and deploy a serverless pipeline using Azure Durable Functions to extract metadata from uploaded images and save it into an Azure SQL Database.

## YouTube Link: https://youtu.be/OR7ylrUBvbU

##  Project Setup in VS Code  
### 1. Created Durable Function App  
- **Language:** Python  
- **Programming Model:** v2  
- **Triggers:**
  - Blob Trigger: `starter_function`
  - Orchestration Trigger: `orchestrator_function`
  - Activities: `extract_metadata_activity`, `store_metadata_activity`

### 2. Blob Trigger Configuration  
Activates when new images are uploaded to the `images-input` storage container.

### 3. Metadata Extraction  
Used python `Pillow` library to read image metadata.

### 4. SQL Storage  
Inserts extracted metadata into an Azure SQL Database table via `pyodbc`.

---

## Azure Resources
- Azure Blob Storage container: `images-input`  
  - **Table:** `dbo.image_metadata`

### SQL Table Schema  
```sql
CREATE TABLE dbo.image_metadata (
    file_name NVARCHAR(100),
    file_size_kb FLOAT,
    width INT,
    height INT,
    format NVARCHAR(20)
);
```

### Configuration in Azure Portal  
- **Application Settings:**
  - `AzureWebJobsStorage` – Blob connection string  
  - `SQLConnectionString` – SQL connection string

---

##  Local Testing  
1. Start local environment:  
   ```bash
   func start
   ```
2. Upload image to `images-input`.  
3. Functions process images and store metadata in SQL.

---

##  Deployment to Azure  
1. Deploy Function App:  
   ```bash
   func azure functionapp publish <your-app-name>
   ```

2. Upload images via Azure Portal to trigger processing. 
3. Check the Query metadata in SQL:
   ```sql
   SELECT * FROM dbo.image_metadata;
   ```

---



