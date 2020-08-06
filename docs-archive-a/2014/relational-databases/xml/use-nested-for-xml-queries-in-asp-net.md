---
title: 在 ASP.NET 中使用嵌套 FOR XML 查询 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], ASP.NET and
- nested FOR XML queries in ASP.NET
- ASP.NET [SQL Server]
ms.assetid: 691ac7dd-afc5-4760-932c-2b1dcd9394ed
author: rothja
ms.author: jroth
ms.openlocfilehash: 1218b4ad46f0d21d42ba480d68b29d7c39b03ea2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578744"
---
# <a name="use-nested-for-xml-queries-in-aspnet"></a>在 ASP.NET 中使用嵌套 FOR XML 查询
  在此示例中，ASP.NET 应用程序通过在 SQL Server 中执行存储过程将 XML 返回至浏览器。 该存储过程使用嵌套查询生成 XML。 [使用嵌套 AUTO 模式查询生成同级](generate-siblings-with-a-nested-auto-mode-query.md)主题中显示了一个类似的 SELECT 语句。 本示例演示了一种在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用嵌套的 FOR XML 查询来生成以元素为中心的 XML 的方法。  
  
## <a name="example"></a>示例  
  
```  
CREATE PROC GetSalesOrderInfo AS  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
      FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
      for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE, ELEMENTS)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
GO  
```  
  
 以下是 .aspx 应用程序。 它执行存储过程并在浏览器中返回 XML：  
  
```  
<%@LANGUAGE=C# Debug=true %>  
<%@import Namespace="System.Xml"%>  
<%@import namespace="System.Data.SqlClient" %><%  
Response.Expires = -1;  
Response.ContentType = "text/xml";  
%>  
  
<%  
using(System.Data.SqlClient.SqlConnection c = new System.Data.SqlClient.SqlConnection("Data Source=server;Database=AdventureWorks;Integrated Security=SSPI;"))  
using(System.Data.SqlClient.SqlCommand cmd = c.CreateCommand())  
{  
   cmd.CommandText = "GetSalesOrderInfo";  
   cmd.CommandType = CommandType.StoredProcedure;  
   cmd.Connection.Open();  
   System.Xml.XmlReader r = cmd.ExecuteXmlReader();  
   System.Xml.XmlTextWriter w = new System.Xml.XmlTextWriter(Response.Output);  
   w.WriteStartElement("Root");  
   r.MoveToContent();  
   while(! r.EOF)  
   {  
      w.WriteNode(r, true);  
   }  
   w.WriteEndElement();  
   w.Flush();  
}  
%>  
```  
  
##### <a name="to-test-the-application"></a>测试应用程序  
  
1.  在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中创建存储过程。  
  
2.  将 .aspx 应用程序 (GetSalesOrderInfo.aspx) 保存至 c:\inetpub\www 根目录中。  
  
3.   (执行应用程序 http://server/GetSalesOrderInfo.aspx) 。  
  
## <a name="see-also"></a>另请参阅  
 [使用嵌套 FOR XML 查询](use-nested-for-xml-queries.md)  
  
  
