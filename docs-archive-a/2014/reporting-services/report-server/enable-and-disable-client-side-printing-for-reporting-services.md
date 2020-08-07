---
title: 启用和禁用 Reporting Services 的客户端打印 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 031a7cd9b5da07b03b76b6bf49db63572a8fe546
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588277"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>启用和禁用 Reporting Services 的客户端打印
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]ActiveX 控件**RSClientPrint**为在浏览器中查看的报表提供客户端打印。 该控件显示一个自定义打印对话框，它支持其他打印对话框常见的功能。 这些功能包括打印预览、指定特定页和范围的页面选择、页边距和打印方向等功能。 虽然默认情况下将启用客户端打印功能，但是您也可以将其禁用，以禁止使用该功能。  
  
> [!NOTE]  
>  下载 ActiveX 控件需要管理员权限。  
  
## <a name="downloading-the-activex-control"></a>下载 ActiveX 控件  
 对于希望使用打印功能的每个用户来说，都必须下载并安装提供客户端打印功能的 ActiveX 控件。 用户首次单击报表工具栏上的**打印机**图标时，Microsoft ActiveX 控件将下载到计算机。 在下载该控件后，每当用户单击**打印机**图标时，都会显示 "**打印**" 对话框。  
  
 根据浏览器设置的不同，系统可能会提示用户安装控件，阻止用户安装控件，或者在后台透明地安装控件。  
  
 对于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer，可通过 Web 内容区域的 "**安全设置**" 页中的 " **ActiveX 控件和插件**" 节点来指定影响 ActiveX 控件下载和安装的设置。 以下设置基于 Web 区域安全首选项，确定用户是否可以下载和运行打印控件：  
  
-   下载已签名的 ActiveX 控件。  
  
-   对标记为可安全执行脚本的 ActiveX 控件执行脚本。  
  
-   运行 ActiveX 控件和插件。  
  
 希望使用**RSClientPrint**执行客户端打印的用户必须启用以下各项：  
  
-   **下载已签名的 activex 控件**和**脚本 activex 控件**，并将其标记为安全，以便进行安装。  
  
-   为正在进行的打印操作**运行 ActiveX 控件和插件**。  
  
 **RSClientPrint** ActiveX 控件已签名，这意味着它包含中的有效数字证书 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
## <a name="enabling-and-disabling-client-side-printing"></a>启用和禁用客户端打印功能  
 报表服务器管理员可以通过将 Report Server 系统属性**EnableClientPrinting**设置为来禁用打印功能 `false` 。 这将对该服务器管理的所有报表禁用客户端打印功能。 默认情况下， **EnableClientPrinting**设置为 `true` 。 您可以通过下列方式禁用客户端打印功能：  
  
-   对于本机模式下的报表服务器 ****：  
  
    1.  使用管理权限启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    2.  连接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的报表服务器实例。  
  
    3.  右键单击报表服务器节点，然后单击“属性”****。 如果 **“属性”** 选项被禁用，请确认您是在使用管理权限启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 。  
  
    4.  选择 **"启用 ActiveX 客户端打印控件的下载"**。  
  
    5.  单击“确定”。  
  
-   对于 SharePoint 模式报表服务器 ****：  
  
    1.  在 SharePoint 管理中心中，单击 **“应用程序管理”**。  
  
    2.  单击 **“管理服务应用程序”**。  
  
    3.  单击 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的名称，然后在 SharePoint 功能区中单击 "**管理**"。  
  
    4.  单击 **“系统设置”**。  
  
    5.  选择 **“启用客户端打印”**。 **“启用客户端打印”** 选项位于页面的底部附近。  
  
    6.  单击“确定”。  
  
-   编写脚本或代码，以将 Report Server 系统属性**EnableClientPrinting**设置为`false.`  
  
 下面的示例脚本说明了一种禁用客户端打印功能的方法。 编译并运行以下 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 代码，将 EnableClientPrinting**** 属性设置为 False****。 在运行代码后，请重新启动 IIS。  
  
### <a name="sample-script"></a>示例脚本  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```  
  
  
