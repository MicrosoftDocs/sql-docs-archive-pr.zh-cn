---
title: ) XMLA (处理错误和警告 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
author: minewiskan
ms.author: owend
ms.openlocfilehash: 07b88d800237e5b4b06af0c1ff11cbd0af846600
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580968"
---
# <a name="handling-errors-and-warnings-xmla"></a>处理错误和警告 (XMLA)
  如果 XML for Analysis (XMLA) [发现](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)或[执行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法调用未运行、运行成功但生成了错误或警告，或成功运行，但返回的结果包含错误，则需要进行错误处理。  
  
|错误|报告|  
|-----------|---------------|  
|XMLA 方法调用不能运行|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 返回包含失败详细信息的 SOAP 错误消息。<br /><br /> 有关详细信息，请参阅[处理 SOAP 错误](#handling_soap_faults)一节。|  
|方法调用运行成功，但生成了错误或警告|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在包含方法调用结果的[root](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)元素的[Messages](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)属性中，分别为每个错误或警告分别包含[错误](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)或[警告](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla)元素。<br /><br /> 有关详细信息，请参阅[处理错误和警告](#handling_errors_and_warnings)一节。|  
|方法调用运行成功，但结果中包含错误|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]`error` `warning` 在方法调用结果的相应[单元格或](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)[行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla)元素中，分别包含错误或警告的内联或元素。<br /><br /> 有关详细信息，请参阅[处理内联错误和警告](#handling_inline_errors_and_warnings)一节。|  
  
##  <a name="handling-soap-faults"></a><a name="handling_soap_faults"></a>处理 SOAP 错误  
 出现以下情况时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会返回 SOAP 错误：  
  
-   包含 XMLA 方法的 SOAP 消息格式不正确，或者无法由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例验证。  
  
-   出现与包含 XMLA 方法的 SOAP 消息有关的通信错误或其他错误。  
  
-   XMLA 方法未在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上运行。  
  
 XMLstartA 的 SOAP 错误代码以“XMLForAnalysis”开头，后跟一个句号和十六进制的 HRESULT 结果代码。 例如，错误代码“`0x80000005`”的格式为“`XMLForAnalysis.0x80000005`”。 有关 SOAP 错误格式的详细信息，请参阅“W3C 简单对象访问协议 (SOAP) 1.1. 中的 SOAP 错误”。  
  
### <a name="fault-code-information"></a>错误代码信息  
 下表显示了 SOAP 响应详细信息部分包含的 XMLA 错误代码信息。 这些列为 SOAP 错误详细信息部分中所包含的错误的属性。  
  
|列名称|类型|说明|允许为 Null<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|指示方法是成功还是失败的返回代码。 十六进制值必须转换为 `UnsignedInt` 值。|否|  
|`WarningCode`|`UnsignedInt`|指示警告条件的返回代码。 十六进制值必须转换为 `UnsignedInt` 值。|是|  
|`Description`|`String`|由生成错误的组件返回的错误或警告的文本和说明。|是|  
|`Source`|`String`|生成错误或警告的组件的名称。|是|  
|`HelpFile`|`String`|指向介绍错误或警告的“帮助”文件或主题的路径或 URL。|是|  
  
 <sup>1</sup>指示数据是否是必需的并且必须返回，或者数据是否是可选的，如果列不适用，则允许为空字符串。  
  
 下面列出了一个由于方法调用失败而出现的 SOAP 错误示例：  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling-errors-and-warnings"></a><a name="handling_errors_and_warnings"></a>处理错误和警告  
 如果运行某命令后出现以下情况，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在该命令的 `Messages` 元素中返回 `root` 属性：  
  
-   该方法本身没有失败，但在该方法调用成功后，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上出现了错误。  
  
-    实例在该命令成功后返回一个警告。  
  
  属性出现在  元素中包含的所有其他属性之后，该属性可包含一个或多个  元素。 而每个 `Message` 元素又可以包含一个 `error` 或 `warning` 元素，这些元素分别描述了指定命令产生的所有错误或警告。  
  
 有关属性中包含的错误和警告的详细信息 `Messages` ，请参阅[Messages 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)。  
  
### <a name="handling-errors-during-serialization"></a>处理序列化期间发生的错误  
 如果在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例已经开始序列化已成功运行命令的输出后发生错误，则会在错误发生时 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 返回不同命名空间中的[异常](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla)元素。  实例随后会关闭所有已打开的元素，以确保发送到客户端的 XML 文档为有效文档。 该实例还会返回包含错误说明的 `Messages` 元素。  
  
##  <a name="handling-inline-errors-and-warnings"></a><a name="handling_inline_errors_and_warnings"></a>处理内联错误和警告  
 如果 XMLA 方法本身没有失败，但在 XMLA 方法调用成功后，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上出现了特定于该方法返回结果中的数据元素的错误，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会为命令返回内联 `error` 或 `warning`。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]`error` `warning` 如果出现特定于单元格的问题或对使用 MDDataSet 数据类型的元素中包含的其他数据的问题（ `root` 如单元的安全性错误或格式设置错误）， [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla)则提供内联和元素。 在这类情况下，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在包含错误或警告的 `error` 或 `warning` 元素中返回 `Cell` 或 `row` 元素。  
  
 下面的示例说明了一个结果集，该结果集在 `Execute` 使用[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令从方法返回的行集中包含错误。  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
