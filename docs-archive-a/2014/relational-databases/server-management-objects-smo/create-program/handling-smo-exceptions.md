---
title: 处理 SMO 异常 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
author: stevestein
ms.author: sstein
ms.openlocfilehash: f4ae9e475a019c9bf874ee3f8365f3f3ac8e19d5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590682"
---
# <a name="handling-smo-exceptions"></a>处理 SMO 异常
  在托管代码中，如果出现错误，便会引发异常。 SMO 方法和属性不在返回值中报告成功或失败信息。 相反，可以通过异常处理程序捕获和处理异常。  
  
 SMO 中存在多种不同的异常类。 可以从提供与异常相关的文字信息的异常属性（例如 `Message` 属性）中提取出关于异常的信息。  
  
 异常处理语句是特定于编程语言的。 例如，在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 中，该语句为 `Catch` 语句。  
  
## <a name="inner-exceptions"></a>内部异常  
 异常可能是常规异常，也可能是特定异常。 常规异常包含一组特定异常。 可使用几条 `Catch` 语句处理预计可能出现的错误，并使用常规异常处理代码处理其余错误。 通常，异常按照级联顺序发生。 很多情况下，SMO 异常可能是由 SQL 异常导致的。 检测是否为这种情况的方法便是连续使用 `InnerException` 属性确定导致最终顶级异常的原始异常。  
  
> [!NOTE]  
>  此 `SQLException` 异常在**SqlClient**命名空间中声明。  
  
 ![显示级别的关系图](../../../database-engine/dev-guide/media/exception-flow.gif "显示级别的关系图")  
  
 此图显示了异常通过各应用程序层的流程。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual studio .net 中创建 Visual C&#35; SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)或[在 visual Studio .net 中创建 Visual Basic SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)。  
  
## <a name="catching-an-exception-in-visual-basic"></a>在 Visual Basic 中捕获异常  
 此代码示例演示如何使用 `Try...Catch...Finally`[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 语句捕获 SMO 异常。 所有 SMO 异常的类型均为 SmoException，并且均列出在 SMO 引用中。 显示内部异常的顺序的目的在于揭示错误的根源。 有关详细信息，请参阅 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET 文档。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBExceptions1](SMO How to#SMO_VBExceptions1)]  -->  
  
## <a name="catching-an-exception-in-visual-c"></a>在 Visual C# 中捕获异常  
 此代码示例演示如何使用 `Try...Catch...Finally` Visual C# 语句捕获 SMO 异常。 所有 SMO 异常的类型均为 SmoException，并且均列出在 SMO 引用中。 显示内部异常的顺序的目的在于揭示错误的根源。 有关详细信息，请参阅 Visual C# 文档。  
  
```  
{   
//This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace to be included.   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.   
//Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.   
op = new Operator(srv.JobServer, "Test_Operator");   
op.Create();   
//Start exception handling.   
try {   
    //Create the operator again to cause an SMO exception.   
    OperatorCategory opx;   
    opx = new OperatorCategory(srv.JobServer, "Test_Operator");   
    opx.Create();   
}   
//Catch the SMO exception   
catch (SmoException smoex) {   
    Console.WriteLine("This is an SMO Exception");   
   //Display the SMO exception message.   
   Console.WriteLine(smoex.Message);   
   //Display the sequence of non-SMO exceptions that caused the SMO exception.   
   Exception ex;   
   ex = smoex.InnerException;   
   while (!object.ReferenceEquals(ex.InnerException, (null))) {   
      Console.WriteLine(ex.InnerException.Message);   
      ex = ex.InnerException;   
    }   
    }   
   //Catch other non-SMO exceptions.   
   catch (Exception ex) {   
      Console.WriteLine("This is not an SMO exception.");   
}   
}  
```  
  
  
