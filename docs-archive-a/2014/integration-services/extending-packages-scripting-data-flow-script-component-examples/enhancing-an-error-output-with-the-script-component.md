---
title: 使用脚本组件增强错误输出 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 18637aa1e147ce989645ae859681929f4d0c438a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590924"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>使用脚本组件增强错误输出
  默认情况下，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误输出中的另外两列 ErrorCode 和 ErrorColumn 只包含表示错误号的数值代码以及出现错误的列的 ID。 如果没有相应的错误说明，这些数值没有多大用处。  
  
 本主题介绍如何使用脚本组件向数据流中的现有错误输出数据中添加错误说明列。 示例使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 接口的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法添加与特定预定义 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误代码对应的错误说明，该接口通过脚本组件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 属性提供。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个数据流任务和多个包的组件，请考虑以此脚本组件示例中的代码为基础，创建自定义数据流组件。 有关详细信息，请参阅 [开发自定义数据流组件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>示例  
 下面显示的示例使用一个配置为转换的脚本组件向数据流中的现有错误输出数据中添加错误说明列。  
  
 有关如何配置脚本组件以用作数据流中的转换的详细信息，请参阅[使用脚本组件创建同步转换](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)和[使用脚本组件创建异步转换](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>配置此脚本组件示例  
  
1.  创建新脚本组件之前，先配置数据流中的上游组件，以便在错误或截断出现时将行重定向到上游组件的错误输出。 出于测试目的，可能希望以确保将发生错误的方式来配置组件，例如，在两个将发生查找失败的表之间配置一个查找转换。  
  
2.  向数据流设计器图面添加新的脚本组件并将其配置为转换。  
  
3.  将错误输出从上游组件连接到新脚本组件。  
  
4.  打开“脚本转换编辑器”****，在“脚本”**** 页中，为 **ScriptLanguage** 属性选择脚本语言。  
  
5.  单击“编辑脚本”打开 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE，并添加下面的示例代码****。  
  
6.  关闭 VSTA。  
  
7.  在 "脚本转换编辑器" 的 "**输入列**" 页中，选择 ErrorCode 列。  
  
8.  在 "**输入和输出**" 页中，添加 `String` 名为**ErrorDescription**的类型的新输出列。 将新列的默认长度提高到 255 以支持长消息。  
  
9. 关闭“脚本转换编辑器”****。  
  
10. 将脚本组件的输出附加到合适的目标。 对于即席测试，平面文件目标是最容易配置的。  
  
11. 运行包。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  Row.ErrorDescription = _  
    Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
  Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
    }  
}  
  
```  
  
![Integration Services 图标 (小型) ](../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [数据中的错误处理](../data-flow/error-handling-in-data.md)   
 [在数据流组件中使用错误输出](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [使用脚本组件创建同步转换](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
