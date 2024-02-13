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

Disaster recovery is essential for maintaining business continuity and safeguarding data against unforeseen incidents. Testing these procedures in a controlled environment is critical for validating the recovery strategies, enhancing plan effectiveness, reducing potential downtime, identifying improvement areas, and ensuring compliance with regulations.

Azure SQL Database supports various methods for simulating data loss, enabling organizations to prepare for different scenarios:

- Intentional Deletion of Data: Simulate loss by deleting data, such as records, tables, or data ranges.
- Data Corruption: Introduce corruption by altering records or fields to test recovery processes.
- Accidental Updates: Perform incorrect updates via direct manipulation or flawed scripts.
- Service Outages: Mimic service interruptions or connectivity issues to evaluate disaster recovery readiness.
- Simulated Regional Outages: For georeplicated setups, simulate outages in the primary region to assess failover to secondary regions.

### Precautions for Data Loss Simulation

When simulating data loss, it's crucial to minimize risk and avoid impacting live data:

- Use Non-Production Environments: Conduct tests in non-production settings, though for this project, data was intentionally removed from the production database to simulate disaster scenarios due to its test nature and lack of active users.
- Backup Before Testing: Ensure the database is backed up before testing to allow restoration to a known good state.
- Inform Stakeholders: Keep relevant parties informed about the testing to maintain transparency.
- Document the Process: Record testing steps and outcomes for future reference and analysis.

Regular testing of disaster recovery procedures by simulating data loss in a controlled environment equips organizations to effectively respond to actual incidents, minimizing the impact on critical operations.

### 4.1 Mimic Data Loss in Production Environment

To mimic data loss in the production database of AdventureWorks, first a query was run to view all the data in the 'Sales.Customer' table of the database. 

1. **Identify Relevant Tables/Data**: Determine which tables contain
```sql
SELECT * 
FROM Sales.Customer;
```

This query returns all customer information from the `Sales.Customer` table in Azure Data Studio. In total there are 19820 rows in the table, containing customer information such as account numbers.

2. **Corrupting Data**: Modify or delete data directly within the database using a tool like Azure Data Studio
To simulate a data loss scenario, you can delete this record using the following code snippet:
```sql
DELETE FROM SALES.Customer
WHERE PersonID IS NULL;
```
> Note: Before proceeding with any deletion or modification operation, make sure you have a backup!

This query execution removes 701 rows from the 'Sales.Customer' table. This serves as a considerable data loss for the production database AdventureWorks. 

The data loss was verified by running the inital query again to  check if the deleted rows are present. The query now returns a table with 19119 entries, compared to 19820 after the first query before the data loss, confirming that the table is now missing 701 rows. 

### 4.2 Restore Database from Azure SQL Database Backup

After performing the simulation, the production database needs to be restored to its previous uncorrupted state from an Azure SQL Database backup. This backup was uploaded to the Azure SQL database earlier in the project. 

To restore an Azure SQL Database, access the Azure portal and navigate to your database dashboard. Select the database, then click "Restore" on the top bar. In the "Restore database" window, a restore point before the data loss was selected — choose a point based on when the last known good data was present, like two hours before the incident if applicable. It's important to note that if the database is very active with lots of users, you would need to choose the closest point in time before data loss has occurred for minimal data loss. 

Name the new database, appending "-restored" to distinguish it, then click "Review + create" followed by "Create" to initiate the restoration, which takes a few minutes. After deployment, find the new database in the Azure SQL Database resource list. Verify its restoration point by connecting through Azure Data Studio.

The same intial query was run on the restored database to confirm its success. 
```sql
SELECT * 
FROM Sales.Customer;
```
As  expected, the query returned the same result as the initial production database before the simulated data loss. Therefore the database restoration was successful. It is important to now delete the corrupted data loss and now the restored database acts as the production database. This is achieved by using the 'Delete Connection' option on the original database (e.g. my-database-fred) under the 'Servers' Object Explorer under 'Connections'.

## Section 5: Geo-Replication and Failover

