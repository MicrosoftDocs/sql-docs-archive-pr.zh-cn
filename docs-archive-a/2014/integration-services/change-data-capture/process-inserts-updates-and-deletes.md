---
title: 处理插入、更新和删除 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],processing data
ms.assetid: 13a84d21-2623-4efe-b442-4125a7a2d690
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 67f016aaf4f7f83c0fa506966c4e78f5b8fadef6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577775"
---
# <a name="process-inserts-updates-and-deletes"></a>处理插入、更新和删除
  在用于执行变更数据的增量加载的 Integration Services 包的数据流中，第二个任务是分隔插入、更新和删除操作。 然后，可以使用相应的命令将它们应用到目标。  
  
> [!NOTE]  
>  为执行变更数据增量加载的包设计数据流的过程中，第一个任务是配置用于运行查询以检索变更数据的源组件。 有关此组件的详细信息，请参阅 [检索和了解变更数据](retrieve-and-understand-the-change-data.md)。 有关创建用于执行变更数据增量加载的包的完整过程的说明，请参阅[变更数据捕获 (SSIS)](change-data-capture-ssis.md)。  
  
## <a name="associating-friendly-values-to-separate-inserts-updates-and-deletes"></a>关联友好值以分隔插入、更新和删除操作  
 在检索变更数据的示例查询中，**cdc.fn_cdc_get_net_changes_<capture_instance>** 函数仅返回名为 **__$operation** 的元数据列。 此元数据列包含一个序号值，该值指示哪个操作导致更改。  
  
> [!NOTE]  
>  有关使用和调用 **cdc.fn_cdc_get_net_changes_<capture_instance>** 函数的查询的详细信息，请参阅[创建函数以检索变更数据](create-the-function-to-retrieve-the-change-data.md)。  
  
 将序号值与其相应的操作匹配，不像使用操作的助记键那样容易。 例如，D 可以简便地表示删除操作，而 I 则可表示插入操作。 在主题 [创建函数以检索变更数据](create-the-function-to-retrieve-the-change-data.md)中创建的示例查询执行了此转换，即将序号值转换为新列中返回的友好字符串值。 下面的代码段显示了此转换：  
  
```  
select   
    ...  
    case __$operation  
        when 1 then 'D'  
        when 2 then 'I'  
        when 4 then 'U'  
        else null  
     end as CDC_OPERATION  
```  
  
## <a name="configuring-a-conditional-split-transformation-to-direct-inserts-updates-and-deletes"></a>配置有条件拆分转换以定向插入、更新和删除操作  
 若要将变更数据行定向到三个输出中的一个输出，有条件拆分转换是理想的选择。 该转换只是检索各行中 **CDC_OPERATION** 列的值，并确定该变更是插入操作、更新操作还是删除操作。  
  
> [!NOTE]  
>  CDC_OPERATION 列包含一个从 **__$operation** 列中的数值派生的友好字符串值。  
  
#### <a name="to-split-inserts-updates-and-deletes-for-processing-by-using-a-conditional-split-transformation"></a>使用有条件拆分转换拆分要进行处理的插入、更新和删除操作  
  
1.  在 **“数据流”** 选项卡上，添加一个有条件拆分转换。  
  
2.  将 OLE DB 源的输出连接到有条件拆分转换。  
  
3.  在 **“有条件拆分转换编辑器”** 的下部窗格中，输入下面三行以指定三个输出  
  
    1.  输入条件为 `CDC_OPERATION == "I"` 的行，以将已插入的行定向到插入操作的输出。  
  
    2.  输入条件为 `CDC_OPERATION == "U"` 的行，以将已更新的行定向到更新操作的输出。  
  
    3.  输入条件为 `CDC_OPERATION == "D"` 的行，以将已删除的行定向到删除操作的输出。  
  
## <a name="next-step"></a>下一步  
 在拆分要处理的行之后，下一步是将更改应用到目标中。  
  
 **下一个主题：** [将变更应用到目标](apply-the-changes-to-the-destination.md)  
  
## <a name="see-also"></a>另请参阅  
 [Conditional Split Transformation](../data-flow/transformations/conditional-split-transformation.md)   
 [使用有条件拆分转换拆分数据集](../data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
