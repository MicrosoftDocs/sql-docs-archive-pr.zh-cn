---
title: DQS 域支持的 SQL Server 和 SSIS 数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad79983f570beb4c789379b2b48682b358c34e1b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694138"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>DQS 域支持的 SQL Server 和 SSIS 数据类型
  SQL Server 和 SQL Server Integration Services (SSIS) 中有很多数据类型，但是只有四种数据类型用于 DQS 域：Date、Decimal、Integer 和 String。 并非所有 SQL Server 和 SSIS 数据类型在 DQS 中都受支持。 仅当源数据类型在 DQS 中受支持且与 DQS 域数据类型匹配时，才能将源数据映射到 DQS 域来执行数据质量活动。 本主题提供有关支持的可映射到 DQS 中四种域数据类型之一的 SQL Server 和 SSIS 数据类型信息。  
  
> [!NOTE]  
>  在 .xlsx 和 .xls 文件中，源列的数据类型由前八行中最主要的数据类型确定。 如果某一单元不符合该数据类型，将向它提供 null 值。 同样，在 .csv 文件中，源列的数据类型由前八行中最主要的数据类型确定。  
  
##  <a name="supported-sql-server-data-types"></a><a name="SQLServer"></a>支持的 SQL Server 数据类型  
 下表提供有关对于每种 DQS 域数据类型支持的 SQL Server 数据类型的信息：  
  
|DQS 域数据类型|支持的 SQL Server 数据类型|  
|--------------------------|------------------------------------|  
|日期|date|  
|小数|Decimal<br /><br /> FLOAT<br /><br /> money<br /><br /> numeric<br /><br /> real<br /><br /> smallmoney|  
|Integer|bigint<br /><br /> int<br /><br /> smallint<br /><br /> tinyint|  
|String|char<br /><br /> nchar<br /><br /> nvarchar<br /><br /> varchar|  
  
 其余 SQL Server 数据类型在 DQS 中不受支持。 有关所有 SQL Server 数据类型的信息，请参阅[数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)。  
  
##  <a name="supported-ssis-data-types"></a><a name="SSIS"></a>支持的 SSIS 数据类型  
 下表提供有关对于每种 DQS 域数据类型支持的 SSIS 数据类型的信息：  
  
|DQS 域数据类型|支持的 SSIS 数据类型|  
|--------------------------|------------------------------|  
|Date|DT_DATE|  
|小数|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 其余 SSIS 数据类型在 DQS 中不受支持。 有关所有 SSIS 数据类型的信息，请参阅 [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="see-also"></a>另请参阅  
 [管理域](../../2014/data-quality-services/managing-a-domain.md)  
  
  
