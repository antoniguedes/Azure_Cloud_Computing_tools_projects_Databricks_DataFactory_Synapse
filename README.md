# Azure Cloud Computing Tools Projects: Databricks, Data Factory, Synapse

This repository contains hands-on projects and resources for working with key Azure cloud data tools, including Databricks, Data Factory, and Synapse. It is organized into folders that follow the typical workflow for setting up, developing, and orchestrating data pipelines and dataflows in Azure.

## Repository Structure

- **Azure setup/**
  - Contains instructions and resources for configuring your Azure environment. This includes setting up resource groups, storage accounts, and security prerequisites needed before building data solutions.
- **Databricks/**
  - Resources, notebooks, and guides for working with Azure Databricks. Use this folder to find Databricks-specific setup steps, demonstration notebooks, and integration tips with other Azure tools.
- **Azure dataflow/**
  - Video tutorials, sample dataflows, and documentation for building and managing dataflows within Azure Data Factory. This folder includes:
    - `Azure dataflow 1 - Transformations Join Filter Sink_a.mp4`: Video demonstration showing how to create, join, filter, and sink (write) data in a dataflow.
    - `README.md`: Additional documentation for the dataflow tutorials.
- **Databricks/**
  - Exploration EDA and querying embeded data in JSON files using SQL Spark
---

## Building a Dataflow and Data Pipeline in Azure: Step-by-Step Guide

**1. Azure Setup**
   - Prepare your Azure environment by creating a resource group and storage account.
   - Set up permissions and authentication (e.g., via Azure Active Directory).
   - Deploy Azure Data Factory and/or Databricks workspace as needed.
![Azure setup - creating Blob containers in Azure](https://github.com/user-attachments/assets/1dcac525-5a12-4ba3-852c-613d197e6d91)
[Azure setup - creating Blob containers in Azure]

![Azure setup - creating the SQL database cost](https://github.com/user-attachments/assets/f5432ca7-01ce-4d07-8ec8-d842a13eaa4c)
[Azure setup - creating the SQL database cost]

**2. Creating a Dataflow in Azure Data Factory**
   - **Start a new Dataflow**: In Azure Data Factory, navigate to the Author tab and create a new Dataflow.
   - **Add Source(s)**: Define the datasets you want to ingest (e.g., CSVs from Blob Storage, SQL tables).
   - **Apply Transformations**:
     - **Join**: Combine multiple sources using a join transformation.
     - **Filter**: Use filter transformations to remove unwanted data based on conditions.
     - **Other Transformations**: Aggregate, derive columns, or perform lookups as necessary for your use case.
   - **Configure Sink**: Define where the transformed data should be written (e.g., another Blob Storage container, SQL database).
   - **Debug and Preview**: Use the debug mode to preview data at each step and validate your logic.
![Azure dataflow - Complete Dataflow](https://github.com/user-attachments/assets/6ee1c87b-12f1-4a6c-bded-4b7ccdaecea1)
[Azure dataflow - Complete Dataflow]  
![Azure dataflow - Creating Pipeline of the Dataflow](https://github.com/user-attachments/assets/7e6bc7ff-372f-4471-b102-0708aba616cc)
[Azure dataflow - Creating Pipeline of the Dataflow]  

**3. Creating a Data Pipeline**
   - **Pipeline Creation**: In Data Factory, create a new pipeline.
   - **Add Dataflow Activity**: Drag your dataflow into the pipeline as an activity.
   - **Set up Triggers and Parameters**: Schedule the pipeline or parameterize it for dynamic execution.
   - **Monitor & Manage**: Use Data Factory monitoring tools to track pipeline runs, diagnose errors, and optimize performance.
![Azure pipeline - pipeline Container to SQL database](https://github.com/user-attachments/assets/d043aa77-958c-4965-abe3-f62568c21461)
[Azure pipeline - pipeline Container to SQL database]
![Azure pipeline - creating the SQL database connection in ADStudio](https://github.com/user-attachments/assets/351d5ee1-c875-4c60-97b4-8cbdbcdb2a4a)
[Azure pipeline - creating the SQL database connection in ADStudio]



---

## Getting Started

1. Review the `Azure setup` folder to prepare your Azure environment.
2. Watch the video(s) in `Azure dataflow` for practical demonstrations of building dataflows.
3. Explore the `Databricks` folder for additional advanced analytics and processing scenarios.
4. Combine these components to build robust, end-to-end data solutions in Azure!

---

## Notes

- This repository is intended for educational and demonstration purposes.
- Each folder includes readme files and/or videos to guide you through the specific steps and best practices for that tool or process.
