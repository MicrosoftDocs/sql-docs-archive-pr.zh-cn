---
title: timestamp 数据类型的 FOR XML 支持 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type
ms.assetid: 4e1920e1-e7a4-4069-965e-3f6039a6099e
author: rothja
ms.author: jroth
ms.openlocfilehash: cbc37cc396922631a958fff270032e669387d72d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694382"
---
# <a name="for-xml-support-for-the-timestamp-data-type"></a>timestamp 数据类型的 FOR XML 支持
  在 FOR XML 转换中， **timestamp** 类型值被视为 **varbinary(8)** 数据，并且始终为 Base64 编码。 XSD 架构或 XDR 架构反映此类型（如果请求）。  
  
```  
drop table t  
go  
create table t  
(c1 int,  
 c2 timestamp)  
go  
  
insert t values(1, null)  
go  
select * from t  
for xml auto, xmldata  
go  
```  
  
 结果如下：  
  
```  
<Schema name="Schema1"   
        xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="t" content="empty" model="closed">  
    <AttributeType name="c1" dt:type="i4" />  
    <AttributeType name="c2" dt:type="bin.base64" />  
    <attribute type="c1" />  
    <attribute type="c2" />  
  </ElementType>  
</Schema>  
<t xmlns="x-schema:#Schema1" c1="1" c2="AAAAAAAAH04=" />  
```  
  
## <a name="see-also"></a>另请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](for-xml-support-for-various-sql-server-data-types.md)  
  
  
