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
