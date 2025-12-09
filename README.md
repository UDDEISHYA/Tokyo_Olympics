# Tokyo Olympics 2020 Data Engineering Project
<p align="center">
  <a href="" rel="noopener">
 <img width=800px height=600px src="https://media.telanganatoday.com/wp-content/uploads/2021/07/All-you-need-to-know-about-Tokyo-Olympics-2020.jpg" alt="Project logo"></a>
</p>


<div align="center">

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=for-the-badge&logo=apache-spark&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

**An end-to-end cloud-based data engineering pipeline built on Microsoft Azure**

[Features](#-features) • [Architecture](#-architecture-overview) • [Installation](#-setting-up-the-environment) • [Usage](#-usage) • [Contributing](#-contributing)

</div>

---

## 📋 Table of Contents

- [Problem Statement](#-problem-statement)
- [Idea / Solution](#-idea--solution)
- [Architecture Overview](#-architecture-overview)
- [Technology Stack](#-technology-stack)
- [Dependencies / Limitations](#-dependencies--limitations)
- [Prerequisites](#-prerequisites)
- [Setting up the Environment](#-setting-up-the-environment)
- [Implementation Guide](#-implementation-guide)
- [Usage](#-usage)
- [Data Schema](#-data-schema)
- [Future Scope](#-future-scope)
- [Contributing](#-contributing)
- [Acknowledgments](#-acknowledgments)

---

## 🎯 Problem Statement

Organizations often struggle with processing and analyzing large-scale event data stored across distributed sources. The Tokyo Olympics 2021 dataset, containing information about 11,000+ athletes, 47 disciplines, and 743 teams, presents several challenges:

- **Data Accessibility**: Raw data scattered across multiple CSV files in external repositories
- **Scalability**: Need for cloud-based infrastructure to handle large-scale data processing
- **Transformation Complexity**: Requirement for robust ETL pipelines to clean and transform raw data
- **Analytics Readiness**: Data must be structured and optimized for analytical queries and visualization
- **Integration**: Seamless connection between ingestion, transformation, and analytics layers

---

## 💡 Solution

This project implements a **comprehensive Azure-based data engineering solution** that addresses the challenges through a modern cloud-native architecture:

### Core Solution Components


|                                                                                                                         |                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
|  1. **Automated Data Ingestion**<br>- Leverages Azure Data Factory to extract data from HTTP endpoints (GitHub repository)<br>- Implements parameterized pipelines for multiple CSV files<br>- Stores raw data in Azure Data Lake Storage Gen2 with hierarchical namespace | 2. **Scalable Data Transformation**<br>- Utilizes Azure Databricks with Apache Spark for distributed data processing<br>- Implements schema validation and type casting<br>- Performs data quality checks and basic transformations<br>- Supports both batch processing and iterative development |
| 3. **Analytics-Ready Data Storage**<br>- Maintains separate layers for raw and transformed data (Data Lake architecture)<br>- Enables version control and data lineage tracking<br>- Optimizes data formats for query performance | 4. **SQL-Based Analytics**<br>- Integrates Azure Synapse Analytics for ad-hoc querying<br>- Provides foundation for building dashboards and visualizations<br>- Supports complex analytical queries on transformed datasets |


---

## 🏗️ Architecture Overview
```
┌─────────────────┐
│   Data Source   │
│  (GitHub API)   │
└────────┬────────┘
         │
         ▼
┌─────────────────────────┐
│  Azure Data Factory     │
│  (Ingestion Pipeline)   │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────────────┐
│  Azure Data Lake Storage Gen2   │
│  ┌─────────────────────────┐    │
│  │     Raw Data Layer      │    │
│  └───────────┬─────────────┘    │
│              │                   │
│              ▼                   │
│  ┌─────────────────────────┐    │
│  │   Azure Databricks      │    │
│  │   (Spark Transformation)│    │
│  └───────────┬─────────────┘    │
│              │                   │
│              ▼                   │
│  ┌─────────────────────────┐    │
│  │  Transformed Data Layer │    │
│  └───────────┬─────────────┘    │
└──────────────┼─────────────────┘
               │
               ▼
┌─────────────────────────┐
│  Azure Synapse Analytics│
│  (SQL Analytics)        │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│  Visualization Layer    │
│  (Power BI/Tableau)     │
└─────────────────────────┘
```

### Data Flow

1. **Extraction**: Azure Data Factory connects to GitHub repository via HTTP
2. **Raw Storage**: Data loaded as-is into ADLS Gen2 raw data container
3. **Transformation**: Databricks notebook reads raw data, applies Spark transformations
4. **Processed Storage**: Cleaned data written back to ADLS Gen2 transformed data container
5. **Analytics**: Synapse Analytics queries transformed data for insights
6. **Visualization**: Results consumed by BI tools for dashboard creation

---

## 🛠️ Technology Stack

### Cloud Platform
- **Microsoft Azure** - Primary cloud infrastructure provider

### Core Services

| Service | Purpose | Version/SKU |
|---------|---------|-------------|
| **Azure Data Factory** | ETL/ELT orchestration and data pipeline management | Standard |
| **Azure Data Lake Storage Gen2** | Hierarchical data lake with blob storage capabilities | Standard LRS |
| **Azure Databricks** | Apache Spark-based analytics platform | Premium |
| **Azure Synapse Analytics** | Cloud data warehouse and analytics service | Standard |

### Programming & Frameworks

| Technology | Purpose |
|------------|---------|
| **Python 3.x** | Primary programming language for transformations |
| **PySpark** | Distributed data processing framework |
| **SQL** | Data querying and analysis |

### Data Formats
- **CSV** - Input/output file format

---

## ⚠️ Dependencies / Limitations

### Technical Dependencies

#### 1. **Azure Account Requirements**
- Active Azure subscription (Free trial provides $200 credit for 30 days)
- Valid payment method for account verification
- Access to Azure Portal

#### 2. **Service Quotas**
- Regional resource availability may vary
- Default quota limits on compute resources
- Storage account limits (500 TB default)

#### 3. **Network Requirements**
- Stable internet connection for cloud operations
- Access to GitHub API endpoints
- HTTPS connectivity for Azure services

### Known Limitations

#### 1. **Cost Considerations**
- Databricks compute clusters incur charges when running
- Data Lake storage costs scale with data volume
- Data transfer charges for egress traffic
- Synapse Analytics has per-query or provisioned capacity costs

#### 2. **Performance Constraints**
- Single-node Databricks cluster limits processing speed
- HTTP-based data ingestion may be slower than native integrations
- CSV format less efficient than columnar formats (Parquet/ORC)

#### 3. **Security Limitations**
- Credentials stored in code (not production-ready)
- No Azure Key Vault integration in base implementation
- Anonymous authentication for GitHub repository

#### 4. **Scalability Boundaries**
- Manual pipeline creation for each data source
- Limited error handling and retry logic
- No automated schema evolution handling

#### 5. **Data Quality**
- Basic validation only (schema casting, null handling)
- No comprehensive data quality frameworks
- Limited data profiling capabilities

### Regional Restrictions
- Some Azure services may not be available in all regions
- Compliance requirements may restrict data residency

---

## Setting up the Environment

### Step 1: Configure Azure Storage

#### 1.1 Create Storage Account
```bash
# Navigate to Azure Portal → Storage Accounts → Create
```

**Configuration:**
- **Subscription**: Free Trial
- **Resource Group**: `tokyo-olympic-rg` (create new)
- **Storage Account Name**: `tokyoolympicdata` (must be globally unique)
- **Region**: Select nearest region (e.g., `Southeast Asia`)
- **Performance**: Standard
- **Redundancy**: LRS (Locally Redundant Storage)

**Advanced Settings:**
- ✅ Enable hierarchical namespace (critical for Data Lake Gen2)

#### 1.2 Create Container and Folder Structure
```
Container: tokyo-olympic-data
├── raw-data/           # Stores original ingested data
└── transform-data/     # Stores processed data
```

**Steps:**
1. Navigate to Storage Account → Containers
2. Click "+ Container"
3. Name: `tokyo-olympic-data`
4. Create folders: `raw-data` and `transform-data`

---

### Step 2: Setup Azure Data Factory

#### 2.1 Create Data Factory Instance
```bash
# Azure Portal → Data Factory → Create
```

**Configuration:**
- **Resource Group**: `tokyo-olympic-rg`
- **Name**: `tokyo-olympic-df`
- **Region**: Same as storage account
- **Version**: V2

#### 2.2 Launch Data Factory Studio

1. Click "Launch Studio" from Data Factory overview
2. Navigate to **Author** tab (pencil icon)

---

### Step 3: Configure Azure Databricks

#### 3.1 Create Databricks Workspace
```bash
# Azure Portal → Azure Databricks → Create
```

**Configuration:**
- **Resource Group**: `tokyo-olympic-rg`
- **Workspace Name**: `tokyo-olympic-db`
- **Region**: Same as previous resources
- **Pricing Tier**: Premium (for full features)

#### 3.2 Create Compute Cluster

1. Launch Databricks workspace
2. Navigate to **Compute** → Create Compute
3. **Configuration**:
   - **Cluster Mode**: Single Node
   - **Databricks Runtime**: 11.3 LTS (or latest LTS)
   - **Node Type**: Standard_DS3_v2 (4 cores, 14GB RAM)
   - **Terminate after**: 30 minutes of inactivity

---

### Step 4: Setup App Registration (for Databricks-ADLS Authentication)

#### 4.1 Register Application
```bash
# Azure Portal → App Registrations → New Registration
```

**Configuration:**
- **Name**: `databricks-app-01`
- **Supported Account Types**: Single tenant
- **Redirect URI**: Leave blank

**Collect Credentials** (save these securely):
```
Application (client) ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
Directory (tenant) ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

#### 4.2 Create Client Secret

1. Navigate to **Certificates & Secrets**
2. Click **New Client Secret**
3. **Description**: `secret-key`
4. **Expires**: 24 months
5. **Copy the Value** (not Secret ID) - save immediately, it won't be shown again
```
Secret Value: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

#### 4.3 Assign Storage Permissions
```bash
# Storage Account → Access Control (IAM) → Add Role Assignment
```

- **Role**: Storage Blob Data Contributor
- **Assign Access To**: User, group, or service principal
- **Members**: Select `databricks-app-01`
- **Review + Assign**

---

### Step 5: Environment Variables Setup

Create a configuration file (for reference, not executed):
```python
# databricks_config.py
configs = {
    "fs.azure.account.auth.type": "OAuth",
    "fs.azure.account.oauth.provider.type": 
        "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
    "fs.azure.account.oauth2.client.id": "<APPLICATION_CLIENT_ID>",
    "fs.azure.account.oauth2.client.secret": "<CLIENT_SECRET_VALUE>",
    "fs.azure.account.oauth2.client.endpoint": 
        "https://login.microsoftonline.com/<TENANT_ID>/oauth2/token"
}

# Mount Configuration
STORAGE_ACCOUNT_NAME = "tokyoolympicdata"
CONTAINER_NAME = "tokyo-olympic-data"
MOUNT_POINT = "/mnt/tokyoolympic"
```

---

## 📘 Implementation Guide

### Phase 1: Data Ingestion Pipeline

#### 1.1 Create Linked Services

**For Source (GitHub HTTP)**:

1. In Data Factory Studio → Manage → Linked Services → New
2. Select **HTTP** connector
3. Configuration:
```
   Name: athletes_http
   Base URL: https://raw.githubusercontent.com/<your-repo>/athletes.csv
   Authentication Type: Anonymous
```

**For Sink (Azure Data Lake Gen2)**:

1. New Linked Service → Azure Data Lake Storage Gen2
2. Configuration:
```
   Name: adls_gen2
   Authentication: Account Key
   Storage Account: tokyoolympicdata
```

#### 1.2 Build Copy Pipeline

Create pipeline for each dataset:
```
Pipeline: data-ingestion
├── Copy_Athletes
├── Copy_Coaches
├── Copy_EntriesGender
├── Copy_Medals
└── Copy_Teams
```

**Copy Activity Configuration** (example for Athletes):
- **Source**:
  - Dataset: CSV from HTTP (athletes.csv)
  - First row as header: ✅
- **Sink**:
  - Dataset: ADLS Gen2 CSV
  - File path: `tokyo-olympic-data/raw-data/athletes.csv`
  - Copy method: Sequential

**Pipeline Execution**:
1. Click **Debug** to test
2. Monitor execution in **Monitor** tab
3. Verify files in Storage Account

---

### Phase 2: Data Transformation (Databricks)

#### 2.1 Mount ADLS to Databricks

Create new notebook: `tokyo-olympic-transformation`
```python
# Cell 1: Import required libraries
from pyspark.sql.functions import col
from pyspark.sql.types import IntegerType, StringType

# Cell 2: Configure ADLS Gen2 connection
configs = {
    "fs.azure.account.auth.type": "OAuth",
    "fs.azure.account.oauth.provider.type": 
        "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
    "fs.azure.account.oauth2.client.id": "<YOUR_CLIENT_ID>",
    "fs.azure.account.oauth2.client.secret": "<YOUR_CLIENT_SECRET>",
    "fs.azure.account.oauth2.client.endpoint": 
        "https://login.microsoftonline.com/<YOUR_TENANT_ID>/oauth2/token"
}

# Cell 3: Mount ADLS container
dbutils.fs.mount(
    source = "abfss://tokyo-olympic-data@tokyoolympicdata.dfs.core.windows.net/",
    mount_point = "/mnt/tokyoolympic",
    extra_configs = configs
)

# Cell 4: Verify mount
display(dbutils.fs.ls("/mnt/tokyoolympic/raw-data"))
```

#### 2.2 Read Raw Data
```python
# Read all datasets
athletes = spark.read.format("csv") \
    .option("header", "true") \
    .load("/mnt/tokyoolympic/raw-data/athletes.csv")

coaches = spark.read.format("csv") \
    .option("header", "true") \
    .load("/mnt/tokyoolympic/raw-data/coaches.csv")

entries_gender = spark.read.format("csv") \
    .option("header", "true") \
    .option("inferSchema", "true") \
    .load("/mnt/tokyoolympic/raw-data/entriesgender.csv")

medals = spark.read.format("csv") \
    .option("header", "true") \
    .option("inferSchema", "true") \
    .load("/mnt/tokyoolympic/raw-data/medals.csv")

teams = spark.read.format("csv") \
    .option("header", "true") \
    .load("/mnt/tokyoolympic/raw-data/teams.csv")
```

#### 2.3 Apply Transformations

**Schema Validation and Type Casting**:
```python
# Validate and display schemas
athletes.printSchema()
coaches.printSchema()

# Transform entries_gender: Cast numeric columns
entries_gender = entries_gender \
    .withColumn("Female", col("Female").cast(IntegerType())) \
    .withColumn("Male", col("Male").cast(IntegerType())) \
    .withColumn("Total", col("Total").cast(IntegerType()))

# Verify transformation
entries_gender.printSchema()
entries_gender.show(5)
```

**Sample Analytics**:
```python
# Top countries by gold medals
top_gold_countries = medals \
    .select("Team_Country", "Gold") \
    .orderBy(col("Gold").desc())

top_gold_countries.show(10)

# Calculate average entries by gender
from pyspark.sql.functions import col

entries_with_avg = entries_gender \
    .withColumn("Avg_Female", col("Female") / col("Total")) \
    .withColumn("Avg_Male", col("Male") / col("Total"))

entries_with_avg.show(10)
```

#### 2.4 Write Transformed Data
```python
# Write to transformed data layer
athletes.repartition(1).write \
    .mode("overwrite") \
    .option("header", "true") \
    .csv("/mnt/tokyoolympic/transform-data/athletes")

coaches.repartition(1).write \
    .mode("overwrite") \
    .option("header", "true") \
    .csv("/mnt/tokyoolympic/transform-data/coaches")

entries_gender.repartition(1).write \
    .mode("overwrite") \
    .option("header", "true") \
    .csv("/mnt/tokyoolympic/transform-data/entriesgender")

medals.repartition(1).write \
    .mode("overwrite") \
    .option("header", "true") \
    .csv("/mnt/tokyoolympic/transform-data/medals")

teams.repartition(1).write \
    .mode("overwrite") \
    .option("header", "true") \
    .csv("/mnt/tokyoolympic/transform-data/teams")
```

---

### Phase 3: Analytics Setup (Synapse Analytics)

#### 3.1 Create Synapse Workspace
```bash
# Azure Portal → Azure Synapse Analytics → Create
```

**Configuration:**
- **Resource Group**: `tokyo-olympic-rg`
- **Workspace Name**: `tokyo-olympic-synapse`
- **Region**: Same as other resources
- **Data Lake Storage**: Select existing `tokyoolympicdata`

#### 3.2 Query Transformed Data

1. Launch Synapse Studio
2. Navigate to **Data** → Linked → Azure Data Lake Storage Gen2
3. Browse to `transform-data` folder
4. Right-click on dataset → **New SQL Script** → **Select TOP 100**

**Sample Analytical Queries**:
```sql
-- Query 1: Top 10 countries by total medals
SELECT 
    Team_Country,
    Gold,
    Silver,
    Bronze,
    Total,
    Rank_by_Total
FROM medals
ORDER BY Total DESC
LIMIT 10;

-- Query 2: Gender distribution by discipline
SELECT 
    Discipline,
    Female,
    Male,
    Total,
    ROUND((Female * 100.0 / Total), 2) AS Female_Percentage
FROM entriesgender
ORDER BY Total DESC;

-- Query 3: Athlete count by country
SELECT 
    Country,
    COUNT(*) AS Athlete_Count
FROM athletes
GROUP BY Country
ORDER BY Athlete_Count DESC;
```

---

## 📖 Usage

### Running the Complete Pipeline

#### 1. **Data Ingestion** (Azure Data Factory)
```bash
1. Open Azure Data Factory Studio
2. Navigate to Author → Pipelines → data-ingestion
3. Click "Debug" or "Add Trigger" → "Trigger Now"
4. Monitor execution in Monitor tab
5. Verify files in ADLS raw-data folder
```

**Expected Output**: 5 CSV files in `raw-data/` folder

#### 2. **Data Transformation** (Databricks)
```bash
1. Open Databricks Workspace
2. Navigate to Workspace → Notebooks
3. Open tokyo-olympic-transformation notebook
4. Attach cluster (start if stopped)
5. Run all cells (Cell → Run All)
6. Verify output in ADLS transform-data folder
```

**Expected Output**: 5 processed datasets in `transform-data/` folder

#### 3. **Analytics** (Synapse Analytics)
```bash
1. Open Synapse Studio
2. Navigate to Develop → SQL Scripts
3. Create new script or open existing
4. Connect to built-in serverless pool
5. Execute analytical queries
6. Export results or build visualizations
```

---

### Monitoring and Troubleshooting

#### Data Factory Pipeline Monitoring
```
Location: Data Factory Studio → Monitor
Check:
- Pipeline run status
- Activity-level details
- Error messages and logs
- Duration and throughput
```

#### Databricks Job Monitoring
```
Location: Databricks → Clusters → Event Log
Check:
- Cluster startup time
- Cell execution duration
- Spark UI for job details
- Driver and executor logs
```

#### Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| **Mount fails in Databricks** | Incorrect credentials or permissions | Verify App Registration credentials; Check Storage IAM roles |
| **Pipeline copy activity fails** | Network/firewall issues | Check NSG rules; Verify linked service connections |
| **Schema mismatch errors** | Data type inconsistencies | Use `inferSchema` option; Explicit type casting |
| **Out of memory errors** | Insufficient cluster resources | Increase cluster size; Optimize partitioning |
| **Access denied errors** | Missing RBAC permissions | Grant appropriate roles in IAM |

---

## 📊 Data Schema

### Athletes Dataset
```
PersonName: String - Name of the athlete
Country: String - Country representation
Discipline: String - Sport discipline
```

### Coaches Dataset
```
Name: String - Coach name
Country: String - Country of coach
Discipline: String - Sport discipline
Event: String - Specific event
```

### Entries Gender Dataset
```
Discipline: String - Sport discipline
Female: Integer - Number of female participants
Male: Integer - Number of male participants
Total: Integer - Total participants
```

### Medals Dataset
```
Rank: Integer - Country ranking
Team_Country: String - Country name
Gold: Integer - Gold medals count
Silver: Integer - Silver medals count
Bronze: Integer - Bronze medals count
Total: Integer - Total medals
Rank_by_Total: Integer - Ranking by total medals
```

### Teams Dataset
```
TeamName: String - Name of the team
Discipline: String - Sport discipline
Country: String - Country representation
Event: String - Specific event
```

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
