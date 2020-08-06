---
title: 开发具有多个输入的数据流组件 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb56878c1b1b68dfdc4de19cb2b811de494c761b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691814"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>开发具有多个输入的数据流组件
  如果其多个输入以不相等速率生成数据，则具有多个输入的数据流组件可能会占用过多的内存。 开发支持两个或多个输入的自定义数据流组件时，可以通过使用 Microsoft.SqlServer.Dts.Pipeline 命名空间中的下列成员来管理此内存压力：  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 属性。 如果您想要实现使您的自定义数据流组件可管理以不相等速率流动的数据所需的代码，则将此属性的值设置为 `true`。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 如果您将 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 属性设置为 `true`，则必须提供此方法的实现方式。 如果未提供某一实现方式，则数据流引擎将在运行时引发异常。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 如果您将 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 属性设置为 `true`，并且您的自定义组件支持多个输入，则必须也提供此方法的实现方式。 如果未提供某一实现方式，且用户附加多个输入，则数据流引擎将在运行时将引发异常。  
  
 这些成员一起使您能够开发一个解决方案来解决内存压力，该解决方案类似于 Microsoft 为合并转换和合并联接转换开发的解决方案。  
  
## <a name="setting-the-supportsbackpressure-property"></a>设置 SupportsBackPressure 属性  
 为支持多个输入的自定义数据流组件实现更好的内存管理的第一步是将 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 属性的值设置为 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 中的 `true`。 在 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 的值为 `true` 时，数据流引擎将调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法；并且在有多个输入时，还在运行时调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。  
  
### <a name="example"></a>示例  
 在下面的示例中，<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 的实现方式将 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 的值设置为 `true`。  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>实现 IsInputReady 方法  
 在您在 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 对象中将 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 属性的值设置为 `true` 时，还必须提供 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法的实现方式。  
  
> [!NOTE]  
>  您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法的实现方式不应在基类中调用这些实现方式。 基类中此方法的默认实现方式只是引发 `NotImplementedException`。  
  
 实现此方法时，为该组件的每个输入都在布尔 canProcess  数组中设置元素的状态。  (在*inputIDs*数组中由其 ID 值标识输入。 ) 将*canProcess*数组中元素的值设置为 `true` 用于输入时，数据流引擎将调用该组件的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法，并为指定的输入提供更多数据。  
  
 当更多的上游数据可用时，至少一个输入的*canProcess*数组元素的值必须始终为 `true` ，否则处理将停止。  
  
 数据流引擎将在发送每个数据缓冲区前调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法，以便确定哪些输入正在等待接收更多数据。 在返回值指示某个输入被阻塞时，数据流引擎暂时为该输入缓存附加的数据缓冲区，而不是将它们发送到该组件。  
  
> [!NOTE]  
>  您不必在自己的代码中调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 数据流引擎调用这些方法以及您覆盖的 `PipelineComponent` 类的其他方法（在数据流引擎运行您的组件时）。  
  
### <a name="example"></a>示例  
 在下面的示例中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法的实现方式指示在以下条件成立时某个输入正在等待接收更多数据：  
  
-   更多的上游数据可用于该输入 (`!inputEOR`)。  
  
-   在已接收该组件的缓冲区中，对于该输入该组件当前不具有可供处理的数据 (`inputBuffers[inputIndex].CurrentRow() == null`)。  
  
 如果某个输入正在等待接收更多数据，则数据流组件通过将设置为 `true` 与该输入相对应的*canProcess*数组中的元素的值来指示这一点。  
  
 相反，在该组件对于该输入仍具有可供处理的数据时，该示例将挂起对该输入的处理。 该示例通过将设置为 `false` 与该输入相对应的*canProcess*数组中的元素的值来实现此目标。  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 前面的示例使用布尔型 `inputEOR` 数组指示是否有更多的上游数据可用于每个输入。 该数组名称中的 `EOR` 表示“行集结束”，并且引用数据流缓冲区的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 属性。 在此处未包括的示例部分中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法为它接收的每个数据缓冲区检查 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 属性的值。 在 `true` 的值指示没有更多的上游数据可用于某个输入时，该示例将针对该输入将 `inputEOR` 数组元素的值设置为 `true`。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> *canProcess* `false` 当 `inputEOR` 数组元素的值指示没有更多的上游数据可用于输入时，此方法的示例会将 canProcess 数组中相应元素的值设置为。  
  
## <a name="implementing-the-getdependentinputs-method"></a>实现 GetDependentInputs 方法  
 在您的自定义数据流组件支持多个输入时，您还必须为 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法提供实现方式。  
  
> [!NOTE]  
>  您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法的实现方式不应在基类中调用这些实现方式。 基类中此方法的默认实现方式只是引发 `NotImplementedException`。  
  
 在用户将多个输入附加到组件时，数据流引擎仅调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 如果组件仅具有两个输入，并且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法指示一个输入被阻塞 (*canProcess*  =  `false`) ，则数据流引擎将知道另一个输入正在等待接收更多数据。 但是，在存在多个输入，并且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法指示一个输入被阻塞时，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 中的附加代码标识哪些输入正在等待接收更多数据。  
  
> [!NOTE]  
>  您不必在自己的代码中调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 数据流引擎调用这些方法以及您覆盖的 `PipelineComponent` 类的其他方法（在数据流引擎运行您的组件时）。  
  
### <a name="example"></a>示例  
 对于被阻塞的特定输入，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法的以下实现方式返回正在等待接收更多数据、并因此阻塞指定输入的输入集合。 该组件通过检查在已接收组件的缓冲区中是否存在当前没有可供处理的数据的输入（但并非已阻塞的输入）(`inputBuffers[i].CurrentRow() == null`)，标识正在阻塞的输入 。 然后，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法将正在阻塞的输入的集合以输入 ID 的集合的形式返回。  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
