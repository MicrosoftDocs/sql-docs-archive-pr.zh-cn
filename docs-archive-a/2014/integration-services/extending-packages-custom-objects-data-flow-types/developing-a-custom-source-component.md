---
title: 开发自定义源组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [Integration Services], components
- external data sources [Integration Services]
- data flow components [Integration Services], source components
- output columns [Integration Services]
- custom data flow components [Integration Services], source components
- custom sources [Integration Services]
- source components [Integration Services]
ms.assetid: 4dc0f631-8fd6-4007-b573-ca67f58ca068
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6679b28463a09efe069235a5aef9dca54a381d62
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691819"
---
# <a name="developing-a-custom-source-component"></a><span data-ttu-id="8292e-102">开发自定义源组件</span><span class="sxs-lookup"><span data-stu-id="8292e-102">Developing a Custom Source Component</span></span>
  <span data-ttu-id="8292e-103">开发人员可以通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 编写可连接到自定义数据源的源组件，并可以将这些自定义数据源中的数据提供给数据流任务中的其他组件。</span><span class="sxs-lookup"><span data-stu-id="8292e-103">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gives developers the ability to write source components that can connect to custom data sources and supply data from those sources to other components in a data flow task.</span></span> <span data-ttu-id="8292e-104">如果必须连接到无法使用现有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源之一进行访问的数据源，则创建自定义源是非常重要的。</span><span class="sxs-lookup"><span data-stu-id="8292e-104">The ability to create custom sources is valuable when you must connect to data sources that cannot be accessed by using one of the existing [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sources.</span></span>

 <span data-ttu-id="8292e-105">源组件有一个或多个输出，没有输入。</span><span class="sxs-lookup"><span data-stu-id="8292e-105">Source components have one or more outputs and zero inputs.</span></span> <span data-ttu-id="8292e-106">在设计时，源组件用于创建和配置连接、从外部数据源读取列元数据并基于外部数据源配置源的输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-106">At design time, source components are used to create and configure connections, read column metadata from the external data source, and configure the source's output columns based on the external data source.</span></span> <span data-ttu-id="8292e-107">在执行过程中，源组件连接到外部数据源，并将行添加到输出缓冲区。</span><span class="sxs-lookup"><span data-stu-id="8292e-107">During execution they connect to the external data source and add rows to an output buffer.</span></span> <span data-ttu-id="8292e-108">然后，数据流任务会将此数据行缓冲区提供给下游组件。</span><span class="sxs-lookup"><span data-stu-id="8292e-108">The data flow task then provides this buffer of data rows to downstream components.</span></span>

 <span data-ttu-id="8292e-109">有关数据流组件开发的一般概述，请参阅[开发自定义数据流组件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。</span><span class="sxs-lookup"><span data-stu-id="8292e-109">For a general overview of data flow component development, see [Developing a Custom Data Flow Component](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).</span></span>

## <a name="design-time"></a><span data-ttu-id="8292e-110">设计时</span><span class="sxs-lookup"><span data-stu-id="8292e-110">Design Time</span></span>
 <span data-ttu-id="8292e-111">实现源组件的设计时功能包括指定与外部数据源的连接、添加和配置反映数据源的输出列以及验证该组件是否可以执行。</span><span class="sxs-lookup"><span data-stu-id="8292e-111">Implementing the design-time functionality of a source component involves specifying a connection to an external data source, adding and configuring output columns that reflect the data source, and validating that the component is ready to execute.</span></span> <span data-ttu-id="8292e-112">根据定义，源组件没有输入，有一个或多个异步输出。</span><span class="sxs-lookup"><span data-stu-id="8292e-112">By definition, a source component has zero inputs and one or more asynchronous outputs.</span></span>

### <a name="creating-the-component"></a><span data-ttu-id="8292e-113">创建组件</span><span class="sxs-lookup"><span data-stu-id="8292e-113">Creating the Component</span></span>
 <span data-ttu-id="8292e-114">源组件使用包中定义的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 对象连接到外部数据源。</span><span class="sxs-lookup"><span data-stu-id="8292e-114">Source components connect to external data sources by using <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> objects defined in a package.</span></span> <span data-ttu-id="8292e-115">源组件将元素添加到 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 属性的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 集合，以指明自己需要连接管理器。</span><span class="sxs-lookup"><span data-stu-id="8292e-115">They indicate their requirement for a connection manager by adding an element to the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> collection of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> property.</span></span> <span data-ttu-id="8292e-116">此集合有两个用途：一是保存对组件所用包中的连接管理器的引用；二是通知设计器此集合需要连接管理器。</span><span class="sxs-lookup"><span data-stu-id="8292e-116">This collection serves two purposes-to hold references to connection managers in the package used by the component, and to advertise the need for a connection manager to the designer.</span></span> <span data-ttu-id="8292e-117"><xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> 添加到该集合后，“高级编辑器”会显示“连接属性”选项卡，用户可以在其中选择包中的连接或创建连接   。</span><span class="sxs-lookup"><span data-stu-id="8292e-117">When an <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> has been added to the collection, the **Advanced Editor** displays the **Connection Properties** tab, which lets users select or create a connection in the package.</span></span>

 <span data-ttu-id="8292e-118">下面的代码示例演示 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 的实现，该实现添加一个输出，然后将 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> 对象添加到 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>。</span><span class="sxs-lookup"><span data-stu-id="8292e-118">The following code example shows an implementation of <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> that adds an output, and adds a <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> object to the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>.</span></span>

```csharp
using System;
using System.Collections;
using System.Data;
using System.Data.SqlClient;
using System.Data.OleDb;
using Microsoft.SqlServer.Dts.Runtime;
using Microsoft.SqlServer.Dts.Runtime.Wrapper;
using Microsoft.SqlServer.Dts.Pipeline;
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;

namespace Microsoft.Samples.SqlServer.Dts
{
    [DtsPipelineComponent(DisplayName = "MySourceComponent",ComponentType = ComponentType.SourceAdapter)]
    public class MyComponent : PipelineComponent
    {
        public override void ProvideComponentProperties()
        {
            // Reset the component.
            base.RemoveAllInputsOutputsAndCustomProperties();
            ComponentMetaData.RuntimeConnectionCollection.RemoveAll();

            IDTSOutput100 output = ComponentMetaData.OutputCollection.New();
            output.Name = "Output";

            IDTSRuntimeConnection100 connection = ComponentMetaData.RuntimeConnectionCollection.New();
            connection.Name = "ADO.NET";
        }
```

```vb
Imports System.Data
Imports System.Data.SqlClient
Imports Microsoft.SqlServer.Dts.Runtime
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper
Imports Microsoft.SqlServer.Dts.Pipeline
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper

<DtsPipelineComponent(DisplayName:="MySourceComponent", ComponentType:=ComponentType.SourceAdapter)> _
Public Class MySourceComponent
    Inherits PipelineComponent

    Public Overrides Sub ProvideComponentProperties()

        ' Allow for resetting the component.
        RemoveAllInputsOutputsAndCustomProperties()
        ComponentMetaData.RuntimeConnectionCollection.RemoveAll()

        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New()
        output.Name = "Output"

        Dim connection As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection.New()
        connection.Name = "ADO.NET"

    End Sub
End Class
```

### <a name="connecting-to-an-external-data-source"></a><span data-ttu-id="8292e-119">连接外部数据源</span><span class="sxs-lookup"><span data-stu-id="8292e-119">Connecting to an External Data Source</span></span>
 <span data-ttu-id="8292e-120">将连接添加到 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 后，请重写 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法以建立与外部数据源的连接。</span><span class="sxs-lookup"><span data-stu-id="8292e-120">After a connection has been added to the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>, you override the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> method to establish a connection to the external data source.</span></span> <span data-ttu-id="8292e-121">此方法在设计和执行期间调用。</span><span class="sxs-lookup"><span data-stu-id="8292e-121">This method is called during both design and execution time.</span></span> <span data-ttu-id="8292e-122">组件应先建立与连接管理器（由运行时连接指定）的连接，再建立与外部数据源的连接。</span><span class="sxs-lookup"><span data-stu-id="8292e-122">The component should establish a connection to the connection manager specified by the run-time connection, and subsequently, to the external data source.</span></span>

 <span data-ttu-id="8292e-123">连接建立后，组件应在内部缓存该连接，并在调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 方法时释放该连接。</span><span class="sxs-lookup"><span data-stu-id="8292e-123">After the connection is established, it should be cached internally by the component and released when the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> method is called.</span></span> <span data-ttu-id="8292e-124"><xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 方法与 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法一样，在设计时和执行时调用。</span><span class="sxs-lookup"><span data-stu-id="8292e-124">The <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> method is called at design and execution time, like the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> method.</span></span> <span data-ttu-id="8292e-125">开发人员可重写此方法，释放在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 过程中由组件建立的连接。</span><span class="sxs-lookup"><span data-stu-id="8292e-125">Developers override this method, and release the connection established by the component during <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>.</span></span>

 <span data-ttu-id="8292e-126">下面的代码示例演示在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法中连接到 ADO.NET 连接，然后在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 方法中关闭该连接的组件。</span><span class="sxs-lookup"><span data-stu-id="8292e-126">The following code example shows a component that connects to an ADO.NET connection in the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> method and closes the connection in the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> method.</span></span>

```csharp
private SqlConnection sqlConnection;

public override void AcquireConnections(object transaction)
{
    if (ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager != null)
    {
        ConnectionManager cm = Microsoft.SqlServer.Dts.Runtime.DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager);
        ConnectionManagerAdoNet cmado = cm.InnerObject as ConnectionManagerAdoNet;

        if (cmado == null)
            throw new Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.");

        sqlConnection = cmado.AcquireConnection(transaction) as SqlConnection;
        sqlConnection.Open();
    }
}

public override void ReleaseConnections()
{
    if (sqlConnection != null && sqlConnection.State != ConnectionState.Closed)
        sqlConnection.Close();
}
```

```vb
Private sqlConnection As SqlConnection

Public Overrides Sub AcquireConnections(ByVal transaction As Object)

    If Not IsNothing(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager) Then

        Dim cm As ConnectionManager = Microsoft.SqlServer.Dts.Runtime.DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager)
        Dim cmado As ConnectionManagerAdoNet = CType(cm.InnerObject, ConnectionManagerAdoNet)

        If IsNothing(cmado) Then
            Throw New Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.")
        End If

        sqlConnection = CType(cmado.AcquireConnection(transaction), SqlConnection)
        sqlConnection.Open()

    End If
End Sub

Public Overrides Sub ReleaseConnections()

    If Not IsNothing(sqlConnection) And sqlConnection.State <> ConnectionState.Closed Then
        sqlConnection.Close()
    End If

End Sub
```

### <a name="creating-and-configuring-output-columns"></a><span data-ttu-id="8292e-127">创建和配置输出列</span><span class="sxs-lookup"><span data-stu-id="8292e-127">Creating and Configuring Output Columns</span></span>
 <span data-ttu-id="8292e-128">源组件的输出列反映在执行该组件的过程中从外部数据源添加到数据流的列。</span><span class="sxs-lookup"><span data-stu-id="8292e-128">The output columns of a source component reflect the columns from the external data source that the component adds to the data flow during execution.</span></span> <span data-ttu-id="8292e-129">在设计时，在组件配置为连接到外部数据源后添加输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-129">At design time, you add output columns after the component has been configured to connect to an external data source.</span></span> <span data-ttu-id="8292e-130">组件用来将列添加到其输出集合的设计时方法会因所需组件而异，但不应在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 执行期间添加列。</span><span class="sxs-lookup"><span data-stu-id="8292e-130">The design-time method that a component uses to add the columns to its output collection can vary based on the needs of the component, although they should not be added during <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> or <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>.</span></span> <span data-ttu-id="8292e-131">例如，自定义属性中包含用于控制组件数据集的 SQL 语句的组件可在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetComponentProperty%2A> 方法中添加其输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-131">For example, a component that contains a SQL statement in a custom property that controls the data set for the component may add its output columns during the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetComponentProperty%2A> method.</span></span> <span data-ttu-id="8292e-132">组件会检查自己是否具有缓存的连接，如果有，则连接到数据源并生成输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-132">The component checks to see whether it has a cached connection, and, if it does, connects to the data source and generates its output columns.</span></span>

 <span data-ttu-id="8292e-133">创建输出列后，调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A> 方法可设置该列的数据类型属性。</span><span class="sxs-lookup"><span data-stu-id="8292e-133">After an output column has been created, set its data type properties by calling the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A> method.</span></span> <span data-ttu-id="8292e-134">此方法是必需的，因为 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> 属性是只读的，并且每个属性都依赖于其他属性的设置。</span><span class="sxs-lookup"><span data-stu-id="8292e-134">This method is necessary because the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A>, and <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> properties are read-only and each property is dependent on the settings of the other.</span></span> <span data-ttu-id="8292e-135">此方法强制使这些值的设置保持一致，并且数据流任务会验证是否正确设置了这些值。</span><span class="sxs-lookup"><span data-stu-id="8292e-135">This method enforces the need for these values to be set consistently, and the data flow task validates that they are set correctly.</span></span>

 <span data-ttu-id="8292e-136">列的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> 决定了为其他属性设置的值。</span><span class="sxs-lookup"><span data-stu-id="8292e-136">The <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> of the column determines the values that are set for the other properties.</span></span> <span data-ttu-id="8292e-137">下表说明了对每个 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> 的依赖属性的要求。</span><span class="sxs-lookup"><span data-stu-id="8292e-137">The following table shows the requirements on the dependent properties for each <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>.</span></span> <span data-ttu-id="8292e-138">未列出的数据类型的依赖属性设置为零。</span><span class="sxs-lookup"><span data-stu-id="8292e-138">The data types not listed have their dependent properties set to zero.</span></span>

|<span data-ttu-id="8292e-139">数据类型</span><span class="sxs-lookup"><span data-stu-id="8292e-139">DataType</span></span>|<span data-ttu-id="8292e-140">长度</span><span class="sxs-lookup"><span data-stu-id="8292e-140">Length</span></span>|<span data-ttu-id="8292e-141">缩放</span><span class="sxs-lookup"><span data-stu-id="8292e-141">Scale</span></span>|<span data-ttu-id="8292e-142">Precision</span><span class="sxs-lookup"><span data-stu-id="8292e-142">Precision</span></span>|<span data-ttu-id="8292e-143">CodePage</span><span class="sxs-lookup"><span data-stu-id="8292e-143">CodePage</span></span>|
|--------------|------------|-----------|---------------|--------------|
|<span data-ttu-id="8292e-144">DT_DECIMAL</span><span class="sxs-lookup"><span data-stu-id="8292e-144">DT_DECIMAL</span></span>|<span data-ttu-id="8292e-145">0</span><span class="sxs-lookup"><span data-stu-id="8292e-145">0</span></span>|<span data-ttu-id="8292e-146">大于 0 且小于或等于 28。</span><span class="sxs-lookup"><span data-stu-id="8292e-146">Greater than 0 and less than or equal to 28.</span></span>|<span data-ttu-id="8292e-147">0</span><span class="sxs-lookup"><span data-stu-id="8292e-147">0</span></span>|<span data-ttu-id="8292e-148">0</span><span class="sxs-lookup"><span data-stu-id="8292e-148">0</span></span>|
|<span data-ttu-id="8292e-149">DT_CY</span><span class="sxs-lookup"><span data-stu-id="8292e-149">DT_CY</span></span>|<span data-ttu-id="8292e-150">0</span><span class="sxs-lookup"><span data-stu-id="8292e-150">0</span></span>|<span data-ttu-id="8292e-151">0</span><span class="sxs-lookup"><span data-stu-id="8292e-151">0</span></span>|<span data-ttu-id="8292e-152">0</span><span class="sxs-lookup"><span data-stu-id="8292e-152">0</span></span>|<span data-ttu-id="8292e-153">0</span><span class="sxs-lookup"><span data-stu-id="8292e-153">0</span></span>|
|<span data-ttu-id="8292e-154">DT_NUMERIC</span><span class="sxs-lookup"><span data-stu-id="8292e-154">DT_NUMERIC</span></span>|<span data-ttu-id="8292e-155">0</span><span class="sxs-lookup"><span data-stu-id="8292e-155">0</span></span>|<span data-ttu-id="8292e-156">大于 0 且小于或等于 28，并且小于 Precision。</span><span class="sxs-lookup"><span data-stu-id="8292e-156">Greater than 0 and less than or equal to 28, and less than Precision.</span></span>|<span data-ttu-id="8292e-157">大于或等于 1 且小于或等于 38。</span><span class="sxs-lookup"><span data-stu-id="8292e-157">Greater than or equal to 1 and less than or equal to 38.</span></span>|<span data-ttu-id="8292e-158">0</span><span class="sxs-lookup"><span data-stu-id="8292e-158">0</span></span>|
|<span data-ttu-id="8292e-159">DT_BYTES</span><span class="sxs-lookup"><span data-stu-id="8292e-159">DT_BYTES</span></span>|<span data-ttu-id="8292e-160">大于 0。</span><span class="sxs-lookup"><span data-stu-id="8292e-160">Greater than 0.</span></span>|<span data-ttu-id="8292e-161">0</span><span class="sxs-lookup"><span data-stu-id="8292e-161">0</span></span>|<span data-ttu-id="8292e-162">0</span><span class="sxs-lookup"><span data-stu-id="8292e-162">0</span></span>|<span data-ttu-id="8292e-163">0</span><span class="sxs-lookup"><span data-stu-id="8292e-163">0</span></span>|
|<span data-ttu-id="8292e-164">DT_STR</span><span class="sxs-lookup"><span data-stu-id="8292e-164">DT_STR</span></span>|<span data-ttu-id="8292e-165">大于 0 且小于 8000。</span><span class="sxs-lookup"><span data-stu-id="8292e-165">Greater than 0 and less than 8000.</span></span>|<span data-ttu-id="8292e-166">0</span><span class="sxs-lookup"><span data-stu-id="8292e-166">0</span></span>|<span data-ttu-id="8292e-167">0</span><span class="sxs-lookup"><span data-stu-id="8292e-167">0</span></span>|<span data-ttu-id="8292e-168">不为 0，并且是一个有效的代码页。</span><span class="sxs-lookup"><span data-stu-id="8292e-168">Not 0, and a valid code page.</span></span>|
|<span data-ttu-id="8292e-169">DT_WSTR</span><span class="sxs-lookup"><span data-stu-id="8292e-169">DT_WSTR</span></span>|<span data-ttu-id="8292e-170">大于 0 且小于 4000。</span><span class="sxs-lookup"><span data-stu-id="8292e-170">Greater than 0 and less than 4000.</span></span>|<span data-ttu-id="8292e-171">0</span><span class="sxs-lookup"><span data-stu-id="8292e-171">0</span></span>|<span data-ttu-id="8292e-172">0</span><span class="sxs-lookup"><span data-stu-id="8292e-172">0</span></span>|<span data-ttu-id="8292e-173">0</span><span class="sxs-lookup"><span data-stu-id="8292e-173">0</span></span>|

 <span data-ttu-id="8292e-174">由于对数据类型属性的限制是基于输出列的数据类型的，因此使用托管类型时必须选择正确的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 数据类型。</span><span class="sxs-lookup"><span data-stu-id="8292e-174">Because the restrictions on the data type properties are based on the data type of the output column, you must choose the correct [!INCLUDE[ssIS](../../includes/ssis-md.md)] data type when you work with managed types.</span></span> <span data-ttu-id="8292e-175">基类提供了三个帮助程序方法：<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A>，它们可协助托管组件开发人员在给定托管类型的情况下选择 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 数据类型。</span><span class="sxs-lookup"><span data-stu-id="8292e-175">The base class provides three helper methods, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A>, and <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A>, to assist managed component developers in selecting an [!INCLUDE[ssIS](../../includes/ssis-md.md)] data type given a managed type.</span></span> <span data-ttu-id="8292e-176">这些方法用于将托管数据类型转换为 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 数据类型，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="8292e-176">These methods convert managed data types to [!INCLUDE[ssIS](../../includes/ssis-md.md)] data types, and vice versa.</span></span>

 <span data-ttu-id="8292e-177">下面的代码示例演示如何基于表架构来填充组件的输出列集合。</span><span class="sxs-lookup"><span data-stu-id="8292e-177">The following code example shows how the output column collection of a component is populated based on the schema of a table.</span></span> <span data-ttu-id="8292e-178">基类的帮助器方法用于设置列的数据类型，并基于该数据类型设置依赖属性。</span><span class="sxs-lookup"><span data-stu-id="8292e-178">The helper methods of the base class are used to set the data type of the column, and the dependent properties are set based on the data type.</span></span>

```csharp
SqlCommand sqlCommand;

private void CreateColumnsFromDataTable()
{
    // Get the output.
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];

    // Start clean, and remove the columns from both collections.
    output.OutputColumnCollection.RemoveAll();
    output.ExternalMetadataColumnCollection.RemoveAll();

    this.sqlCommand = sqlConnection.CreateCommand();
    this.sqlCommand.CommandType = CommandType.Text;
    this.sqlCommand.CommandText = (string)ComponentMetaData.CustomPropertyCollection["SqlStatement"].Value;
    SqlDataReader schemaReader = this.sqlCommand.ExecuteReader(CommandBehavior.SchemaOnly);
    DataTable dataTable = schemaReader.GetSchemaTable();

    // Walk the columns in the schema, 
    // and for each data column create an output column and an external metadata column.
    foreach (DataRow row in dataTable.Rows)
    {
        IDTSOutputColumn100 outColumn = output.OutputColumnCollection.New();
        IDTSExternalMetadataColumn100 exColumn = output.ExternalMetadataColumnCollection.New();

        // Set column data type properties.
        bool isLong = false;
        DataType dt = DataRecordTypeToBufferType((Type)row["DataType"]);
        dt = ConvertBufferDataTypeToFitManaged(dt, ref isLong);
        int length = 0;
        int precision = (short)row["NumericPrecision"];
        int scale = (short)row["NumericScale"];
        int codepage = dataTable.Locale.TextInfo.ANSICodePage;

        switch (dt)
        {
            // The length cannot be zero, and the code page property must contain a valid code page.
            case DataType.DT_STR:
            case DataType.DT_TEXT:
                length = precision;
                precision = 0;
                scale = 0;
                break;

            case DataType.DT_WSTR:
                length = precision;
                codepage = 0;
                scale = 0;
                precision = 0;
                break;

            case DataType.DT_BYTES:
                precision = 0;
                scale = 0;
                codepage = 0;
                break;

            case DataType.DT_NUMERIC:
                length = 0;
                codepage = 0;

                if (precision > 38)
                    precision = 38;

                if (scale > 6)
                    scale = 6;
                break;

            case DataType.DT_DECIMAL:
                length = 0;
                precision = 0;
                codepage = 0;
                break;

            default:
                length = 0;
                precision = 0;
                codepage = 0;
                scale = 0;
                break;

        }

        // Set the properties of the output column.
        outColumn.Name = (string)row["ColumnName"];
        outColumn.SetDataTypeProperties(dt, length, precision, scale, codepage);
    }
}
```

```vb
Private sqlCommand As SqlCommand

Private Sub CreateColumnsFromDataTable()

    ' Get the output.
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)

    ' Start clean, and remove the columns from both collections.
    output.OutputColumnCollection.RemoveAll()
    output.ExternalMetadataColumnCollection.RemoveAll()

    Me.sqlCommand = sqlConnection.CreateCommand()
    Me.sqlCommand.CommandType = CommandType.Text
    Me.sqlCommand.CommandText = CStr(ComponentMetaData.CustomPropertyCollection("SqlStatement").Value)

    Dim schemaReader As SqlDataReader = Me.sqlCommand.ExecuteReader(CommandBehavior.SchemaOnly)
    Dim dataTable As DataTable = schemaReader.GetSchemaTable()

    ' Walk the columns in the schema, 
    ' and for each data column create an output column and an external metadata column.
    For Each row As DataRow In dataTable.Rows

        Dim outColumn As IDTSOutputColumn100 = output.OutputColumnCollection.New()
        Dim exColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New()

        ' Set column data type properties.
        Dim isLong As Boolean = False
        Dim dt As DataType = DataRecordTypeToBufferType(CType(row("DataType"), Type))
        dt = ConvertBufferDataTypeToFitManaged(dt, isLong)
        Dim length As Integer = 0
        Dim precision As Integer = CType(row("NumericPrecision"), Short)
        Dim scale As Integer = CType(row("NumericScale"), Short)
        Dim codepage As Integer = dataTable.Locale.TextInfo.ANSICodePage

        Select Case dt

            ' The length cannot be zero, and the code page property must contain a valid code page.
            Case DataType.DT_STR
            Case DataType.DT_TEXT
                length = precision
                precision = 0
                scale = 0

            Case DataType.DT_WSTR
                length = precision
                codepage = 0
                scale = 0
                precision = 0

            Case DataType.DT_BYTES
                precision = 0
                scale = 0
                codepage = 0

            Case DataType.DT_NUMERIC
                length = 0
                codepage = 0

                If precision > 38 Then
                    precision = 38
                End If

                If scale > 6 Then
                    scale = 6
                End If

            Case DataType.DT_DECIMAL
                length = 0
                precision = 0
                codepage = 0

            Case Else
                length = 0
                precision = 0
                codepage = 0
                scale = 0
        End Select

        ' Set the properties of the output column.
        outColumn.Name = CStr(row("ColumnName"))
        outColumn.SetDataTypeProperties(dt, length, precision, scale, codepage)
    Next
End Sub
```

### <a name="validating-the-component"></a><span data-ttu-id="8292e-179">验证组件</span><span class="sxs-lookup"><span data-stu-id="8292e-179">Validating the Component</span></span>
 <span data-ttu-id="8292e-180">您应验证源组件，并验证源组件的输出列集合中定义的列是否与外部数据源中的列相匹配。</span><span class="sxs-lookup"><span data-stu-id="8292e-180">You should validate a source component and verify that the columns defined in its output column collections match the columns at the external data source.</span></span> <span data-ttu-id="8292e-181">有时，根据外部数据源验证输出列是不可能，例如处于断开连接状态时，或者希望避免与服务器之间费时的往返通信时。</span><span class="sxs-lookup"><span data-stu-id="8292e-181">Sometimes, verifying the output columns against the external data source can be impossible, such as in a disconnected state, or when it is preferable to avoid lengthy round trips to the server.</span></span> <span data-ttu-id="8292e-182">在这些情况下，仍然可以使用输出对象的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.ExternalMetadataColumnCollection%2A> 来验证输出中的列。</span><span class="sxs-lookup"><span data-stu-id="8292e-182">In these situations, the columns in the output can still be validated by using the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.ExternalMetadataColumnCollection%2A> of the output object.</span></span> <span data-ttu-id="8292e-183">有关详细信息，请参阅[验证数据流组件](../extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)。</span><span class="sxs-lookup"><span data-stu-id="8292e-183">For more information, see [Validating a Data Flow Component](../extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md).</span></span>

 <span data-ttu-id="8292e-184">此集合同时存在于输入对象和输出对象中，可以使用来自外部数据源的列填充此集合。</span><span class="sxs-lookup"><span data-stu-id="8292e-184">This collection exists on both input and output objects and you can populate it with the columns from the external data source.</span></span> <span data-ttu-id="8292e-185">此集合可用于在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器处于离线状态、组件断开连接或 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 属性为 `false` 时验证输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-185">You can use this collection to validate the output columns when [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer is offline, when the component is disconnected, or when the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> property is `false`.</span></span> <span data-ttu-id="8292e-186">应在创建输出列的同时对该集合进行首次填充。</span><span class="sxs-lookup"><span data-stu-id="8292e-186">The collection should be first populated at the same time that the output columns are created.</span></span> <span data-ttu-id="8292e-187">将外部元数据列添加到集合相对比较容易，因为外部元数据列最初就应与输出列相匹配。</span><span class="sxs-lookup"><span data-stu-id="8292e-187">Adding external metadata columns to the collection is relatively easy because the external metadata column should initially match the output column.</span></span> <span data-ttu-id="8292e-188">列的数据类型属性应已正确设置，这些属性可直接复制到 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> 对象。</span><span class="sxs-lookup"><span data-stu-id="8292e-188">The data type properties of the column should have already been set correctly, and the properties can be copied directly to the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> object.</span></span>

 <span data-ttu-id="8292e-189">下面的示例代码添加一个外部元数据列，该列基于新创建的输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-189">The following sample code adds an external metadata column that is based on a newly created output column.</span></span> <span data-ttu-id="8292e-190">假定已经创建了该输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-190">It assumes that the output column has already been created.</span></span>

```csharp
private void CreateExternalMetaDataColumn(IDTSOutput100 output, IDTSOutputColumn100 outputColumn)
{

    // Set the properties of the external metadata column.
    IDTSExternalMetadataColumn100 externalColumn = output.ExternalMetadataColumnCollection.New();
    externalColumn.Name = outputColumn.Name;
    externalColumn.Precision = outputColumn.Precision;
    externalColumn.Length = outputColumn.Length;
    externalColumn.DataType = outputColumn.DataType;
    externalColumn.Scale = outputColumn.Scale;

    // Map the external column to the output column.
    outputColumn.ExternalMetadataColumnID = externalColumn.ID;

}
```

```vb
Private Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumn As IDTSOutputColumn100)

        ' Set the properties of the external metadata column.
        Dim externalColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New()
        externalColumn.Name = outputColumn.Name
        externalColumn.Precision = outputColumn.Precision
        externalColumn.Length = outputColumn.Length
        externalColumn.DataType = outputColumn.DataType
        externalColumn.Scale = outputColumn.Scale

        ' Map the external column to the output column.
        outputColumn.ExternalMetadataColumnID = externalColumn.ID

    End Sub
```

## <a name="run-time"></a><span data-ttu-id="8292e-191">运行时</span><span class="sxs-lookup"><span data-stu-id="8292e-191">Run Time</span></span>
 <span data-ttu-id="8292e-192">执行期间，组件会将行添加到输出缓冲区中，输出缓冲区由数据流任务创建并在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 中提供给组件。</span><span class="sxs-lookup"><span data-stu-id="8292e-192">During execution, components add rows to output buffers that are created by the data flow task and provided to the component in <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>.</span></span> <span data-ttu-id="8292e-193">只为源组件调用一次该方法，该方法会为连接到下游组件的组件的每个 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 接收一个输出缓冲区。</span><span class="sxs-lookup"><span data-stu-id="8292e-193">Called once for source components, the method receives an output buffer for each <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> of the component that is connected to a downstream component.</span></span>

### <a name="locating-columns-in-the-buffer"></a><span data-ttu-id="8292e-194">在缓冲区中查找列</span><span class="sxs-lookup"><span data-stu-id="8292e-194">Locating Columns in the Buffer</span></span>
 <span data-ttu-id="8292e-195">组件的输出缓冲区中包含组件定义的列以及向下游组件的输出添加的所有列。</span><span class="sxs-lookup"><span data-stu-id="8292e-195">The output buffer for a component contains the columns defined by the component and any columns added to the output of a downstream component.</span></span> <span data-ttu-id="8292e-196">例如，如果源组件在其输出中提供三列，下一个组件添加了第四个输出列，则供源组件使用的输出缓冲区将包含这四列。</span><span class="sxs-lookup"><span data-stu-id="8292e-196">For example, if a source component provides three columns in its output, and the next component adds a fourth output column, the output buffer provided for use by the source component contains these four columns.</span></span>

 <span data-ttu-id="8292e-197">缓冲区行中的列顺序不是由输出列集合中输出列的索引确定的。</span><span class="sxs-lookup"><span data-stu-id="8292e-197">The order of the columns in a buffer row is not defined by the index of the output column in the output column collection.</span></span> <span data-ttu-id="8292e-198">只有使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSBufferManagerClass.FindColumnByLineageID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 方法才能在缓冲区行中准确地定位输出列。</span><span class="sxs-lookup"><span data-stu-id="8292e-198">An output column can only be accurately located in a buffer row by using the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSBufferManagerClass.FindColumnByLineageID%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A>.</span></span> <span data-ttu-id="8292e-199">此方法在指定缓冲区中查找具有指定沿袭 ID 的列，并返回其在行中的位置。</span><span class="sxs-lookup"><span data-stu-id="8292e-199">This method locates the column with the specified lineage ID in the specified buffer, and returns its location in the row.</span></span> <span data-ttu-id="8292e-200">输出列的索引通常在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 方法中查找，并存储以供在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 中使用。</span><span class="sxs-lookup"><span data-stu-id="8292e-200">The indexes of the output columns are typically located in the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> method, and stored for use during <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>.</span></span>

 <span data-ttu-id="8292e-201">下面的代码示例在调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 期间在输出缓冲区中查找输出列的位置，并将其存储在内部结构中。</span><span class="sxs-lookup"><span data-stu-id="8292e-201">The following code example finds the location of the output columns in the output buffer during a call to <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>, and stores them in an internal structure.</span></span> <span data-ttu-id="8292e-202">列的名称也存储在该结构中，在本主题下一部分的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法的代码示例中将使用该名称。</span><span class="sxs-lookup"><span data-stu-id="8292e-202">The name of the column is also stored in the structure and is used in the code example for the  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> method in the next section of this topic.</span></span>

```csharp
ArrayList columnInformation;

private struct ColumnInfo
{
    public int BufferColumnIndex;
    public string ColumnName;
}

public override void PreExecute()
{
    this.columnInformation = new ArrayList();
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];

    foreach (IDTSOutputColumn100 col in output.OutputColumnCollection)
    {
        ColumnInfo ci = new ColumnInfo();
        ci.BufferColumnIndex = BufferManager.FindColumnByLineageID(output.Buffer, col.LineageID);
        ci.ColumnName = col.Name;
        columnInformation.Add(ci);
    }
}
```

```vb
Public Overrides Sub PreExecute()

    Me.columnInformation = New ArrayList()
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)

    For Each col As IDTSOutputColumn100 In output.OutputColumnCollection

        Dim ci As ColumnInfo = New ColumnInfo()
        ci.BufferColumnIndex = BufferManager.FindColumnByLineageID(output.Buffer, col.LineageID)
        ci.ColumnName = col.Name
        columnInformation.Add(ci)
    Next
End Sub
```

### <a name="processing-rows"></a><span data-ttu-id="8292e-203">处理行</span><span class="sxs-lookup"><span data-stu-id="8292e-203">Processing Rows</span></span>
 <span data-ttu-id="8292e-204">调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> 方法可将行添加到输出缓冲区，该方法会创建一个其各列为空值的新缓冲区行。</span><span class="sxs-lookup"><span data-stu-id="8292e-204">Rows are added to the output buffer by calling the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> method, which creates a new buffer row with empty values in its columns.</span></span> <span data-ttu-id="8292e-205">然后，组件将为各列赋值。</span><span class="sxs-lookup"><span data-stu-id="8292e-205">The component then assigns values to the individual columns.</span></span> <span data-ttu-id="8292e-206">提供给组件的输出缓冲区由数据流任务创建并监视。</span><span class="sxs-lookup"><span data-stu-id="8292e-206">The output buffers provided to a component are created and monitored by the data flow task.</span></span> <span data-ttu-id="8292e-207">输出缓冲区满后，缓冲区中的行会移到下一个组件中。</span><span class="sxs-lookup"><span data-stu-id="8292e-207">As they become full, the rows in the buffer are moved to the next component.</span></span> <span data-ttu-id="8292e-208">无法确定一批行何时发送到下一个组件，因为数据流任务执行的行移动对组件开发人员是透明的，并且输出缓冲区的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.RowCount%2A> 属性始终为零。</span><span class="sxs-lookup"><span data-stu-id="8292e-208">There is no way to determine when a batch of rows has been sent to the next component because the movement of rows by the data flow task is transparent to the component developer, and the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.RowCount%2A> property is always zero on output buffers.</span></span> <span data-ttu-id="8292e-209">源组件完成将行添加到其输出缓冲区后，它将调用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 方法通知数据流任务，缓冲区中的其余行会传递给下一个组件。</span><span class="sxs-lookup"><span data-stu-id="8292e-209">When a source component is finished adding rows to its output buffer, it notifies the data flow task by calling the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> method of the <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer>, and the remaining rows in the buffer are passed to the next component.</span></span>

 <span data-ttu-id="8292e-210">源组件从外部数据源读取行时，可以调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.IncrementPipelinePerfCounter%2A> 方法来更新“Rows read”或“BLOB bytes read”性能计数器。</span><span class="sxs-lookup"><span data-stu-id="8292e-210">While the source component reads rows from the external data source, you may want to update the "Rows read" or "BLOB bytes read" performance counters by calling the <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.IncrementPipelinePerfCounter%2A> method.</span></span> <span data-ttu-id="8292e-211">有关详细信息，请参阅 [性能计时器](../performance/performance-counters.md)。</span><span class="sxs-lookup"><span data-stu-id="8292e-211">For more information, see [Performance Counters](../performance/performance-counters.md).</span></span>

 <span data-ttu-id="8292e-212">下面的代码示例演示在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 中将行添加到输出缓冲区的组件。</span><span class="sxs-lookup"><span data-stu-id="8292e-212">The following code example shows a component that adds rows to an output buffer in <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>.</span></span> <span data-ttu-id="8292e-213">缓冲区中输出列的索引已在前面的代码示例中使用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 找到。</span><span class="sxs-lookup"><span data-stu-id="8292e-213">The indexes of the output columns in the buffer were located using <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> in the previous code example.</span></span>

```csharp
public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)
{
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];
    PipelineBuffer buffer = buffers[0];

    SqlDataReader dataReader = sqlCommand.ExecuteReader();

    // Loop over the rows in the DataReader, 
    // and add them to the output buffer.
    while (dataReader.Read())
    {
        // Add a row to the output buffer.
        buffer.AddRow();

        for (int x = 0; x < columnInformation.Count; x++)
        {
            ColumnInfo ci = (ColumnInfo)columnInformation[x];
            int ordinal = dataReader.GetOrdinal(ci.ColumnName);

            if (dataReader.IsDBNull(ordinal))
                buffer.SetNull(ci.BufferColumnIndex);
            else
            {
                buffer[ci.BufferColumnIndex] = dataReader[ci.ColumnName];
            }
        }
    }
    buffer.SetEndOfRowset();
}
```

```vb
Public Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())

    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)
    Dim buffer As PipelineBuffer = buffers(0)

    Dim dataReader As SqlDataReader = sqlCommand.ExecuteReader()

    ' Loop over the rows in the DataReader, 
    ' and add them to the output buffer.
    While (dataReader.Read())

        ' Add a row to the output buffer.
        buffer.AddRow()

        For x As Integer = 0 To columnInformation.Count

            Dim ci As ColumnInfo = CType(columnInformation(x), ColumnInfo)

            Dim ordinal As Integer = dataReader.GetOrdinal(ci.ColumnName)

            If (dataReader.IsDBNull(ordinal)) Then
                buffer.SetNull(ci.BufferColumnIndex)
            Else
                buffer(ci.BufferColumnIndex) = dataReader(ci.ColumnName)

            End If
        Next

    End While

    buffer.SetEndOfRowset()
End Sub
```

## <a name="sample"></a><span data-ttu-id="8292e-214">示例</span><span class="sxs-lookup"><span data-stu-id="8292e-214">Sample</span></span>
 <span data-ttu-id="8292e-215">下面的示例演示一个简单的源组件，该组件使用文件连接管理器将文件的二进制内容加载到数据流中。</span><span class="sxs-lookup"><span data-stu-id="8292e-215">The following sample shows a simple source component that uses a File connection manager to load the binary contents of files into the data flow.</span></span> <span data-ttu-id="8292e-216">此示例未演示本主题中讨论的全部方法和功能。</span><span class="sxs-lookup"><span data-stu-id="8292e-216">This sample does not demonstrate all the methods and functionality discussed in this topic.</span></span> <span data-ttu-id="8292e-217">它演示了每个自定义源组件都必须重写的重要方法，但不包含用于设计时验证的代码。</span><span class="sxs-lookup"><span data-stu-id="8292e-217">It demonstrates the important methods that every custom source component must override, but does not contain code for design-time validation.</span></span>

```csharp
using System;
using System.IO;
using Microsoft.SqlServer.Dts.Pipeline;
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;
using Microsoft.SqlServer.Dts.Runtime.Wrapper;

namespace BlobSrc
{
  [DtsPipelineComponent(DisplayName = "BLOB Inserter Source", Description = "Inserts files into the data flow as BLOBs")]
  public class BlobSrc : PipelineComponent
  {
    IDTSConnectionManager100 m_ConnMgr;
    int m_FileNameColumnIndex = -1;
    int m_FileBlobColumnIndex = -1;

    public override void ProvideComponentProperties()
    {
      IDTSOutput100 output = ComponentMetaData.OutputCollection.New();
      output.Name = "BLOB File Inserter Output";

      IDTSOutputColumn100 column = output.OutputColumnCollection.New();
      column.Name = "FileName";
      column.SetDataTypeProperties(DataType.DT_WSTR, 256, 0, 0, 0);

      column = output.OutputColumnCollection.New();
      column.Name = "FileBLOB";
      column.SetDataTypeProperties(DataType.DT_IMAGE, 0, 0, 0, 0);

      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection.New();
      conn.Name = "FileConnection";
    }

    public override void AcquireConnections(object transaction)
    {
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection[0];
      m_ConnMgr = conn.ConnectionManager;
    }

    public override void ReleaseConnections()
    {
      m_ConnMgr = null;
    }

    public override void PreExecute()
    {
      IDTSOutput100 output = ComponentMetaData.OutputCollection[0];

      m_FileNameColumnIndex = (int)BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[0].LineageID);
      m_FileBlobColumnIndex = (int)BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[1].LineageID);
    }

    public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)
    {
      string strFileName = (string)m_ConnMgr.AcquireConnection(null);

      while (strFileName != null)
      {
        buffers[0].AddRow();

        buffers[0].SetString(m_FileNameColumnIndex, strFileName);

        FileInfo fileInfo = new FileInfo(strFileName);
        byte[] fileData = new byte[fileInfo.Length];
        FileStream fs = new FileStream(strFileName, FileMode.Open, FileAccess.Read, FileShare.Read);
        fs.Read(fileData, 0, fileData.Length);

        buffers[0].AddBlobData(m_FileBlobColumnIndex, fileData);

        strFileName = (string)m_ConnMgr.AcquireConnection(null);
      }

      buffers[0].SetEndOfRowset();
    }
  }
}
```

```vb
Imports System 
Imports System.IO 
Imports Microsoft.SqlServer.Dts.Pipeline 
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper 
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper 
Namespace BlobSrc 

 <DtsPipelineComponent(DisplayName="BLOB Inserter Source", Description="Inserts files into the data flow as BLOBs")> _ 
 Public Class BlobSrc 
 Inherits PipelineComponent 
   Private m_ConnMgr As IDTSConnectionManager100 
   Private m_FileNameColumnIndex As Integer = -1 
   Private m_FileBlobColumnIndex As Integer = -1 

   Public  Overrides Sub ProvideComponentProperties() 
     Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New 
     output.Name = "BLOB File Inserter Output" 
     Dim column As IDTSOutputColumn100 = output.OutputColumnCollection.New 
     column.Name = "FileName" 
     column.SetDataTypeProperties(DataType.DT_WSTR, 256, 0, 0, 0) 
     column = output.OutputColumnCollection.New 
     column.Name = "FileBLOB" 
     column.SetDataTypeProperties(DataType.DT_IMAGE, 0, 0, 0, 0) 
     Dim conn As IDTSRuntimeConnection90 = ComponentMetaData.RuntimeConnectionCollection.New 
     conn.Name = "FileConnection" 
   End Sub 

   Public  Overrides Sub AcquireConnections(ByVal transaction As Object) 
     Dim conn As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection(0) 
     m_ConnMgr = conn.ConnectionManager 
   End Sub 

   Public  Overrides Sub ReleaseConnections() 
     m_ConnMgr = Nothing 
   End Sub 

   Public  Overrides Sub PreExecute() 
     Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0) 
     m_FileNameColumnIndex = CType(BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(0).LineageID), Integer) 
     m_FileBlobColumnIndex = CType(BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(1).LineageID), Integer) 
   End Sub 

   Public  Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer()) 
     Dim strFileName As String = CType(m_ConnMgr.AcquireConnection(Nothing), String) 
     While Not (strFileName Is Nothing) 
       buffers(0).AddRow 
       buffers(0).SetString(m_FileNameColumnIndex, strFileName) 
       Dim fileInfo As FileInfo = New FileInfo(strFileName) 
       Dim fileData(fileInfo.Length) As Byte 
       Dim fs As FileStream = New FileStream(strFileName, FileMode.Open, FileAccess.Read, FileShare.Read) 
       fs.Read(fileData, 0, fileData.Length) 
       buffers(0).AddBlobData(m_FileBlobColumnIndex, fileData) 
       strFileName = CType(m_ConnMgr.AcquireConnection(Nothing), String) 
     End While 
     buffers(0).SetEndOfRowset 
   End Sub 
 End Class 
End Namespace
```

<span data-ttu-id="8292e-218">![Integration Services 图标 (小型) ](../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**</span><span class="sxs-lookup"><span data-stu-id="8292e-218">![Integration Services icon (small)](../media/dts-16.gif "Integration Services icon (small)")  **Stay Up to Date with Integration Services**</span></span><br /> <span data-ttu-id="8292e-219">若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：</span><span class="sxs-lookup"><span data-stu-id="8292e-219">For the latest downloads, articles, samples, and videos from Microsoft, as well as selected solutions from the community, visit the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] page on MSDN:</span></span><br /><br /> [<span data-ttu-id="8292e-220">访问 MSDN 上的 Integration Services 页</span><span class="sxs-lookup"><span data-stu-id="8292e-220">Visit the Integration Services page on MSDN</span></span>](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> <span data-ttu-id="8292e-221">若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。</span><span class="sxs-lookup"><span data-stu-id="8292e-221">For automatic notification of these updates, subscribe to the RSS feeds available on the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="8292e-222">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8292e-222">See Also</span></span>
 <span data-ttu-id="8292e-223">[开发自定义目标组件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)[使用脚本组件创建源](../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)</span><span class="sxs-lookup"><span data-stu-id="8292e-223">[Developing a Custom Destination Component](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md) [Creating a Source with the Script Component](../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)</span></span>


