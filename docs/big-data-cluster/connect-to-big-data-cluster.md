---
title: Connect to master and HDFS Big data clusters
description: Learn how to connect to the SQL Server master instance and the HDFS/Spark gateway for a SQL Server Big Data Cluster.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab 
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
---

# Connect to a SQL Server big data cluster with Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

This article describes how to connect to a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] from Azure Data Studio.

## Prerequisites

- A deployed [SQL Server 2019 big data cluster](deployment-guidance.md).
- [SQL Server 2019 big data tools](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 extension**
   - **kubectl**
   - **azdata**

## <a id="master"></a> Connect to the cluster

To connect to a big data cluster with Azure Data Studio, make a new connection to the SQL Server master instance in the cluster. The following steps describe how to connect to the master instance using Azure Data Studio.

1. Find the SQL Server master instance endpoint:

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > For more information on how to retrieve endpoints see [Retrieve endpoints](deployment-guidance.md#endpoints).

1. In Azure Data Studio, press **F1** > **New Connection**.

1. In **Connection type**, select **Microsoft SQL Server**.

1. Type the endpoint name you found for SQL Server master instance in the **Server name** textbox (for example: **\<IP_Address\>,31433**). 

1. Choose your authentication type. For SQL Server master instance running in big data clusters only **Windows Authentication** and 
**SQL login** are supported. 

1. Enter SQL login **User name** and **Password**. If you are using Windows Authentication, this is not 
necessary.

   > [!TIP]
   > By default, the user name **SA** is disabled during big data cluster deployment. A new sysadmin user is provisioned during deployemnt with the name corresponding to **AZDATA_USERNAME** environment variable and the password corresponding to the **AZDATA_PASSWORD** environment variable used during deployment.

1. Change the target **Database name** to one of your relational databases.

   ![Connect to the master instance](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. Press **Connect**, and the **Server Dashboard** should appear.

With the February 2019 release of Azure Data Studio, connecting to the SQL Server master instance also enables you to interact with the HDFS/Spark gateway. This means that you do not need to use a separate connection for HDFS and Spark that the next section describes.

- The Object Explorer now contains a new **Data Services** node with right-click support for big data cluster tasks, such as creating new notebooks or submitting spark jobs. 
- The **Data Services** node also contains an **HDFS** folder for HDFS exploration and performing actions such as Create External Table or Analyze in Notebook.
- The **Server Dashboard** for the connection also contains tabs for **SQL Server big data cluster** and **SQL Server 2019** when the extension is installed.

   ![Azure Data Studio Data Services Node](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## Next steps

For more information about [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], see [What are [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md).
