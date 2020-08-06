---
title: 为 DQS 日志文件配置高级设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- log files,advanced settings
- dqs log files,advanced settings
ms.assetid: 1d565748-9759-425c-ae38-4d2032a86868
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad41b0cac95f9bfe5565ccbac16b0fda3e28ddf6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87683078"
---
# <a name="configure-advanced-settings-for-dqs-log-files"></a>为 DQS 日志文件配置高级设置
  本主题介绍如何为 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 和 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志文件配置高级设置，例如设置日志文件的滚动文件大小限制、设置事件的时间戳模式等。  
  
> [!NOTE]  
>  这些活动不能使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]执行，并且仅面向高级用户。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
  
-   您的 Windows 用户帐户必须是 SQL Server 实例中 sysadmin 固定服务器角色的成员，才能修改 DQS_MAIN 中 A_CONFIGURATION 表的配置设置。  
  
-   您必须以正在修改 DQLog.Client.xml 文件以便配置 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志记录的计算机上 Administrators 组成员的身份登录。  
  
##  <a name="configure-data-quality-server-log-settings"></a><a name="DQSServer"></a>配置数据质量服务器日志设置  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志设置在 DQS_MAIN 数据库的 A_CONFIGURATION 表中 **ServerLogging** 行的 **VALUE** 列中以 XML 格式提供。 您可以运行以下 SQL 查询以便查看配置信息：  
  
```sql  
select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'; 
```  
  
 若要更改 **** 日志记录的配置设置，您必须在 **ServerLogging** 行的 VALUE [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 列中更新相应信息。 在此示例中，我们将更新 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志设置，以便将滚动文件大小限制设置为 25000 KB（默认值为 20000 KB）。  
  
1.  启动 Microsoft SQL Server Management Studio 并连接到适当的 SQL Server 实例。  
  
2.  在“对象资源管理器”中，右键单击服务器，再单击 **“新建查询”**。  
  
3.  在“查询编辑器”窗口中，复制以下 SQL 语句：  
  
    ```sql  
    -- Begin the transaction.  
    BEGIN TRAN  
    GO  
    -- set the XML value field for the row with name=ServerLogging  
    update DQS_MAIN.dbo.A_CONFIGURATION   
    set VALUE='<configuration>  
      <configSections>  
        <section name="loggingConfiguration" type="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.LoggingSettings, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" />  
      </configSections>  
      <loggingConfiguration name="Logging Application Block" tracingEnabled="true" defaultCategory="" logWarningsWhenNoCategoriesMatch="true">  
        <listeners>  
          <add fileName="###REPLACE_THIS_WITH_SQL_SERVER_INSTANCE_LOG_FOLDER_NAME###DQServerLog.###REPLACE_THIS_WITH_SQL_CATALOG_NAME###.log" footer="" formatter="Custom Text Formatter" header="" rollFileExistsBehavior="Increment" rollInterval="None" rollSizeKB="25000" timeStampPattern="yyyy-MM-dd" listenerDataType="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.RollingFlatFileTraceListenerData, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" traceOutputOptions="None" filter="All" type="Microsoft.Practices.EnterpriseLibrary.Logging.TraceListeners.RollingFlatFileTraceListener, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Rolling Flat File Trace Listener" />  
        </listeners>  
        <formatters>  
          <add template="{timestamp(local)}|[{threadName}]|{dictionary({value}|)}{message}" type="Microsoft.Practices.EnterpriseLibrary.Logging.Formatters.TextFormatter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Custom Text Formatter" />  
        </formatters>  
        <logFilters>  
          <add enabled="true" type="Microsoft.Practices.EnterpriseLibrary.Logging.Filters.LogEnabledFilter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="LogEnabled Filter" />  
        </logFilters>  
        <categorySources />  
        <specialSources>  
          <allEvents switchValue="All" name="All Events" />  
          <notProcessed switchValue="All" name="Unprocessed Category" />  
          <errors switchValue="All" name="Logging Errors & Warnings">  
            <listeners>  
              <add name="Rolling Flat File Trace Listener" />  
            </listeners>  
          </errors>  
        </specialSources>  
      </loggingConfiguration>  
    </configuration>'  
    WHERE NAME='ServerLogging'  
    GO  
    -- check the result  
    select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
  
    -- Commit the transaction.  
    COMMIT TRAN  
  
    ```  
  
4.  按 F5 执行这些语句。 检查 "**结果**" 窗格以验证语句是否已成功执行。  
  
5.  若要应用对 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志记录配置进行的更改，您必须运行以下 Transact-SQL 语句。 打开新的“查询编辑器”窗口，然后粘贴以下 Transact-SQL 语句：  
  
    ```sql  
    USE [DQS_MAIN]  
    GO  
    DECLARE @return_value int  
    EXEC @return_value = [internal_core].[RefreshLogSettings]  
    SELECT 'Return Value' = @return_value  
    GO  
    ```  
  
6.  按 F5 执行这些语句。 检查 "**结果**" 窗格以验证语句是否已成功执行。  
  
> [!NOTE]  
>  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志记录设置配置动态生成并且存储于 DQS_MAIN.Log 文件中，该文件通常位于 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log 下（如果您安装了 SQL Server 的默认实例）。 但是，将不会保存在此文件中直接进行的更改，它们将会被 DQS_MAIN 数据库中 A_CONFIGURATION 表的配置设置覆盖。  
  
##  <a name="configure-data-quality-client-log-settings"></a><a name="DQSClient"></a>配置 Data Quality Client 日志设置  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]日志设置配置文件 DQLog.Client.xml 通常在 C:\Program FILES\MICROSOFT SQL server\120\tools\binn\dq\config。上提供。XML 文件的内容类似于您之前为日志配置设置修改的 XML 文件 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 。 配置 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志设置：  
  
1.  以管理员身份运行任何 XML 编辑工具或记事本。  
  
2.  在工具或记事本中打开 DQLog.Client.xml 文件。  
  
3.  进行所需更改，然后保存该文件以便应用新的日志记录更改。  
  
## <a name="see-also"></a>另请参阅  
 [为 DQS 日志文件配置严重级别](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)  
  
  
