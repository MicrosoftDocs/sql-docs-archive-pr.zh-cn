---
title: 安装 SQL Server 更新后升级 DQS 数据库架构 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 80a1714ea250cf7cf5d34bc9d208a42a64284308
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587617"
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>在安装 SQL Server 更新后升级 DQS 数据库架构
  当你在先前配置的 DQS 实例上安装了 SQL Server 更新（补丁、修补程序或累积更新）后，你可能需要运行 DQSInstaller.exe 文件（带 **upgrade** 命令行参数）来升级 DQS 数据库架构。 否则，当您尝试使用数据质量客户端连接到数据质量服务器时，可能会收到以下错误：  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 升级 DQS 数据库架构不会影响 DQS 数据库（知识库、数据质量项目以及 DQS_STAGING_DATA 数据库中的已导出结果）中的现有数据。 但是，您必须先备份 DQS 数据库，然后才能升级 DQS 数据库架构，以防止在架构升级过程中出现任何意外数据损失。 有关备份 DQS 数据库的信息，请参阅 [Backing Up and Restoring DQS Databases](../backing-up-and-restoring-dqs-databases.md)。  
  
> [!NOTE]  
>  大多数 SQL Server 更新将要求升级到 DQS 数据库架构。 有关要求升级到 DQS 数据库架构的 SQL Server 更新的信息，请参阅 [升级 DQS：在 Data Quality Services 中安装累积更新或修补程序](https://go.microsoft.com/fwlink/?LinkID=251565)中的步骤 1.A。  
  
## <a name="prerequisites"></a>必备条件  
  
-   您必须作为 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 计算机上 Administrators 组的成员登录。  
  
-   您的 Windows 用户帐户必须是安装了 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 的 SQL Server 实例中 sysadmin 固定服务器角色的成员。  
  
### <a name="to-upgrade-dqs-databases-schema"></a>升级 DQS 数据库架构  
  
1.  （建议）首先备份 DQS 数据库，然后进行架构升级。 有关备份 DQS 数据库的信息，请参阅 [Backing Up and Restoring DQS Databases](../backing-up-and-restoring-dqs-databases.md)。  
  
2.  启动命令提示符。  
  
3.  在命令提示符下，将目录更改为 DQSInstaller.exe 出现的位置。 如果您安装了 SQL Server 的默认实例，则 DQSInstaller.exe 文件将出现在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn 下：  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  在命令提示符下，键入以下命令，再按 Enter：  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  安装程序会提示您在继续操作之前备份 DQS 数据库。 如果已经备份了 DQS 数据库，请键入 `Y` 或 `Yes`，然后按 Enter 以继续升级。  
  
6.  在成功升级 DQS 数据库架构之后，将显示一条完成消息。  
  
## <a name="next-steps"></a>后续步骤  
 从数据质量客户端应用程序登录到升级后的数据质量服务器。  
  
 有关安装 SQL Server 更新后升级 DQS 数据库架构以及相关故障排除步骤的详细信息，请参阅 [升级 DQS：在 Data Quality Services 中安装累积更新或修补程序更新](https://go.microsoft.com/fwlink/?LinkID=251565)。  
  
## <a name="see-also"></a>另请参阅  
 [安装 Data Quality Services](install-data-quality-services.md)   
 [.NET Framework 更新后升级 SQLCLR 程序集](upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  
