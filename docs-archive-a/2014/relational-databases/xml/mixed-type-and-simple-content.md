---
title: 混合类型和简单内容 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
author: rothja
ms.author: jroth
ms.openlocfilehash: eb46769ee4c4d635af36a3c50fda34e8e1801b34
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687559"
---
# <a name="mixed-type-and-simple-content"></a>混合类型和简单内容
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持将混合类型限制为简单内容。  
  
## <a name="example"></a>示例  
 在下面的 XML 架构集合中， `myComplexTypeA` 是可以清空的复杂类型。 即它的两个元素都将 `minOccurs` 设置为 0。 与在 `myComplexTypeB` 声明中一样，不支持将此限制为简单内容的尝试。 因此，下面的 XML 架构集合创建语句将失败：  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns"  
xmlns:ns1="http://ns1">  
  
    <complexType name="myComplexTypeA" mixed="true">  
        <sequence>  
            <element name="a" type="string" minOccurs="0"/>  
            <element name="b" type="string" minOccurs="0" maxOccurs="23"/>  
        </sequence>  
    </complexType>  
  
    <complexType name="myComplexTypeB">  
        <simpleContent>  
            <restriction base="ns:myComplexTypeA">  
                <simpleType>  
                    <restriction base="int">  
                        <minExclusive value="25"/>  
                    </restriction>  
                </simpleType>  
            </restriction>  
        </simpleContent>  
    </complexType>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
