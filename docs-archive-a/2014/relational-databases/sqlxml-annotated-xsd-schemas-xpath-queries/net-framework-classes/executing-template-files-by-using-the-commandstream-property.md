---
title: 使用 CommandStream 属性执行模板文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- CommandStream property
ms.assetid: 55c564e3-56d1-4d85-bcaa-703e2905dd57
author: rothja
ms.author: jroth
ms.openlocfilehash: c57a2ab2f3780a8bc75b53b0cceeee0799fcfcc2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576606"
---
# <a name="executing-template-files-by-using-the-commandstream-property"></a>使用 CommandStream 属性执行模板文件
  此示例演示如何使用 SqlXmlCommand 对象的 CommandStream 属性来指定由 SQL 或 XPath 查询组成的模板文件。 在此应用程序中，将为命令文件打开 FileStreamobject，并将文件流指定为执行的 CommandStream。  
  
 在下面的示例中，CommandType 属性被指定为 SqlXmlCommandType (而不是 TemplateFile) 。  
  
 下面是示例 XML 模板：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 这是示例 C# 应用程序。 若要测试该应用程序，请保存模板 (TemplateFile.xml)，然后执行该应用程序。 应用程序将执行在 XML 模板中指定的查询，并在屏幕上显示所生成的 XML 文档。  
  
> [!NOTE]  
>  在代码中，必须在连接字符串中提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         MemoryStream ms = new MemoryStream();  
         StreamWriter sw = new StreamWriter(ms);  
         ms.Position = 0;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandStream = new FileStream("TemplateFile.xml", FileMode.Open, FileAccess.Read);  
         cmd.CommandType = SqlXmlCommandType.Template;  
         using (Stream strm = cmd.ExecuteStream())  
         {  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;        
      }  
  
      public static int Main(String[] args)  
      {  
         testParams();     
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  将该示例中提供的 XML 模板 (TemplateFile.xml) 保存在某个文件夹中。  
  
2.  将此示例中提供的 c # 代码 (DocSample.cs) 保存到存储架构的相同文件夹中。 （如果将文件存储在其他文件夹中，则必须编辑代码并为映射架构指定相应的目录路径。）  
  
3.  编译代码。 若要在命令提示符下编译此代码，请使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     这将创建一个可执行文件 (DocSample.exe)。  
  
4.  在命令提示符下，执行 DocSample.exe。  
  
  
