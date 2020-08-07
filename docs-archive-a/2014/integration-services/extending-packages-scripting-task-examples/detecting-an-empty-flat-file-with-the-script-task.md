---
title: 使用脚本任务检测空平面文件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 379b11bd18752ad648fc5f24d11d9ed5bfb63e14
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587471"
---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>使用脚本任务检测空平面文件
  平面文件源在尝试处理平面文件之前不确定该平面文件是否包含数据行。 您可能希望跳过不含任何数据行的文件，从而提高包的效率，尤其是循环访问大量平面文件的包。 脚本任务可以在包开始处理数据流之前查找空平面文件。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>说明  
 下面的示例使用 `System.IO` 命名空间中的方法来测试在平面文件连接管理器中指定的平面文件，以确定该文件是否是空的，或者是否只包含预期的非数据行，例如，列标题或空行。 该脚本先检查文件的大小，如果大小为零字节，则该文件是空的。 如果文件大小大于零，该脚本会从文件中读取行，直到没有行可读为止，或者直到行数超过预期的非数据行数为止。 如果该文件中的行数小于或等于预期的非数据行数，则认为该文件是空的。 结果将以布尔值的形式在用户变量中返回，该变量的值可用于在包控制流中进行分支跳转。 `FireInformation`方法还会**Output**在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] (VSTA) 的应用程序的工具的 "输出" 窗口中显示结果。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
1.  创建并配置一个名为的平面文件连接管理器 `EmptyFlatFileTest` 。  
  
2.  创建一个名为 `FFNonDataRows` 的整数变量，并将其值设置为预期在平面文件中出现的非数据行数。  
  
3.  创建一个名为 `FFIsEmpty` 的布尔变量。  
  
4.  将 `FFNonDataRows` 变量添加到脚本任务的 **ReadOnlyVariables** 属性中。  
  
5.  将 `FFIsEmpty` 变量添加到脚本任务的 **ReadWriteVariables** 属性中。  
  
6.  在您的代码中，导入 `System.IO` 命名空间。  
  
 如果使用的是 Foreach 文件枚举器来循环访问文件，而不是使用单个平面文件连接管理器，则需要修改下面的代码，以便从存储枚举值的变量中而不是从连接管理器获取文件名和路径。  
  
### <a name="code"></a>代码  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
![Integration Services 图标 (小型) ](../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [脚本任务示例](../extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
