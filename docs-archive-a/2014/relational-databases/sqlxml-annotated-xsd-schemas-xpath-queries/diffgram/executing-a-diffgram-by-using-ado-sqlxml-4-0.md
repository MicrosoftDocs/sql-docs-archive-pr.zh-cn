---
title: 使用 ADO 执行 DiffGram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
author: rothja
ms.author: jroth
ms.openlocfilehash: b96db25fd46b1ecbbc15c8acd912743e5560f178
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587294"
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>使用 ADO 执行 DiffGram (SQLXML 4.0)
  该 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 应用程序使用 ADO 建立与 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的连接，然后执行 DiffGram。 在该应用程序中，DiffGram 和 XSD 架构存储在文件中。 该应用程序从指定的文件加载 DiffGram。 可以使用[DiffGram 示例](diffgram-examples-sqlxml-4-0.md)中所述的任何 diffgram (和关联的 XSD 架构) 。  
  
 以下是示例应用程序的过程：  
  
-   **Conn**对象 (**adodb.recordset。连接**) 与在特定服务器上运行的 SQL Server 实例建立连接。  
  
-   **Cmd**对象 (在已建立的连接上执行**adodb.recordset) 。**  
  
-   将命令方言设置为 DBGUID_MSSQLXML。  
  
-   DiffGram 将从文件复制到命令流 (**strmIn**) 。  
  
-   命令的输出流设置为**StrmOut**对象 (**adodb.recordset。流式传输**) 可接收任何返回的数据。  
  
-   当使用 SQLOLEDB 访问接口时，默认情况下，您将获取 Sqlxmlx.dll 提供的 Microsoft SQLXML 功能。 若要将 Sqlxml4.dll 与 SQLOLEDB 提供程序一起使用，必须在 SQLOLEDB 提供程序**连接**对象上将**sqlxml Version**属性设置为**sqlxml。**  
  
-   执行该命令 (DiffGram)。  
  
 以下代码为示例应用程序。  
  
> [!NOTE]  
>  在该代码中，必须在连接字符串中提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>测试 DiffGram  
  
1.  对于计算机上的文件夹，请从[DiffGram 示例](diffgram-examples-sqlxml-4-0.md)中的一个示例复制其中一个 diffgram 和对应的 XSD 架构。  
  
2.  打开 Visual Basic 并创建标准 EXE 项目。  
  
3.  将这些引用添加到项目中：  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  在 "工具箱" 中，单击 "**命令**按钮"，然后在窗体上绘制一个按钮。  
  
5.  双击该按钮编辑代码，并添加本主题中提供的应用程序代码。  
  
6.  编辑代码以指定 DiffGram 和 XSD 文件名， 并根据需要编辑连接字符串。  
  
7.  执行应用程序。 执行结果取决于您执行的 DiffGram。  
  
  
