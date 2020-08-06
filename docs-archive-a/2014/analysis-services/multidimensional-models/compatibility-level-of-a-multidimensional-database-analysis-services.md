---
title: 设置多维数据库 (Analysis Services) 的兼容级别 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 978279e6-a581-4184-af9d-8701b9826a89
author: minewiskan
ms.author: owend
ms.openlocfilehash: eea3d522abc5133e759cf476f3b169fd570b196f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691986"
---
# <a name="set-the-compatibility-level-of-a-multidimensional-database-analysis-services"></a>设置多维数据库的兼容级别 (Analysis Services)
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，数据库兼容级别属性确定数据库的功能级别。 兼容级别对于每个模型类型都是唯一的。 例如，兼容级别 `1100` 具有不同的含义，具体取决于该数据库是多维数据库还是表格数据库。  
  
 本主题仅描述多维数据库的兼容级别。 有关表格解决方案的详细信息，请参阅[&#40;SSAS 表格 SP1&#41;兼容级别](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
> [!NOTE]  
>  表格模型具有其他一些不适用于多维模型的数据库兼容级别。 多维模型不具有兼容级别 `1103`。 有关表格解决方案的详细信息，请参阅[SQL Server 2012 SP1 和兼容性级别中表格模型的新增功能](https://go.microsoft.com/fwlink/?LinkId=301727) `1103` 。  
  
 **多维数据库的兼容级别**  
  
 目前，唯一因功能级别而异的多维数据库行为是字符串存储体系结构。 通过提高数据库兼容级别，可以覆盖度量值和维度的最大 4 GB 字符串存储限制。  
  
 对于多维数据库，`CompatibilityLevel` 属性的有效值包括以下：  
  
|设置|说明|  
|-------------|-----------------|  
|`1050`|此值在脚本或工具中不可见，但它对应于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中创建的数据库。 对于任何没有显式设置 `CompatibilityLevel` 的数据库，都将在 `1050` 级别隐式运行。|  
|`1100`|这是在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中创建的新数据库的默认值。 您还可以为在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的早期版本中创建的数据库指定该值，以便使用仅在此兼容级别支持的功能（也就是说，增大了用于包含字符串数据的维度属性或非重复计数度量值的字符串存储空间）。<br /><br /> `CompatibilityLevel`如果数据库设置为 `1100` 获取附加属性， `StringStoresCompatibilityLevel` 则可以为分区和维度选择其他字符串存储。|  
  
> [!WARNING]  
>  将数据库兼容级别设置为更高级别是不可逆的。 将兼容级别提高到后 `1100` ，必须继续在更高版本的服务器上运行数据库。 不能回滚到 `1050` 。 不能 `1100` 在早于或的服务器版本上附加或还原数据库 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。  
  
## <a name="prerequisites"></a>先决条件  
 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引入数据库兼容级别。 你必须具有 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或更高版本才能查看或设置数据库兼容级别。  
  
 数据库不能为本地多维数据集。 本地多维数据集不支持 `CompatibilityLevel` 属性。  
  
 该数据库必须已在以前的版本（SQL Server 2008 R2 或更早版本）中创建，然后附加或还原到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或更高版本的服务器。 部署到 SQL Server 2012 的数据库已在 `1100` 级别，无法降级到更低级别。  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>确定多维数据库的现有数据库兼容级别  
 查看或修改数据库兼容级别的唯一方法就是通过 XMLA。 您可以在 SQL Server Management Studio 中查看或修改指定您的数据库的 XMLA 脚本。  
  
 如果在数据库的 XMLA 定义中搜索属性 `CompatibilityLevel`，没有任何结果，则该数据库很可能已位于 `1050` 级别。  
  
 下一节中提供了有关查看和修改 XMLA 脚本的说明。  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中设置数据库兼容级别  
  
1.  在提高兼容级别之前，请备份该数据库，以备稍后您要撤消更改。  
  
2.  使用 SQL Server Management Studio，连接到承载数据库的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器。  
  
3.  右键单击数据库名称，指向“编写数据库脚本为”****，指向“ALTER to”****，然后选择“新查询编辑器窗口”****。 数据库的 XMLA 表示形式将在新窗口中打开。  
  
4.  复制以下 XML 元素：  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  将其粘贴到 `</Annotations>` 结尾元素之后、 `<Language>` 元素之前。 XML 应类似以下示例：  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  保存文件。  
  
7.  若要运行脚本，请在“查询”菜单上单击 **“执行”** ，或按 F5。  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>要求相同兼容级别的支持的操作  
 以下操作要求源数据库共享相同的兼容级别。  
  
1.  只有在两个不同的数据库共享相同的兼容级别时，才支持从这两个不同的数据库合并分区。  
  
2.  使用来自其他数据库的链接维度要求相同的兼容级别。 例如，如果要使用数据库中的数据库的链接维度 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ，则必须将 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 数据库移植到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 服务器，并将兼容级别设置为 `1100` 。  
  
3.  仅对于共享相同版本和数据库兼容级别的服务器，才支持同步服务器。  
  
## <a name="next-steps"></a>后续步骤  
 在增加了数据库兼容级别之后，可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中设置 `StringStoresCompatibilityLevel` 属性。 这样将增大度量值和维度的字符串存储空间。 有关此功能的详细信息，请参阅 [配置维度和分区的字符串存储](configure-string-storage-for-dimensions-and-partitions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [备份、还原和同步数据库 (XMLA)](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
