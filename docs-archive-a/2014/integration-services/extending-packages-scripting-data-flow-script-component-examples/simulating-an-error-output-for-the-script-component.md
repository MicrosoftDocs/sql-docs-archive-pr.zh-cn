---
title: 模拟脚本组件的错误输出 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], error output
- error outputs [Integration Services], Script component
ms.assetid: f8b6ecff-ac99-4231-a0e7-7ce4ad76bad0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bed458ce378eb26cd863811b4974b5f39429e1b1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688036"
---
# <a name="simulating-an-error-output-for-the-script-component"></a>模拟脚本组件的错误输出
  虽然您无法在脚本组件中直接将输出配置为错误输出，以便自动处理错误行，但必要时可通过创建附加输出并在脚本中使用条件逻辑将行定向到此输出，以再现内置错误输出的功能。 您可能希望通过添加两个用于接收错误号以及出现错误的列的 ID 的附加输出列，以模拟内置错误输出的行为。  
  
 若要添加与特定预定义 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误代码对应的错误说明，可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 接口的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法，该接口可通过脚本组件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 属性提供。  
  
## <a name="example"></a>示例  
 下面的示例使用一个配置为具有两个同步输出的转换的脚本组件。 该脚本组件的目的是从 AdventureWorks 示例数据库中的地址数据中筛选错误行。 此虚构示例假设我们正在为一项针对北美客户的促销活动做准备，需要筛选出不在北美的地址。  
  
#### <a name="to-configure-the-example"></a>配置示例  
  
1.  创建新脚本组件之前，先创建一个连接管理器，并配置一个从 AdventureWorks 示例数据库选择地址数据的数据流源。 对于此示例，由于仅查看 CountryRegionName 列，所以只需使用 Person.vStateCountryProvinceRegion 视图，或通过联接 Person.Address、Person.StateProvince 和 Person.CountryRegion 表来选择数据。  
  
2.  向数据流设计器图面添加新的脚本组件并将其配置为转换。 打开“脚本转换编辑器”  。  
  
3.  在“脚本”  页中，将 **ScriptLanguage** 属性设置为要用于编写脚本代码的脚本语言。  
  
4.  单击“编辑脚本”打开   Tools for Applications (VSTA)[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
5.  在 `Input0_ProcessInputRow` 方法中，键入或粘贴如下所示的示例代码。  
  
6.  关闭 VSTA。  
  
7.  在“输入列”  页中，选择要在脚本转换中处理的列。 此示例仅使用 CountryRegionName 列。 您未选择的可用列将不进行任何更改，原封不动地在数据流中传递。  
  
8.  在 "**输入和输出**" 页上，添加一个新的第二个输出，并将其 `SynchronousInputID` 值设置为输入的 ID，这也是 `SynchronousInputID` 默认输出的属性的值。 将两个输出的 `ExclusionGroup` 属性都设置为同一非零值（例如 1），以指示每一行都将仅定向到两个输出中的一个。 以不同名称为新的错误输出命名，如“MyErrorOutput”。  
  
9. 向新错误输出中添加其他输出列，以捕获所需的错误信息，其中包括错误代码、出现错误的列的 ID，可能还有错误说明。 此示例将创建新列：ErrorColumn 和 ErrorMessage。 若要在自己的实现中捕获预定义的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误，请确保为错误号添加了 ErrorCode 列。  
  
10. 记下脚本组件将查找其错误情况的一个或多个输入列的 ID 值。 本示例使用此列标识符填充 ErrorColumn 值。  
  
11. 关闭“脚本转换编辑器”  。  
  
12. 将脚本组件的输出附加到合适的目标。 对于即席测试，平面文件目标是最容易配置的。  
  
13. 运行包。  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  If Row.CountryRegionName <> "Canada" _  
      And Row.CountryRegionName <> "United States" Then  
  
    Row.ErrorColumn = 68 ' ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America."  
    Row.DirectRowToMyErrorOutput()  
  
  Else  
  
    Row.DirectRowToOutput0()  
  
  End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
{  
  
  if (Row.CountryRegionName!="Canada"&&Row.CountryRegionName!="United States")  
  
  {  
    Row.ErrorColumn = 68; // ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America.";  
    Row.DirectRowToMyErrorOutput();  
  
  }  
  else  
  {  
  
    Row.DirectRowToOutput0();  
  
  }  
  
}  
```  
  
![Integration Services 图标 (小型) ](../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [数据中的错误处理](../data-flow/error-handling-in-data.md)   
 [在数据流组件中使用错误输出](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [使用脚本组件创建同步转换](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
