---
title: 用户定义函数和存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- stored procedures [ADOMD.NET]
- ADOMD.NET, user defined functions
- user defined functions [ADOMD.NET]
- ADOMD.NET, UDFs
- ADOMD.NET, stored procedures
ms.assetid: 07e8aa47-37d4-4bbc-8bff-49e422d12897
author: minewiskan
ms.author: owend
ms.openlocfilehash: a49aa41d158bf2c9fd1ebb1a711d6ff35c0df98b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682431"
---
# <a name="user-defined-functions-and-stored-procedures"></a>用户定义函数和存储过程
  对于 ADOMD.NET 服务器对象，您可以 (UDF) 或存储过程创建用户定义的函数，以与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器中的元数据和数据进行交互。 这些进程内方法是通过多维表达式 (MDX) 或数据挖掘扩展插件 (DMX) 语句调用的，可以提供附加功能而不会有网络通信的延迟。  
  
## <a name="udf-examples"></a>UDF 示例  
 UDF 是一种可在 MDX 或 DMX 语句上下文中调用的方法，可具有任意数目的参数，并可返回任意类型的数据。  
  
 使用 MDX 创建的 UDF 与用 DMX 创建的 UDF 类似。 主要区别在于， [microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))对象的某些属性（如[AdomdServer *](/previous-versions/sql/sql-server-2014/ms137081(v=sql.120))和 CurrentCube * 属性）仅适用于一种脚本语言或另一种语言的属性，例如 microsoft.analysisservices.sharepoint.integration.dll * 和 AdomdServer [*](/previous-versions/sql/sql-server-2014/ms137178(v=sql.120))属性。  
  
 下面的示例演示如何使用 UDF 返回节点说明、筛选元组并对元组应用筛选器。  
  
### <a name="returning-a-node-description"></a>返回节点说明  
 下面的示例创建一个返回指定节点的节点说明的 UDF。 该 UDF 使用它正在其中运行的当前上下文，并使用 DMX FROM 子句从当前挖掘模型检索节点。  
  
```  
public string GetNodeDescription(string nodeUniqueName)  
{  
   return Context.CurrentMiningModel.GetNodeFromUniqueName(nodeUniqueName).Description;  
}  
```  
  
 部署后，下面的 DMX 表达式（检索最有可能的预测节点）就可以调用上面的 UDF 示例了。 节点的说明包含描述组成预测节点的条件的信息。  
  
```  
select Cluster(), SampleAssembly.GetNodeDescription( PredictNodeId(Cluster()) ) FROM [Customer Clusters]  
```  
  
### <a name="returning-tuples"></a>返回元组  
 下面的示例使用一个集和一个返回计数，它从该集中随机检索元组，并返回一个最终子集：  
  
```  
public Set RandomSample(Set set, int returnCount)  
{  
   //Return the original set if there are fewer tuples  
   //in the set than the number requested.  
   if (set.Tuples.Count <= returnCount)  
      return set;  
  
   System.Random r = new System.Random();  
   SetBuilder returnSet = new SetBuilder();  
  
   //Retrieve random tuples until the return set is filled.  
   int i = set.Tuples.Count;  
   foreach (Tuple t in set.Tuples)  
   {  
      if (r.Next(i) < returnCount)  
      {  
         returnCount--;  
         returnSet.Add(t);  
      }  
      i--;  
      //Stop the loop if we have enough tuples.  
      if (returnCount == 0)  
         break;  
   }  
   return returnSet.ToSet();  
}  
```  
  
 下面的 MDX 示例中调用了上面的示例。 在此 MDX 示例中，将从**艾德公司**数据库中检索五个随机状态或省/自治区。  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
### <a name="applying-a-filter-to-a-tuple"></a>对元组应用筛选器  
 下面的示例中定义了一个 UDF，该 UDF 使用一个集，并使用 Expression 对象对集中的每个元组应用筛选器。 所有符合筛选条件的元组都将被添加到返回的集中。  
  
 [!code-csharp[Adomd.NetServer#FilterSet](../../snippets/csharp/SQL14/adomd.net/adomd.netserver/cs/class1.cs#filterset)]  
  
 下面的 MDX 示例调用了上面的示例，该 MDX 示例从集中筛选名称以“A”开头的市县。  
  
```  
Select Measures.Members on Rows,  
SampleAssembly.FilterSet([Customer].[Customer Geography].[City], "[Customer].[Customer Geography].[City].CurrentMember.Name < 'B'") on Columns  
From [Adventure Works]  
```  
  
## <a name="stored-procedure-example"></a>存储过程示例  
 在下面的示例中，基于 MDX 的存储过程使用 AMO 来为 Internet 销售创建分区（如果需要）。  
  
 [!code-csharp[Adomd.NetServer#CreateInternetSalesMeasureGroupPartitions](../../snippets/csharp/SQL14/adomd.net/adomd.netserver/cs/class1.cs#createinternetsalesmeasuregrouppartitions)]  
  
  
