---
title: 用 SQL Server 代理计划 SSAS 管理任务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2c78fa5fcebc0589ba863163b93ad2d10731b75a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690198"
---
# <a name="schedule-ssas-administrative-tasks-with-sql-server-agent"></a>使用 SQL Server 代理来计划 SSAS 管理任务
  使用 SQL Server 代理服务，你可以根据所需顺序和时间来计划要运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理任务。 通过计划任务，可以自动运行定期或以可预测周期运行的进程。 您可以计划管理任务（例如多维数据集处理）以在周期长的业务活动期间运行。 还可以通过在 SQL Server 代理作业中创建作业步骤来确定任务的执行顺序。 例如，可以处理多维数据集，然后对该多维数据集进行备份。  
  
 使用作业步骤，可以控制执行流。 如果一个作业失败，则可以配置 SQL Server 代理以继续运行剩下的任务或停止执行。 也可以配置 SQL Server 代理以发送有关作业执行成功或失败的通知。  
  
 本主题是一个演练，演示了如何使用 SQL Server 代理通过两种方式运行 XMLA 脚本。 第一个示例演示如何计划对单个维度的处理。 第二个示例演示如何将处理任务并入按计划运行的单个脚本。 若要完成此演练，您需要满足下列先决条件。  
  
## <a name="prerequisites"></a>先决条件  
 必须安装 SQL Server 代理服务。  
  
 默认情况下，作业在服务帐户下运行。 在中 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ，SQL Server 代理的默认帐户是 NT Service\SQLAgent $ \<instancename> 。 若要执行备份或处理任务，此帐户必须是 Analysis Services 实例的系统管理员。 有关详细信息，请参阅[&#40;Analysis Services&#41;授予服务器管理员权限](grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
 您还应拥有要使用的测试数据库。 可以部署 AdventureWorks 多维示例数据库或 Analysis Services 多维教程中的项目以在本演练中使用。 有关详细信息，请参阅[安装 Analysis Services 多维建模教程的示例数据和项目](../install-sample-data-and-projects.md)。  
  
## <a name="example-1-processing-a-dimension-in-a-scheduled-task"></a>示例 1：处理计划任务中的维度  
 此示例演示如何创建和计划处理维度的作业。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 计划任务是嵌入在 SQL Server 代理作业中的 XMLA 脚本。 该作业经过计划，按照所需时间和频率运行。 由于 SQL Server 代理是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的一部分，因此要同时使用数据库引擎和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 来创建和计划管理任务。  
  
###  <a name="create-a-script-for-processing-a-dimension-in-a-sql-server-agent-job"></a><a name="bkmk_CreateScript"></a>创建用于处理 SQL Server 代理作业中的维度的脚本  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 打开数据库文件夹并查找维度。 右键单击维度，然后选择“处理”****。  
  
2.  在 **“处理维度”** 对话框的 **“对象列表”** 下的 **“处理选项”** 列中，验证此列的选项是否为 **“处理全部”**。 如果不是，则在“处理选项”**** 下单击选项，然后从下拉列表中选择“处理全部”****。  
  
3.  单击 **“脚本”**。  
  
     此步骤将打开包含处理维度的 XMLA 脚本的 **“XML 查询”** 窗口。  
  
4.  在 **“处理维度”** 对话框中，单击 **“取消”** 关闭该对话框。  
  
5.  在“XMLA 查询”**** 窗口中，突出显示 XMLA 脚本，右键单击突出显示的脚本，然后选择“复制”****。  
  
     此步骤会将 XMLA 脚本复制到 Windows 剪贴板中。 可以将 XMLA 脚本保留在剪贴板中，也可以将其粘贴到记事本或其他文本编辑器中。 以下是 XMLA 脚本的一个示例。  
  
    ```  
    <Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="create-and-schedule-the-dimension-processing-job"></a><a name="bkmk_ProcessJob"></a>创建和计划维度处理作业  
  
1.  连接到数据库引擎实例，然后打开对象资源管理器。  
  
2.  展开 **“SQL Server 代理”**。  
  
3.  右键单击“作业”****，然后选择“新建作业”****。  
  
4.  在 **“新建作业”** 对话框的 **“名称”** 中，输入作业名称。  
  
5.  在 **“选择页”** 下，选择 **“步骤”**，然后单击 **“新建”**。  
  
6.  在 **“新建作业步骤”** 对话框的 **“步骤名称”** 中，输入步骤名称。  
  
7.  在 "**服务器**" 中，键入默认实例的**localhost** ， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 并为命名实例键入**localhost \\ ** \<*instance name*> 。  
  
     如果您将从远程计算机运行作业，请使用将运行作业的服务器和实例的名称。 对于 \<*server name*> 命名实例，请使用格式> 默认实例和 \<*server name*> \\ < *实例名称*。  
  
8.  在 **“类型”** 中，选择 **“SQL Server Analysis Services 命令”**。  
  
9. 在“命令”**** 中，右键单击并选择“粘贴”****。 上一步中生成的 XMLA 脚本应显示在命令窗口中。  
  
10. 单击“确定”  。  
  
11. 在 **“选择页”** 下，单击 **“计划”**，然后单击 **“新建”**。  
  
12. 在 **“新建作业计划”** 对话框的 **“名称”** 中，输入计划名称，然后单击 **“确定”**。  
  
     此步骤将创建一个于星期日 12:00 AM 启动的计划。 下一步将说明如何手动执行作业。 您还可指定在监视作业时执行作业的计划。  
  
13. 在 **“新建作业”** 对话框中，单击 **“确定”**。  
  
14. 在“对象资源管理器”**** 中，展开“作业”****，右键单击创建的作业，然后选择“作业开始步骤”****。  
  
     由于该作业仅包含一个步骤，因此将立即执行它。 如果作业包含多个步骤，则可选择作业的开始步骤。  
  
15. 在作业完成后，请单击 **“关闭”**。  
  
## <a name="example-2-batch-processing-a-dimension-and-a-partition-in-a-scheduled-task"></a>示例 2：批处理计划任务中的维度和分区  
 此示例中的过程演示如何创建和计划一个作业，该作业将批处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库维度并处理依赖于聚合维度的多维数据集分区。 有关批处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的详细信息，请参阅[批处理 (Analysis Services)](../multidimensional-models/batch-processing-analysis-services.md)。  
  
###  <a name="create-a-script-for-batch-processing-a-dimension-and-partition-in-a-sql-server-agent-job"></a><a name="bkmk_BatchProcess"></a>创建用于批处理 SQL Server 代理作业中的维度和分区的脚本  
  
1.  通过使用相同的数据库，展开“维度”****，右键单击“客户”**** 维度，然后选择“处理”****。  
  
2.  在 **“处理维度”** 对话框的 **“对象列表”** 下的 **“处理选项”** 列中，验证此列的选项是否为 **“处理全部”**。  
  
3.  单击 **“脚本”**。  
  
     此步骤将打开包含处理维度的 XMLA 脚本的 **“XML 查询”** 窗口。  
  
4.  在 **“处理维度”** 对话框中，单击 **“取消”** 关闭该对话框。  
  
5.  依次展开“多维数据集”****、“Adventure Works”****、“度量值组”****、“Internet 销售”**** 和“分区”****，右键单击列表中的最后一个分区，然后选择“处理”****。  
  
6.  在 **“处理分区”** 对话框的 **“对象列表”** 下的 **“处理选项”** 列中，验证此列的选项是否为 **“处理全部”**。  
  
7.  单击 **“脚本”**。  
  
     此步骤将打开另一个包含处理分区的 XMLA 脚本的 **“XML 查询”** 窗口。  
  
8.  在 **“处理分区”** 对话框中，单击 **“取消”** 关闭该编辑器。  
  
     此时，您必须合并这两个脚本，并确保先处理维度。  
  
    > [!WARNING]  
    >  如果先处理分区，则后续维度处理将导致分区变为未处理状态。 之后，必须再一次处理分区才能使其处于已处理状态。  
  
9. 在包含处理分区的 XMLA 脚本的“XMLA 查询”**** 窗口中，突出显示 `Batch` 和 `Parallel` 标记中的代码，右键单击突出显示的脚本，然后选择“复制”****。  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. 打开包含处理维度的 XMLA 脚本的 **“XMLA 查询”** 窗口。 在 `</Process>` 标记左侧的脚本中右键单击，然后选择“粘贴”****。  
  
     下面的示例显示了修改后的 XMLA 脚本。  
  
    ```  
    <Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. 突出显示修改后的 XMLA 脚本，右键单击突出显示的脚本，然后选择“复制”****。  
  
12. 此步骤会将 XMLA 脚本复制到 Windows 剪贴板中。 可以将 XMLA 脚本保留在剪贴板中、将其保存到文件中或将其粘贴到记事本或其他文本编辑器中。  
  
###  <a name="create-and-schedule-the-batch-processing-job"></a><a name="bkmk_Scheduling"></a>创建和计划批处理作业  
  
1.  连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，然后打开对象资源管理器。  
  
2.  展开 **“SQL Server 代理”**。 如果该服务尚未运行，请启动该服务。  
  
3.  右键单击“作业”****，然后选择“新建作业”****。  
  
4.  在 **“新建作业”** 对话框的 **“名称”** 中，输入作业名称。  
  
5.  在 **“步骤”** 中，单击 **“新建”**。  
  
6.  在 **“新建作业步骤”** 对话框的 **“步骤名称”** 中，输入步骤名称。  
  
7.  在 **“类型”** 中，选择 **“SQL Server Analysis Services 命令”**。  
  
8.  在 **“运行身份”** 中，选择 **“SQL Server 代理服务帐户”**。 回想“先决条件”部分中所述的内容，此帐户必须对 Analysis Services 具有管理权限。  
  
9. 在 **“服务器”** 中，指定 Analysis Services 实例的服务器名称。  
  
10. 在“命令”**** 中，右键单击并选择“粘贴”****。  
  
11. 单击“确定”  。  
  
12. 在 **“计划”** 页上，单击 **“新建”**。  
  
13. 在 **“新建作业计划”** 对话框的 **“名称”** 中，输入计划名称，然后单击 **“确定”**。  
  
     此步骤将创建一个于星期日 12:00 AM 启动的计划。 下一步将说明如何手动执行作业。 您还可选择将在监视作业时执行作业的计划。  
  
14. 单击 **“确定”** 关闭对话框。  
  
15. 在“对象资源管理器”**** 中，展开“作业”****，右键单击创建的作业，然后选择“作业开始步骤”****。  
  
     由于该作业仅包含一个步骤，因此将立即执行它。 如果作业包含多个步骤，则可选择作业的开始步骤。  
  
16. 在作业完成后，请单击 **“关闭”**。  
  
## <a name="see-also"></a>另请参阅  
 [处理选项和设置的 &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [在 Analysis Services 中编写管理任务脚本](../script-administrative-tasks-in-analysis-services.md)  
  
  