To enhance the disaster recovery strategy for my AdventureWorks database, I embarked on setting up geo-replication in Azure SQL Database. This process involves asynchronously replicating the primary database to a secondary region, providing a robust solution for data redundancy and high availability across different geographic locations.

### 5.1 How Geo-Replication Works
- **Primary Database**: The original database, 'AdventureWorks' in our case, serving the application with read and write capabilities.
- **Secondary Database**: A read-only copy of the 'AdventureWorks' database situated in a different Azure region, synchronized asynchronously to minimize impact on the primary database.
- **Data Replication**: Changes in the primary database are replicated to the secondary database asynchronously, using Azure's infrastructure.
- **Automatic Failover**: Allows manual initiation of failover or relies on Azure's automatic failover to promote the secondary database to primary, reducing downtime.

### 5.2 Implementing Geo-Replication

1. **Primary Database Selection**:
    - Navigated to the Azure portal and located the primary AdventureWorks database from the Azure SQL Database dashboard.

2. **Initiating Geo-Replication**:
    - Selected "Replicas" under "Data Management" in the database's menu and clicked on "Create replica" to start the setup.

3. **Secondary Server Configuration**:
    - Opted to create a new SQL Server (`my-replication-server`) in the East US region for the secondary database, using SQL authentication for login credentials.

4. **Replication Process**:
    - Reviewed the new server details and initiated the replication by clicking "Create", starting the data synchronization between primary and secondary databases.

### 5.3 Post-Setup Verification

Verified the replica type as 'Geo' in the Azure portal, with 'AdventureWorks-database-restored' correctly identified as the primary database, ensuring preparedness for regional disruptions. 

### 5.4 Test Failover and Tailback

After setting up geo-replication, you can test failover by initiating a manual planned failover and tailback  in the Azure portal. Failover is the process of switching the workload from the primary region to the secondary region in a georeplicated environment. Thus, a planned failover simulates real-world challenges where you might need to perform maintenance or planned downtime on the primary server. 

Implemented a failover process for the AdventureWorks database to test the disaster recovery strategy within the Azure SQL Database environment, specifically focusing on switching the primary database role to the secondary server and vice versa.

#### Initiating Failover Group Creation

1. **Primary Database Server Selection**:
    - Accessed the Azure portal and selected the SQL server associated with the primary database, `production-database-restored` located in the UK region, from the Azure SQL Database dashboard.

2. **Failover Group Configuration**:
    - Chose **Failover groups** under the **Data management** pane and selected **Add group** to create a new failover group.

3. **Failover Group Setup**:
    - Named the failover group and selected the secondary server (e.g., `my-replication-server`) for the **Server** field, leaving other settings at their defaults before clicking **Create**.

#### Executing Planned Failover

1. **Secondary Server Navigation**:
    - Navigated to the Azure SQL Server where the replication database resides, in this case, `my-replication-server`.

2. **Planned Failover Initiation**:
    - Initiated a planned failover by selecting **Failover** from the task pane, confirming the operation despite warnings about changing the secondary database to the primary role.

3. **Failover Completion and Verification**:
    - Waited for the failover to complete and then verified the role swap between the two servers. Utilized the connection details from the now primary server in the secondary region to test and validate the database's functionality, ensuring it operated as expected post-failover.

#### Failover Testing Insights

To further assess the functionality of the geo-replicated server, a connection to the server was created on Azure Data Studio in order to execute queries on the AdventureWorks database. This step was crucial to confirm the availability of the server post-failover and to ensure that the data remained complete and accessible. Running these queries provided tangible evidence of the seamless continuation of database operations, highlighting the effectiveness of the geo-replication and failover setup in preserving data integrity and availability in the event of server crashes.

Testing the failover process for the AdventureWorks database by creating a failover group, executing a planned failover, and verifying the operation's success provided invaluable insights into the disaster recovery environment's functionality. Regular testing of these procedures enhances the preparedness of the disaster recovery plan, reinforcing the organization's capability to manage unexpected incidents efficiently.


## Conclusion

This project outlines a structured approach to architecting and implementing a cloud-based database system on Microsoft Azure, focusing on practical aspects of cloud engineering, including disaster recovery, data management, and security.



