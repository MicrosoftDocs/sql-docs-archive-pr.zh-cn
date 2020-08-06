---
title: 在部署项目后设置参数值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c9dcca4d-f1a0-45ec-b078-f4d372589baf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 39572594e429b61de0641c6e6929e84105138f1f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694034"
---
# <a name="set-parameter-values-after-the-project-is-deployed"></a>在部署项目后设置参数值
  通过部署向导，您可以在将项目部署到目录时设置服务器默认参数值。 在您的项目处于目录中后，您可以使用 SQL Server Management Studio (SSMS) 对象资源管理器或 Transact-SQL 来设置服务器默认值。  
  
### <a name="to-set-server-defaults-with-ssms-object-explorer"></a>使用 SSMS 对象资源管理器设置服务器默认值：  
  
1.  选择并右键单击“集成服务”节点下的项目。****  
  
2.  单击 **“属性”** 以便打开 **“项目属性”** 对话框窗口。  
  
3.  通过在 **“选择页”** 之下单击 **“参数”**，打开参数页。  
  
4.  在 **“参数”** 列表中选择所需参数。 注意： **“容器”** 列将帮助区分项目参数和包参数。  
  
5.  在 **“值”** 列中，指定所需的服务器默认参数值。  
  
 若要使用 TRANSACT-SQL 设置服务器默认值，请使用 [catalog.set_object_parameter_value（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database)存储过程。 若要查看当前服务器默认值，请查询 [catalog.object_parameters（SSISDB 数据库）](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)视图。 若要清除服务器默认值，请使用 [catalog.clear_object_parameter_value（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database)存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSIS&#41; 参数 Integration Services](integration-services-ssis-package-and-project-parameters.md)  
  
  
