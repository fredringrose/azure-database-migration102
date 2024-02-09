# Microsoft Azure Database Migration

## Introduction

This project involves the architecture and implementation of a cloud-based database system using Microsoft Azure. It demonstrates expertise in cloud engineering, focusing on establishing a production environment, migrating to Azure SQL Database, and addressing key aspects such as data backup, restoration, automated scheduling, disaster recovery, geo-replication, failover configuration, and security through Microsoft Entra ID integration.

## Objectives

- **Establish a Production Environment**: Set up a Windows Virtual Machine (VM) on Microsoft Azure to replicate an on-premise Windows server functionality. This VM is crucial for creating a secure and dedicated data storage solution.
- **Database Migration and Management**: Migrate an existing database to Azure SQL Database, ensuring data integrity through backup and restoration processes. Implement automated scheduling for efficient data management.
- **Disaster Recovery Simulation**: Test the system's resilience by simulating a disaster recovery scenario, focusing on data loss prevention and recovery strategies.
- **Geo-Replication and Failover Configuration**: Enhance data availability across geographical locations through geo-replication. Configure failover mechanisms to maintain service continuity under adverse conditions.
- **Security Enhancement**: Utilize Microsoft Entra ID for access role definition, adding an extra layer of security and access control.

## Section 1: Production Environment Setup

- **VM Configuration**: Deploy a Windows Virtual Machine (VM) on Microsoft Azure, using Windows 11 Pro. Configure the VM with port 3389 for inbound rules to enable Remote Desktop Protocol (RDP) access.
- **Network Configuration**: Apply appropriate network settings and firewall rules to establish a secure connection to the VM via the RDP protocol.
- **Database Tools Installation**: Install SQL Server and SQL Server Management Studio (SSMS) on the VM for database management.
- **Production Database Creation**: Restore the AdventureWorks database from the .bak backup file provided using SSMS. This database serves as a comprehensive sample representing a fictional manufacturing company, providing a rich dataset for various operations.
Upon successful restoration, the database is available for use or further data retrieval. Under Object Explorer pane, all of the tables in the database are now listed. 


This document outlines the process of migrating an on-premise database to Azure SQL Database. This transition involves moving both the schema and data to Azure's cloud ecosystem, ensuring a seamless migration while maintaining data integrity and system functionality.

## Section 2: Migration Process

This section outlines the process of migrating an on-premise database to Azure SQL Database. This transition involves moving both the schema and data to Azure's cloud ecosystem, ensuring a seamless migration while maintaining data integrity and system functionality.

### Step 1: Creation of Azure SQL Database

- **Objective**: Establish an Azure SQL Database instance to serve as the target for the database migration.
- **Action**: In the Azure portal, create a new Azure SQL Database, configuring it according to the required performance and storage specifications.

### Step 2: Configuration of Azure Data Studio

- **Objective**: Install and configure Azure Data Studio on the production Windows VM.
- **Action**: Download and install Azure Data Studio on the VM. Configure it to connect to the existing on-premise database, ensuring connectivity and access.

### Step 3: Establishing Database Connections

- **Objective**: Create a connection to the Azure SQL Database.
- **Action**: Using Azure Data Studio, establish a connection to both the on-premise database and the Azure SQL Database. This sets the stage for schema and data migration activities.

### Step 4: Schema Migration

- **Objective**: Migrate the database schema from the on-premise database to Azure SQL Database.
- **Action**:
  1. Install the SQL Server Schema Compare extension in Azure Data Studio.
  2. Use the extension to compare the schemas of the two databases.
  3. Execute the schema migration, adjusting as necessary to ensure compatibility and integrity.

### Step 5: Data Migration

- **Objective**: Transfer data from the on-premise database to Azure SQL Database.
- **Action**:
  1. Install the Azure SQL Migration extension in Azure Data Studio.
  2. Use the extension to facilitate the data migration process, ensuring a complete and accurate transfer of all database content.

