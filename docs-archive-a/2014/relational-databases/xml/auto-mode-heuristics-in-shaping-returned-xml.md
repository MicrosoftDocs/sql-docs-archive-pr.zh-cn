---
title: 返回的 XML 成形过程中的 AUTO 模式试探方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
author: rothja
ms.author: jroth
ms.openlocfilehash: 7a64cda8989e1e45d4ad869f8883e1c9d65f4b7e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577442"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>返回的 XML 成形过程中的 AUTO 模式试探方法
  AUTO 模式根据查询决定返回的 XML 的形式。 在决定嵌套元素的方式时，AUTO 模式试探方法会比较相邻行中的列值。 **ntext**、 **text**、 **image**和 **xml**类型以外的所有类型的列都会进行比较。 **(n)varchar(max)** 和 **varbinary(max)** 类型的列会进行比较。  
  
 下面的示例说明了确定生成的 XML 的形式的 AUTO 模式试探方法：  
  
```  
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
FOR XML AUTO  
ORDER BY T1.Id  
```  
  
 如果未指定表 T1 的键，若要确定新 <`T1`> 元素的开始位置，需要比较 T1 中除 **ntext** **text** **image** 和 **xml** 类型以外的所有列的值。 接下来，假定 **Name** 列的数据类型为 **nvarchar(40)** ，SELECT 语句将返回如下行集：  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 AUTO 模式试探方法将比较表 T1 的所有值（Id 列和 Name 列）。 因为前两行的 Id 列和 Name 列具有相同的值，所以向结果中添加了一个具有两个 \<T2> 子元素的 \<T1> 元素。  
  
 下面是返回的 XML：  
  
```  
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 现在，假定 Name 列是 **text** 类型。 AUTO 模式试探方法不比较此类型的值， 而是认为这些值不相同。 这将产生如下所示的 XML 生成结果：  
  
```  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="2" />  
</T1>  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
  <T2 Id="4" />  
</T1>  
```  
  
## <a name="see-also"></a>另请参阅  
 [将 AUTO 模式与 FOR XML 一起使用](use-auto-mode-with-for-xml.md)  
  
  
