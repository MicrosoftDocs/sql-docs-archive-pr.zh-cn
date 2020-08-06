---
title: 创建、更改和删除视图 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- views [SMO]
ms.assetid: 7d445c0e-77ef-4734-993b-e022de31df23
author: stevestein
ms.author: sstein
ms.openlocfilehash: fd8d75e413b1871ce4b8784f5087cb08ed08da73
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590677"
---
# <a name="creating-altering-and-removing-views"></a>创建、更改和删除视图
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 视图由 <xref:Microsoft.SqlServer.Management.Smo.View> 对象表示。  
  
 <xref:Microsoft.SqlServer.Management.Smo.View.TextBody%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.View> 属性可定义视图。 它与创建视图的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 语句等效。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual studio .net 中创建 VISUAL BASIC SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 visual Studio .Net 中创建 VISUAL C&#35; smo 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-view-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除视图  
 此代码示例显示如何使用内部联接创建两个表的视图。 该视图是使用文本模式创建的，因此必须设置 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 属性。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBViews1](SMO How to#SMO_VBViews1)]  -->  
  
## <a name="creating-altering-and-removing-a-view-in-visual-c"></a>在 Visual C# 中创建、更改和删除视图  
 此代码示例显示如何使用内部联接创建两个表的视图。 该视图是使用文本模式创建的，因此必须设置 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 属性。  
  
```csharp
{  
        //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a View object variable by supplying the parent database, view name and schema in the constructor.   
        View myview;   
        myview = new View(db, "Test_View", "Sales");   
        //Set the TextHeader and TextBody property to define the view.   
        myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS";   
        myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID";   
        //Create the view on the instance of SQL Server.   
        myview.Create();   
        //Remove the view.   
        myview.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-view-in-powershell"></a>在 PowerShell 中创建、更改和删除视图  
 此代码示例显示如何使用内部联接创建两个表的视图。 该视图是使用文本模式创建的，因此必须设置 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 属性。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a View object variable by supplying the parent database, view name and schema in the constructor.
$myview  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.View -argumentlist $db, "Test_View", "Sales"  
  
# Set the TextHeader and TextBody property to define the view.
$myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"  
$myview.TextBody ="SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"  
  
# Create the view on the instance of SQL Server.
$myview.Create()  
  
# Remove the view
$myview.Drop();  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.View>  
