---
title: " (SQLXML 托管类) | 在客户端处理 XMLMicrosoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- processing XML on client side [SQLXML]
- client-side XML formatting
- Managed Classes [SQLXML], client-side XML formatting
- SQLXML Managed Classes, client-side XML formatting
- ClientSideXml property
ms.assetid: 5e7ecf18-66fc-49ff-bc50-83635cd7ac0b
author: rothja
ms.author: jroth
ms.openlocfilehash: fb90f7c5c823c750b64f47d0c9df9551b9f857b5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577495"
---
# <a name="processing-xml-on-the-client-side-sqlxml-managed-classes"></a>在客户端处理 XML（SQLXML 托管类）
  此示例演示如何使用 ClientSideXml 属性。 应用程序在服务器上执行存储过程。 在客户端对存储过程的结果（一个有两列的行集）进行处理，以产生 XML 文档。  
  
 下面的 GetContacts 存储过程将返回用户的**名字**和**姓氏**。 AdventureWorks 数据库中的 Contact 表。  
  
```  
USE AdventureWorks  
CREATE PROCEDURE GetContacts @LastName varchar(20)  
AS  
SELECT FirstName, LastName  
FROM   Person.Contact  
WHERE LastName = @LastName  
Go  
```  
  
 此 c # 应用程序执行存储过程，并在指定 CommandText 值中指定 FOR XML AUTO 选项。 在应用程序中，SqlXmlCommand 对象的 ClientSideXml 属性设置为 true。 这将允许执行预先存在的存储过程，然后由存储过程返回行集，并在客户端上对它执行 XML 转换。  
  
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
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.ClientSideXml = true;  
         cmd.CommandText = "EXEC GetContacts ? FOR XML NESTED";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         using (Stream strm = cmd.ExecuteStream())   
         {  
            using (StreamReader sr = new StreamReader(strm))  
                  {  
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
  
 若要测试该示例，必须在计算机上安装 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  创建存储过程。  
  
2.  将此示例中提供的 C# 代码 (DocSample.cs) 保存在某个文件夹中。 编辑代码，以指定合适的登录和密码信息。  
  
3.  编译代码。 若要在命令提示符下编译此代码，请使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     这将创建一个可执行文件 (DocSample.exe)。  
  
4.  在命令提示符下，执行 DocSample.exe。  
  
  
