---
title: " (SQLXML 托管类) | 执行 XPath 查询 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], SQLXML Managed Classes
- queries [SQLXML], SQLXML Managed Classes
- Managed Classes [SQLXML], executing XPath queries
- mapping schema [SQLXML], XPath queries
- SQLXML Managed Classes, executing XPath queries
ms.assetid: 8bef4c4d-bf0e-4236-a875-fd7d3e058396
author: rothja
ms.author: jroth
ms.openlocfilehash: d8f5fd2612a0992f18e0b7f32c749c352d29d2b3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576604"
---
# <a name="executing-xpath-queries-sqlxml-managed-classes"></a>执行 XPath 查询（SQLXML 托管类）
  该示例说明如何针对映射架构执行 XPath 查询。  
  
 考虑该架构：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Con" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
     <xsd:attribute name="ContactID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 该 C# 应用程序针对此架构 (MySchema.xml) 执行 XPath 查询。  
  
> [!NOTE]  
>  在代码中，必须在连接字符串中提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
  
      public static int testXPath()  
      {  
         Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "Con";  
         cmd.CommandType = SqlXmlCommandType.XPath;  
         cmd.RootTag = "ROOT";  
         cmd.SchemaPath = "MySchema.xml";  
         strm = cmd.ExecuteStream();  
         using (StreamReader sr = new StreamReader(strm)){  
            Console.WriteLine(sr.ReadToEnd());  
         }  
         return 0;  
      }  
      public static int Main(String[] args)  
      {  
         testXPath();  
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  确保已在计算机上安装了 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
2.  将在该示例中提供的 XSD 架构 (MySchema.xml) 保存到某个文件夹中。  
  
3.  将此示例中提供的 c # 代码 (DocSample.cs) 保存到存储架构的相同文件夹中。 （如果将文件存储在其他文件夹中，则必须编辑代码并为映射架构指定相应的目录路径。）  
  
4.  编译代码。 若要在命令提示符下编译此代码，请使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     这将创建一个可执行文件 (DocSample.exe)。  
  
5.  在命令提示符下，执行 DocSample.exe。  
  
  
