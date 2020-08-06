---
title: 示例：重命名 &lt;row&gt; 元素 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: rothja
ms.author: jroth
ms.openlocfilehash: 39375fa125f451f21d936b3a6897b93928fa2f02
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577421"
---
# <a name="example-renaming-the-ltrowgt-element"></a>示例：重命名 &lt;row&gt; 元素
  对于结果集中的每一行，RAW 模式都生成一个元素 `<row>`。 您可以通过向 RAW 模式指定一个可选参数为该元素指定另一个名称，如该查询中所示。 该查询为行集中的每一行返回一个 <`ProductModel`> 元素。  
  
## <a name="example"></a>示例  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 结果如下： 由于查询中添加了 `ELEMENTS` 指令，因此，结果以元素为中心。  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>另请参阅  
 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)  
  
  
