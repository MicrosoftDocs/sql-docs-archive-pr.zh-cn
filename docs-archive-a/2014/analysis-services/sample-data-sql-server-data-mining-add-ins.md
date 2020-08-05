---
title: " (SQL Server 数据挖掘外接程序的示例数据) |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- holdout
- testing cases
- training cases
- partitioning data [data mining]
- mining models, testing
ms.assetid: 35907ae6-887f-4cb3-a750-cff3d7683d90
author: minewiskan
ms.author: owend
ms.openlocfilehash: 17da9a42f4d76f5c271d5b225cf897a8ac2e97ba
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579121"
---
# <a name="sample-data-sql-server-data-mining-add-ins"></a>示例数据（SQL Server 数据挖掘外接程序）
  ![“数据挖掘”功能区中的为数据分区向导](media/dmc-partition.gif "“数据挖掘”功能区中的为数据分区向导")  
  
 利用**示例数据**向导，可以轻松地将源数据分为两组，一组用于构建 (定型) 模型，另一组用于测试模型。 此向导还提供了一个选项，可用于重新抽样数据来生成能更好地表示您的目标的新数据集。  
  
 为模型的定型和测试创建正确类型的数据是数据挖掘的一个重要部分，但如果没有适当的工具，将非常单调乏味。 该向导执行分层抽样以确保定型和测试集均衡。  
  
## <a name="random-sampling-and-oversampling"></a>随机抽样和过度抽样  
 . 随机抽样是确保用于测试模型的数据能准确表示用于创建模型的数据的最佳方式。 可对存储在 Excel 或外部数据源中的数据进行随机抽样  
  
 如果使用随机抽样选项，则 "**示例数据**" 向导会自动创建定型和测试数据集，并将其输出到单独的 Excel 工作表中以供日后参考。  
  
 如果你的数据存储在 Excel 工作簿中，而不是外部数据源中，则还可以选择使用*过度抽样*。 通过此选项，指定可能在数据中罕见的目标值，而该向导将收集均衡的一组，其中不仅包括目标值。 可让向导达到一个目标百分比或创建某个数量的行。  
  
 如果使用过度抽样选项，则 "**示例数据**" 向导会创建一个新的工作表，其中包含新平衡的示例数据。  
  
## <a name="using-the-sample-data-wizard"></a>使用示例数据向导  
  
#### <a name="to-separate-data-into-training-and-testing-sets"></a>将数据分为定型集和测试集  
  
1.  在 "**数据挖掘**" 功能区中，单击 "**示例数据**"。  
  
2.  在 "**选择源数据**" 页上，指定要分区的**数据**是位于 Excel 范围还是表中，或在外部数据源中。  
  
3.  在 "**选择抽样类型**" 页上，指定是否要通过随机采样创建定型和测试数据集，或通过过度抽样创建新的数据集。  
  
    > [!NOTE]  
    >  如果使用的是外部数据源，则只能使用随机抽样选项。 如果您要使用外部数据进行过度抽样，则可以通过使用 Excel 数据连接，将外部数据导入 Excel 工作簿中，然后使用“示例数据”向导。  
  
4.  设置特定于您所选的抽样方法的选项。  
  
    -   对于随机抽样，请指定测试是使用原始数据的百分比，还是使用测试数据集中的总行数。  
  
    -   对于过度抽样，请选择要强调的列和值。 然后，指定新数据集中的总行数，以及应包括目标值的新数据集中的行百分比。  
  
         过度抽样的目标值必须是一个离散值，不能对连续数值数据进行过度抽样。  
  
5.  在 "**完成" 页**上，接受新数据集的默认名称，或键入新名称。  
  
     该向导会为每个数据集创建新工作表。  
  
 Excel 数据挖掘客户端中的多数向导还提供一个选项，用于将数据随机划入定型集和测试集。 但是，如果使用这些向导，则数据保留在同一工作表（或其他数据源）中，并在内部存储有关特定行是测试事例还是定型事例的信息。 与此相反，当您使用 "**示例数据**" 向导时，测试数据和定型数据将输出到不同的工作表中，以便于引用。  
  
## <a name="related-options"></a>相关选项  
 在向导中前进时，将有以下选项：  
  
|选项|注释|  
|-------------|--------------|  
|“选择源数据”对话框（Excel 数据挖掘客户端）|选择包含数据的 Excel 范围或表。 如果要使用外部数据，则可使用关系数据，但这些数据必须包括在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源中。 T|  
|“选择抽样类型”页（Excel 数据挖掘客户端）|如果您使用外部数据源，则会限制您只能使用随机抽样选项。 此外，还必须通过使用 "**行计数**" 选项来指定要在最终数据集中创建的行数。 不能指定源数据的百分比。|  
|“随机抽样类型”页（Excel 数据挖掘客户端）|可从源复制行的某个百分比或特定行数。|  
|“过度抽样”页（Excel 数据挖掘客户端）|**目标状态**<br /><br /> 从列表中选择在原始数据集中不常见的值。 过度抽样将增加包含此状态的数据行的比例。<br /><br /> **样本大小**<br /><br /> 选择要提取的总行数。 此值表示最终数据集的大小。|  
  
## <a name="other-sampling-options"></a>其他抽样选项  
 如果此向导中的抽样选项不能满足您的需求，您可使用 SQL Server Integration Services (SSIS) 中的抽样转换功能从多个数据源中抽取行。  
  
 有关详细信息，请参阅[行采样转换](../integration-services/data-flow/transformations/row-sampling-transformation.md)和[百分比抽样转换](../integration-services/data-flow/transformations/percentage-sampling-transformation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘准备清单](checklist-of-preparation-for-data-mining.md)  
  
  
