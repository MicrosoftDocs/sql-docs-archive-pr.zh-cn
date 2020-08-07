---
title: 管理 (SQL Server 数据挖掘外接程序) 的模型 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, importing
- mining models, deleting
- mining models, managing
- mining models, training
- mining models, processing
- mining models, exporting
ms.assetid: c11380f0-7c24-4668-9cdf-9c53e4aff665
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5f4b5961ec79bb949bf7fa5f53a980f066e81379
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589331"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>管理模型（SQL Server 数据挖掘外接程序）
  ![“数据挖掘”功能区中的“管理模型”按钮](media/dmc-manage.gif "“数据挖掘”功能区中的“管理模型”按钮")  
  
 利用 "**管理模型**" 对话框，您可以与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 当前连接到的服务器中存储的现有挖掘模型和挖掘结构进行交互。 您还可以查看和管理已在当前会话期间创建的临时结构和模型。 如果您同时使用会话模型和存储在服务器上的模型，则这两种模型在该对话框中都是可见的。  
  
## <a name="using-the-manage-models-wizard"></a>使用管理模型向导  
 单击 "**管理模型**" 时，将打开 "**管理挖掘结构和模型**" 对话框，为管理现有数据挖掘模型和结构提供以下功能的访问权限：  
  
-   重命名挖掘模型或结构  
  
-   删除挖掘模型或结构  
  
-   清除挖掘模型或结构  
  
-   使用新数据或现有数据处理挖掘结构  
  
-   导出或导入挖掘模型或结构  
  
> [!NOTE]  
>  您不能使用此对话框创建查询或模型。 若要创建新的挖掘结构，请使用 Excel 数据挖掘客户端中提供的向导之一，或使用**数据挖掘查询高级编辑器**。  
  
### <a name="requirements"></a>要求  
 若要管理数据挖掘模型，您必须首先创建到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的连接。 连接是必需的，即使处理的是存储在临时文件中的会话模型也需要连接。 有关如何创建或更改连接的详细信息，请参阅[连接到源数据 &#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 如果所连接到的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例不包含任何现有数据挖掘结构或数据挖掘模型，您可以使用此外接程序提供的向导和其他工具来创建它们。 您还可以通过使用**数据挖掘模型高级编辑器**来创建新模型。  
  
## <a name="see-also"></a>另请参阅  
 [记录挖掘模型 &#40;Excel 数据挖掘外接程序&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [&#40;Excel 数据挖掘外接程序部署和缩放挖掘模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
