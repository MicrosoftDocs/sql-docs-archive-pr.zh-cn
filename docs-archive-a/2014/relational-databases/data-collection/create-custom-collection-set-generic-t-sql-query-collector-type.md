---
title: 创建使用一般 T-sql 查询收集器类型的自定义收集组 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- T-SQL Query collector type
- collection sets [SQL Server], creating custom
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ab21ad5fd65556dec639fd5ca6999d23e2de673b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588573"
---
# <a name="create-a-custom-collection-set-that-uses-the-generic-t-sql-query-collector-type-transact-sql"></a>创建使用一般 T-SQL 查询收集器类型的自定义收集组 (Transact-SQL)
  可以使用与数据收集器一起提供的存储过程创建包含使用一般 T-SQL 查询收集器类型的收集项的自定义收集组。 若要完成此任务，需使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的查询编辑器来执行以下过程：  
  
-   配置上载计划。  
  
-   定义和创建收集组。  
  
-   定义和创建收集项。  
  
-   验证该收集组和收集项是否存在。  
  
> [!NOTE]  
>  在创建自定义收集组之前，必须配置数据收集参数。 有关详细信息，请参阅[配置数据收集参数 (Transact-SQL)](configure-data-collection-parameters-transact-sql.md)。  
  
### <a name="define-and-create-the-collection-set"></a>定义和创建收集组  
  
1.  使用 sp_syscollector_create_collection_set 存储过程定义一个新的收集组。  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     收集模式可以设置为 0（缓存）或 1（非缓存）。  
  
     日志记录级别可以设置为 0、1 或 2。  
  
     以下预配置计划随数据收集器一起提供：  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     如果不想使用提供的这些计划，您可以创建一个新计划，然后将其用于收集组。 有关详细信息，请参阅 [创建计划并将计划附加到作业](../../ssms/agent/create-and-attach-schedules-to-jobs.md)。  
  
### <a name="define-and-create-a-collection-item"></a>定义和创建收集项  
  
1.  由于新的收集项基于已经安装的一般收集器类型，因此可以运行以下代码来设置 GUID，使其与一般 T-SQL 查询收集器类型相对应。  
  
    ```sql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  使用 sp_syscollector_create_collection_item 存储过程来创建收集项。 声明收集项的架构，这样它将映射到一般 T-SQL 查询收集器类型所需的架构。  
  
    ```sql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### <a name="verify-that-the-new-collection-set-and-collection-item-exist"></a>验证新的收集组和收集项是否存在  
  
1.  在启动新的收集组之前，运行以下查询以验证新的收集组及其收集项是否已创建。  
  
    ```sql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     您还可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中执行目视检查。 在对象资源管理器中，展开 **“管理”** 节点，然后展开 **“数据收集”** 。 新的收集组将显示。 收集组的红色圆圈图标指示该收集组已停止。  
  
## <a name="example"></a>示例  
 下面的代码示例汇集了上面步骤中记录的示例。 请注意，为收集项设置的收集频率（5 秒钟）将被忽略，因为收集组的收集模式设置为 0，即缓存模式。 有关详细信息，请参阅 [Data Collection](data-collection.md)。  
  
```sql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据收集器存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)   
 [管理计划](../../ssms/agent/manage-schedules.md)   
 [启动或停止收集组](start-or-stop-a-collection-set.md)  
  
  
