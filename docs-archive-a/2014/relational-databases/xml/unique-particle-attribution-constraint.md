---
title: 唯一粒子归属约束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
f1_keywords:
- unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
author: rothja
ms.author: jroth
ms.openlocfilehash: 7416aa4ea14539f3bf633207768783aa439ec818
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682759"
---
# <a name="unique-particle-attribution-constraint"></a>唯一粒子归属约束
  在 XSD 中，复杂内容模型受唯一粒子归属 (UPA) 约束规则的约束。 此规则要求实例文档中的每个元素明确地完全对应于其父级的内容模型中的一个 `<xsd:element>` 或 `<xsd:any>` 粒子。 任何包含具有可能不明确的内容模型的类型的架构都将被拒绝。  
  
 导致不明确的最常见原因是具有可变出现范围（例如 minOccurs < maxOccurs）的 `<xsd:any>` 通配符字符和粒子。 例如，以下内容模型是不明确的，因为 <`e1`> 元素既可以与 `<xsd:element>` 元素匹配，也可以与 `<xsd:any>` 元素匹配。  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
            <xsd:element name="e1"/>  
            <xsd:any namespace="##any"/>  
        </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 以下内容模型也是不明确的：  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:sequence>  
            <xsd:element name="e1" maxOccurs="2"/>  
            <xsd:element name="e2" minOccurs="0"/>  
            <xsd:element name="e1"/>  
        </xsd:sequence>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 虽然可以明确验证像 `<root><e1/><e2/><e1/></root>` 这样的文档，但无法明确验证像 `<root><e1/><e1/></root>` 这样的文档，因为不清楚第二个 `<xsd:element>` 对应于哪一个 `<e1/>` 。 即使可以明确验证某些文档，此架构也将被拒绝，因为这些文档有可能是不明确的。  
  
 请注意，对于有效的内容模型，必须能够在不向下查看的情况下明确验证任何实例。 例如，请思考下面的内容模型：  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e2"/>  
           </xsd:sequence>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e3"/>  
           </xsd:sequence>  
       </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 对于像 `<root><e1/><e3/></root>`这样的文档，序列 `<e1/><e3/>` 明确与第二个 `<xsd:sequence>`匹配。 但是，由于在不向下查看 `<xsd:element>` 情况下无法确定 `<e1/>` 所对应的 `<e3/>`，因此该内容模型违反了 UPA 约束规则。  
  
## <a name="finding-more-information"></a>查找详细信息  
 以下文档由 World Wide Web 联合会 (W3C) 发布，其中包含唯一粒子归属约束的技术说明：  
  
 “XML 架构第 1 部分：结构第二版 - W3C 已修正的提议推荐”：  
  
-   第 3.8.6 节：模型组架构组件的相关约束  
  
-   附录 H：唯一粒子归属约束（非标准）的分析  
  
 若要查看该文档，请访问 [http://www.w3.org/TR/xmlschema-1](https://go.microsoft.com/fwlink/?linkid=48881)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 架构集合 (SQL Server)](xml-schema-collections-sql-server.md)  
  
  
