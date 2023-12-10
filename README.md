# Azure Database Migration Project

## Overview
In this project, I architect and implement a cloud-based database system on Microsoft Azure, showcasing my hands-on expertise in cloud engineering.
I begin by establishing a production environment database. Subsequently, I migrated the database to Azure SQL Database, focusing on crucial aspects like data backup, restoration, and automated scheduling. 
A pivotal phase of the project involved simulating a disaster recovery scenario with potential data loss. Furthermore, I explore the complexities of geo-replication and failover configuration to ensure data availability even under challenging conditions.
To enhance security, I employ Microsoft Entra ID integration to define access roles, adding an extra layer of control and protection.

## Setting up the production environment
1. Azure account and subscription set up.
2. Using the Azure portal, a Windows virtual machine was set up to serve as the production environment.
3. Appropriate network and firewall settings were configured and a secure connection was established using the RDP protocol.
4. SQL Server and SQL Server Management Studio (SSMS) were installed on the virtual machine.
5. The production database was set up by restoring the database from a backup file (AdventureWorks2022.bak).
6. The production database was now set up and ready for use.

## Migration to Azure SQL Database
1. Using the Azure portal, an Azure SQL Database was created as well as an associated SQL server with SQL login authentication.
2. Appropriate network and firewall rules were configured.
3. Data Studio was downloaded and installed on the VM.
4. A connection was made to both the local database and the Azure SQL database via Data Studio.
5. The Data Studio SQL Server Schema Compare extension was installed and leveraged to migrate the schema from the on-premise database to the Azure SQL database.
6. The Data Studio Azure SQL Migration extension was installed and used to facilitate the transfer of data from the on-premise database to the Azure SQL database.
7. The transferred data was inspected to confirm the success of the data migration process.

## Data Back-up and Restoration
1. A full backup was generated of the on-premises database using SQL Server Management Studio.
2. This backup file was stored on a newly created Azure Blob Storage Container.
3. A developmental Windows VM was created and a remote connection was established via RDP protocol. SQL Server and SSMS were installed on the new developmental VM.
4. The database was restored using the backup file stored in the Azure blob storage container. Now a complete replica database of our production VM was available.
5. SSMS Management Task Wizard was utilized to configure a weekly backup schedule to the Azure Blob Storage. This was achieved by creating an SQL Server credential and using the job scheduler to set up a weekly backup schedule.

## Disaster Recovery Simulation
1. Data was manually erased from the database to simulate some data loss. Using the SQL queries attached, a column was deleted in the PersonAddress table and 5 rows of data were deleted from the PersonAddressType table.
2. Data loss was confirmed by using a select query to examine the data.
3. The database restore function was utilised via the Azure portal to create a new database to restore the production database in the state it was 2 hours previously. A new database was created and a new connection was established via Azure Data Studio.
4. The new database was examined to confirm the lost data was recovered.
5. The old database was deleted via the Azure Portal.


