# Student Information Migration & Reporting Suite (SSIS & SSRS)

This repository contains the backend SQL Server Business Intelligence (BI) suite for the **Student Information Database**. It features a robust ETL pipeline (SSIS) to migrate student records between databases and a polished reporting layout (SSRS) for viewing active student records.

Originally developed under a generic customer-centric layout, this suite has been fully refactored and upgraded to a custom student information database model.

---

## 🗄️ Database Schema & Architecture

The suite operates across two databases (`Mydata` as the source, and `StudenData` as the destination) with the following structure:

### Table: `dbo.Student`
| Column Name | Data Type | Key/Constraint | Description |
| :--- | :--- | :--- | :--- |
| **`Id`** | `INT` | Primary Key | Unique student identifier |
| **`Name`** | `NVARCHAR(50)` | Nullable | Full name of the student |
| **`Age`** | `INT` | Nullable | Student's current age |
| **`Session`** | `NVARCHAR(50)` | Nullable | Academic enrollment session (e.g. `2025-26`) |
| **`Groupe`** | `NVARCHAR(50)` | Nullable | Academic group name |
| **`Section`** | `NVARCHAR(50)` | Nullable | Assigned classroom/cohort section |

### Database Setup Scripts
Ensure your SQL Server instance has the following tables created before running the SSIS migration or SSRS reports:

```sql
-- Create Source Database & Table
CREATE DATABASE Mydata;
GO
USE Mydata;
GO
CREATE TABLE dbo.Student (
    Id INT PRIMARY KEY,
    Name NVARCHAR(50),
    Age INT,
    Session NVARCHAR(50),
    Groupe NVARCHAR(50),
    Section NVARCHAR(50)
);
GO

-- Create Destination Database & Table
CREATE DATABASE StudenData;
GO
USE StudenData;
GO
CREATE TABLE dbo.Student (
    Id INT PRIMARY KEY,
    Name NVARCHAR(50),
    Age INT,
    Session NVARCHAR(50),
    Groupe NVARCHAR(50),
    Section NVARCHAR(50)
);
GO
```

---

## 🚀 Projects & Subsystems

### 1. Integration Services (ETL) Project
*   **Path**: `[Student Integration Project/](file:///e:/EDGE/ProjectsI036(Back_End)/Student%20Integration%20Project)`
*   **Solution**: `Student Integration Project.sln`
*   **ETL Package**: `StudentMigration.dtsx`
*   **Description**: Implements a high-performance ADO.NET data pipeline to copy student details from `Mydata` database to `StudenData` database, remapping the 6 active student data fields accurately.

### 2. Reporting Services Project
*   **Path**: `[Student Report Project/](file:///e:/EDGE/ProjectsI036(Back_End)/Student%20Report%20Project)`
*   **Solution**: `Student Report Project.sln`
*   **Report Shared Datasource**: `StudentDS.rds` (Points to `Mydata` database)
*   **Report Definition**: `StudentList.rdl`
*   **Description**: A 6-column professional reporting layout displaying a table of all students. Styled with matching grid alignments, font sizes, and color themes.

---

## 🛠️ Verification & Execution Guide

### How to Run in Visual Studio (SSDT):
1.  **Open Solutions**:
    *   To run the ETL pipeline, open `Student Integration Project.sln`.
    *   To edit or render reports, open `Student Report Project.sln`.
2.  **Execute the SSIS Migration Package**:
    *   Right-click `StudentMigration.dtsx` inside the Solution Explorer and select **Execute Package** to trigger the data migration.
3.  **Preview/Deploy SSRS Reports**:
    *   Open `StudentList.rdl`, navigate to the **Preview** tab to check the report visual, and use the **Deploy** command to publish it to your Reporting Server.
