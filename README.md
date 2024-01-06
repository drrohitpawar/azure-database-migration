# Azure Database Migration Project

## Overview
In this project, I architect and implement a cloud-based database system on Microsoft Azure, showcasing my hands-on expertise in cloud engineering.
I begin by establishing a production environment database. Subsequently, I migrated the database to Azure SQL Database, focusing on crucial aspects like data backup, restoration, and automated scheduling. 
A pivotal phase of the project involved simulating a disaster recovery scenario with potential data loss. Furthermore, I explore the complexities of geo-replication and failover configuration to ensure data availability even under challenging conditions.
To enhance security, I employ Microsoft Entra ID integration to define access roles, adding an extra layer of control and protection.

![](https://github.com/drrohitpawar/azure-database-migration710/blob/main/Images/Copy%20of%20Azure%20Project%20Diagram.jpeg)

## Setting up the production environment
1. Azure account and subscription set up.
2. Using the Azure portal, a Windows virtual machine was set up to serve as the production environment.
3. Appropriate network and firewall settings were configured and a secure connection was established using the RDP protocol.
   - This was done by ensuring that the RDP port (port 3389) was allowed in the NSG inbound rules for the VM.
![](https://github.com/drrohitpawar/azure-database-migration/blob/main/Images/network.png)
4. SQL Server and SQL Server Management Studio (SSMS) were installed on the virtual machine.
5. The production database was set up by restoring the database from a backup file (AdventureWorks2022.bak).
   - This was achieved by utilizing the restore database function on SSMS. Right-click on Databases and select 'restore database.' Select the .bak file and select OK. This will restore the database.
![](https://github.com/drrohitpawar/azure-database-migration/blob/main/Images/backup.jpg)
6. The production database was now set up and ready for use.

## Migration to Azure SQL Database
1. Using the Azure portal, an Azure SQL Database was created as well as an associated SQL server with SQL login authentication.
2. Appropriate network and firewall rules were configured.
3. Data Studio was downloaded and installed on the VM.
4. A connection was made to both the local database and the Azure SQL database via Data Studio.
5. The Data Studio SQL Server Schema Compare extension was installed and leveraged to migrate the schema from the on-premise database to the Azure SQL database.
    - The local database was selected as the source and the Azure SQL database was selected as the target
![](https://github.com/drrohitpawar/azure-database-migration/blob/main/Images/compare.jpg)
6. The Data Studio Azure SQL Migration extension was installed and used to facilitate the transfer of data from the on-premise database to the Azure SQL database.
    - Right-click the local database and then click 'Manage' and select Azure SQL Migration.
    - Data Studio will lead you through the process of migrating the database.
    - This will involve Data Studio assessing the current local database
    - Then select the target Azure SQL database and ensure current authentication.
    - It will require you to create an Azure Database Migration Service.
    - Once all the steps are complete, the migration process will start and may take some time.
7. The transferred data was inspected to confirm the success of the data migration process.

## Data Back-up and Restoration
1. A full backup was generated of the on-premises database using SQL Server Management Studio.
2. This backup file was stored on a newly created Azure Blob Storage Container.
3. A developmental Windows VM was created and a remote connection was established via RDP protocol. SQL Server and SSMS were installed on the new developmental VM.
4. The database was restored using the backup file stored in the Azure blob storage container. Now a complete replica database of our production VM was available.
   - The image below is from SSMS on the development VM showing the successful replication database.
![](https://github.com/drrohitpawar/azure-database-migration/blob/main/Images/development.jpg)
5. SSMS Management Task Wizard was utilized to configure a weekly backup schedule to the Azure Blob Storage. This was achieved by creating an SQL Server credential and using the job scheduler to set up a weekly backup schedule.
   - This may be essential for any business to ensure data protection and data recovery in the event of a data loss event. It may also be required due to regulatory and compliance requirements.

## Disaster Recovery Simulation
1. Data was manually erased from the database to simulate some data loss. Using the SQL queries attached, a column was deleted in the PersonAddress table and 5 rows of data were deleted from the PersonAddressType table.
2. Data loss was confirmed by using a select query to examine the data.
   - In the below image, you can see AddressLine1 column has been deleted.
![](https://github.com/drrohitpawar/azure-database-migration/blob/main/Images/prerec.jpg)
3. The database restore function was utilized via the Azure portal to create a new database to restore the production database in the state it was 2 hours previously. A new database was created and a new connection was established via Azure Data Studio.
4. The new database was examined to confirm the lost data was recovered.
   - In the below image, you can see the previously deleted column has been restored.
![](https://github.com/drrohitpawar/azure-database-migration/blob/main/Images/postrec.jpg)
5. The old database was deleted via the Azure Portal.

## Geo-replication and Failover
1. To test geo-replication and failover, the Azure database replica function was utilized. A new server 'sql-replication-server' was created in a different region (in this case North Europe as opposed to UK south of the primary database).
   -  In case of a catastrophic event, such as a natural disaster, data center outage, or region-wide failure, having a geo-replicated server in a different region ensures that your services remain available. It acts as a failover option, providing business continuity even when the primary region experiences problems.
2. A failover group was then generated on the original server to allow failover to the secondary server.
3. A failover test was completed which successfully shifted the primary server to the Northern Europe server.
4. A new connection was established to the new primary server located in Northern Europe.
5. The data was inspected via Azure Data Studio to ensure all tables were still present and no data loss occurred. 'SELECT COUNT(*) FROM table_name' queries were performed before and after failover on a random selection of tables in the database to ensure no rows of data were lost.
6. A tailback test was performed to revert the primary server back to the original server in UK south.
7. This test was useful in demonstrating the disaster recovery environment's functionality. Failover tests should be performed regularly to ensure it is ready for a real disaster recovery.

## Microsoft Entra Directory Integration
1. Microsoft Entra ID authentication was enabled and an admin was set via the Azure portal.
2. A successful connection was established to the database with the new credentials.
3. A new user "Rohit_DB_Reader" was created via the Azure portal.
   - The reason to create a Reader role may be to limit access to prevent unauthorized change and to ensure strict security policies are adhered to prevent unwanted access.
4. The below query was performed to give the user read-only access.
![alt text](https://github.com/drrohitpawar/azure-database-migration710/blob/main/Images/Create%20db_datareader%20role.jpg)
5. A successful connection was established with the new user credentials.
6. The below queries were run to demonstrate the new user had read-only access and is unable to write data/make changes.
![alt text](https://github.com/drrohitpawar/azure-database-migration710/blob/main/Images/Select%20query.jpg)
![alt text](https://github.com/drrohitpawar/azure-database-migration710/blob/main/Images/Delete%20query.jpg)
