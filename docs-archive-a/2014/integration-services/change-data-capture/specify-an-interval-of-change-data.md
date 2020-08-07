---
title: 指定变更数据的间隔 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],specifying interval
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 70b9c14d609f2db69ee5751eca18acb5262a07a1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580320"
---
# <a name="specify-an-interval-of-change-data"></a>指定变更数据的间隔
  在用于执行变更数据增量加载的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的控制流中，第一个任务是计算变更数据的端点。 这些端点是 `datetime` 值，将存储在包变量中以供以后在包中使用。  
  
> [!NOTE]  
>  有关设计控制流的总体过程的说明，请参阅[变更数据捕获 (SSIS)](change-data-capture-ssis.md)。  
  
## <a name="set-up-package-variables-for-the-endpoints"></a>为端点设置包变量  
 在配置执行 SQL 任务以计算端点之前，必须先定义用于存储端点的包变量。  
  
#### <a name="to-set-up-package-variables"></a>设置包变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在 **“变量”** 窗口中创建以下变量：  
  
    1.  创建一个数据类型为 `datetime` 的变量以保存间隔的起始点。  
  
         以下示例使用变量名 ExtractStartTime。  
  
    2.  再创建一个数据类型为 `datetime` 的变量以保存间隔的结束点。  
  
         以下示例使用变量名 ExtractEndTime。  
  
 如果在执行多个子包的主包中计算端点，则可使用父包变量配置将这些变量的值传递给各个子包。 有关详细信息，请参阅 [执行包任务](../control-flow/execute-package-task.md) 和 [在子包中使用变量和参数的值](../use-the-values-of-variables-and-parameters-in-a-child-package.md)。  
  
## <a name="calculate-a-starting-point-and-an-ending-point-for-change-data"></a>计算变更数据的起始点和结束点  
 为间隔端点设置包变量之后，即可计算这些端点的实际值并将这些值映射到相应的包变量中。 因为这些端点为 `datetime` 值，所以您必须使用可以计算或处理 `datetime` 值的函数。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 表达式语言和 Transact-SQL 都具有可处理 `datetime` 值的函数：  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 表达式语言中可处理 `datetime` 值的函数  
 -   [DATEADD（SSIS 表达式）](../expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF（SSIS 表达式）](../expressions/datediff-ssis-expression.md)  
  
-   [DATEPART（SSIS 表达式）](../expressions/datepart-ssis-expression.md)  
  
-   [DAY（SSIS 表达式）](../expressions/day-ssis-expression.md)  
  
-   [GETDATE（SSIS 表达式）](../expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE（SSIS 表达式）](../expressions/getutcdate-ssis-expression.md)  
  
-   [MONTH（SSIS 表达式）](../expressions/month-ssis-expression.md)  
  
-   [YEAR（SSIS 表达式）](../expressions/year-ssis-expression.md)  
  
 Transact-SQL 中可处理 `datetime` 值的函数  
 [日期和时间的数据类型及函数 (Transact-SQL)](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)。  
  
 在使用上述任一 `datetime` 函数来计算端点之前，必须先确定间隔是否固定并且定期发生。 通常，您会希望定期将在源表中发生的变更应用到目标表中。 例如，您可能希望每小时、每天或每周应用这些变更。  
  
 在了解变更间隔是固定的还是随机的之后，即可计算端点：  
  
-   **计算起始日期和时间**。 将上一次加载的结束日期和时间作为当前的起始日期和时间。 如果对增量加载使用固定间隔，则可使用 Transact-SQL 或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 表达式语言的 `datetime` 函数来计算此值。 否则，您可能需要保持两个执行之间的端点，并使用执行 SQL 任务或脚本任务来加载上一个端点。  
  
-   **计算结束日期和时间**。 如果对增量加载使用固定间隔，则可将当前的结束日期和时间作为起始日期和时间的偏移量来计算。 同样，可以使用 `datetime` transact-sql 或表达式语言的函数来计算此值 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
 在下面的过程中，变更间隔使用固定间隔，并假定无例外的情况下增量加载包每天运行。 否则，缺失间隔的变更数据会丢失。 此间隔的起始点是前天午夜，即 24 小时和 48 小时之前。 此间隔的结束点是昨天午夜，即，昨天晚上，0 和 24 小时之前。  
  
#### <a name="to-calculate-the-starting-point-and-ending-point-for-the-capture-interval"></a>计算捕获间隔的起始点和结束点  
  
1.  在 **设计器的** “控制流” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 选项卡上，向包中添加一个执行 SQL 任务。  
  
2.  打开 **“执行 SQL 任务编辑器”** ，在编辑器的 **“常规”** 页上，选择以下选项：  
  
    1.  对于 **ResultSet**，选择 **“单行”** 。  
  
    2.  配置到源数据库的有效连接。  
  
    3.  对于 **SQLSourceType**，选择 **“直接输入”** 。  
  
    4.  对于 **SQLStatement**，输入以下 SQL 语句：  
  
        ```  
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  在 **“执行 SQL 任务编辑器”** 的 **“结果集”** 页上，将 ExtractStartTime 结果映射到 ExtractStartTime 包变量，并将 ExtractEndTime 结果映射到 ExtractEndTime 包变量。  
  
    > [!NOTE]  
    >  如果使用表达式设置 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 变量的值，则每次访问该变量的值时都会计算表达式。  
  
## <a name="next-step"></a>下一步  
 计算变更范围的起始点和结束点之后，下一步就是确定变更数据是否已准备就绪。  
  
 **下一个主题：** [确定变更数据是否已准备就绪](determine-whether-the-change-data-is-ready.md)  
  
## <a name="see-also"></a>另请参阅  
 [在包中使用变量](../use-variables-in-packages.md)   
 [Integration Services (SSIS) 表达式](../expressions/integration-services-ssis-expressions.md)   
 [执行 SQL 任务](../control-flow/execute-sql-task.md)   
 [脚本任务](../control-flow/script-task.md)  
  
  