### Step 6: Validation of Migration Process

- **Objective**: Confirm the success of the migration process.
- **Action**: Conduct a thorough validation of the migrated database. This includes checking the schema, data, and configurations to ensure everything has been transferred correctly and functions as expected.


Following these steps will lead to a successful migration of an on-premise database to Azure SQL Database. It is crucial to perform a detailed validation post-migration to guarantee the integrity and functionality of the database in its new cloud environment.

https://colab.research.google.com/github/AI-Core/Content-Public/blob/main/Content/units/Cloud-and-DevOps/11.%20Azure%20Essentials/6.%20Azure%20SQL%20Database/Notebook.ipynb#scrollTo=LtP2qQx-xKJZ


https://colab.research.google.com/github/AI-Core/Content-Public/blob/main/Content/units/Cloud-and-DevOps/11.%20Azure%20Essentials/9.%20Azure%20Data%20Studio%20and%20Database%20Migration/Notebook.ipynb


## Section 3: Data Backup and Restore 

Maintaining frequent and regular backups of your Azure SQL Database is essential for data security. This section discusses the significance of implementing a structured backup schedule to protect your organization's critical data effectively.

### 3.1 Backup the On-Premise Database

The first step was to create a complete backup of the production database located on the Windows Virtual Machine. This backup acts as a comprehensive duplicate of the database, serving as a precautionary measure against potential unexpected problems.

1. **Initial Backup Creation**:
   - The journey begins with the generation of a full backup of the production database on the Windows VM. This crucial step duplicates the database, establishing a safety net for unforeseen issues.

2. **Local Backup Storage**:
   - Upon successful backup creation, the file is stored in a predetermined local directory, ready for further actions.

3. **Azure Blob Storage Configuration**:
   - An Azure Blob Storage account is set up to act as a secure, online repository for our database backups. This step involves configuring the storage account and creating a Blob Storage container, for example, named `mycontainerfred`, which will house our backups.

4. **Backup File Upload**:
   - The backup file is then uploaded to the designated Blob Storage container, providing an additional layer of data protection with a remotely stored redundant copy.

### 3.2 Restoration in Development Environment

1. **Development Environment Preparation**:
   - A new Windows VM is provisioned to mirror the development setup, equipped with SQL Server to facilitate database activities within a sandbox environment.

2. **Database Restoration**:
   - Leveraging SSMS, the database backup from Azure Blob Storage is restored onto this development VM, allowing for safe experimentation and innovation without affecting the production data.

### 3.3 Automated Backups

1. **Maintenance Plans Configuration in SSMS**:
   - Within SSMS on the development VM, a Maintenance Plan is established to automate regular backups of the development database. This plan is initially created following the backup process and subsequently configured to meet our specific needs.

2. **Scheduling Automated Backups**:
   - The Maintenance Plan is scheduled for weekly execution, ensuring ongoing data protection. Automated backups were to scheduled to occur every week on Sunday at 12:00:00 AM. This was a suitable downtime to complete weekly backups due to the low activity of traffic and users of the database at this time and during the weekend. The setup involves selecting SQL Server Credentials for accessing the Azure Storage Account, specifying the Azure storage container (e.g., `mycontainerfred`), and adjusting the schedule via the "New Job Schedule" window in SSMS to fit our requirements.


By meticulously following these steps, we have fortified our project's data management strategy, ensuring that our database remains secure, recoverable, and consistently backed up. The combination of Azure Blob Storage for backup storage and SSMS for automation showcases our commitment to leveraging cutting-edge technologies for optimal data protection and management.

## Section 4: Disaster Recovery Simulation 



### 4.1 Mimic Data Loss in Production Environment



## Conclusion

This project outlines a structured approach to architecting and implementing a cloud-based database system on Microsoft Azure, focusing on practical aspects of cloud engineering, including disaster recovery, data management, and security.



