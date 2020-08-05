---
title: 报表服务器状态 (SSRS 本机模式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serverstatus.F1
ms.assetid: 2f63ad1c-1bc2-449d-b451-fb39a0060838
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c2fb2860fd80b827e48ad72b59192573d16b8a4d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577227"
---
# <a name="report-server-status-ssrs-native-mode"></a>报表服务器状态（SSRS 本机模式）
  使用此页可以查看当前连接的报表服务器实例的有关信息。 此页是报表服务器配置的起始页。 此外还提供了用于配置 URL、服务帐户、报表服务器数据库、报表服务器电子邮件传递、扩展部署和加密密钥的其他页。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。  
  
 若要打开此页，请启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器并连接到报表服务器实例。 有关详细信息，请参阅[&#40;del&#41;Reporting Services 配置管理器](reporting-services-configuration-manager-native-mode.md)。  
  
> [!TIP]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安装 Configuration Manager ( # A0) 的权限级别为 "highestAvailable"。 此行为是设计使然。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器要求与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI API 进行通信。 一些 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 通信要求更高级别的权限或管理权限。  
  
 如果连接到报表服务器，但所有页面链接均显示为灰色，请验证是否已启动报表服务器服务。 **报表服务状态：** 应为 "已启动"。 还可以使用“管理工具”中的“服务”控制台应用程序检查服务状态。  
  
## <a name="options"></a>选项  
 **SQL Server 实例**  
 显示当前连接的报表服务器实例的有关信息。 报表服务器实例的名称基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例。 默认实例为 MSSQLSERVER。 命名实例将是您在安装过程中指定的值。 有关实例的详细信息，请参阅联机丛书中的[使用多个版本和实例 SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!NOTE]  
>  在具有高级服务的 SQL Server Express 中，默认实例为 SQLExpress。  
  
 **实例 ID**  
 与文件系统中的某一文件夹对应，该文件夹用于存储您所连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的程序文件。 **“实例 ID”** 值是由安装程序分配的，格式为 *component*.*instance*，其中 *component* 为一个表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的值， *instance* 为实例名称。 默认实例名为 MSSQLSERVER。 例如，如果安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件的默认实例，则对应的文件夹名称分别为：  
  
-   MSSQL12.MSSQLSERVER  
  
-   MSAS12.MSSQLSERVER  
  
-   MSRS12.MSSQLSERVER  
  
 如果安装已安装组件（例如）的第二个实例， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 并为该实例命名为 Contoso，则**实例 ID**为 mssql12.mssqlserver。Contoso.  
  
 **版本**  
 显示版本信息。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)。  
  
 **产品版本**  
 显示所安装的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的版本。  
  
 **报表服务器数据库**  
 显示用于存储当前报表服务器实例的应用程序数据的报表服务器数据库的名称。  
  
 **报表服务器模式**  
 这应始终显示值 **“本机”**。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的配置管理器仅支持本机模式的报表服务器。 如果您看到值 **SharePoint 集成模式**，它可能指示您的本机模式部署未正确配置，您需要连接到本机模式的报表目录。 使用配置管理器的 **“数据库”** 页更改数据库并创建新数据库或连接到现有本机模式的报表服务器数据库目录。  
  
 **服务器状态**  
 显示报表服务器服务是否正在运行。  
  
 **启动**  
 启动报表服务器服务。 在更改某些配置之后（例如，在更改计算机名称之后重新配置报表服务器时），需要重新启动该服务。 如果重新配置 URL 预留，该服务将自动重新启动。 要使更改生效，必须重新启动服务。  
  
 **Stop**  
 停止报表服务器服务。 停止服务会导致报表服务器停止工作。 有关详细信息，请参阅联机丛书中[的启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置管理器的 F1 帮助主题 &#40;SSRS 本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services 配置管理器 &#40;del&#41;](/sql/sql-server/install/reporting-services-configuration-manager-native-mode)   
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
