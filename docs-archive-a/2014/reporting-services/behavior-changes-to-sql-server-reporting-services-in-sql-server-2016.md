---
title: SQL Server 2014 中 SQL Server Reporting Services 的行为更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- rows [Reporting Services], heights
- leading blanks
- installing Reporting Services, behavior changes with release
- cryptography [Reporting Services]
- Setup [Reporting Services], behavior changes with release
- DefaultValueQueryBased property
- encryption [Reporting Services]
- decryption [Reporting Services]
- blank characters [SQL Server]
- initializing installations [Reporting Services]
- behavior changes [Reporting Services]
ms.assetid: 2a767f0f-84f2-4099-8784-1e37790f858e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 966447192c492a907f0b506ae21befd513b2fcfc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579533"
---
# <a name="behavior-changes-to-sql-server-reporting-services--in-sql-server-2014"></a>SQL Server 2014 中 SQL Server Reporting Services 的行为更改
  本主题介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的行为更改。 与早期版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 相比， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的功能的工作或交互方式会受到行为更改的影响。  
  
 本主题内容：  
  
-   [SQL Server 2014 Reporting Services 行为更改](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services 行为更改](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services 行为更改](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-behavior-changes"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Reporting Services 行为更改  
 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中没有 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]行为上的更改。  
  
##  <a name="sssql11-reporting-services-behavior-changes"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Reporting Services 行为更改  
 本节介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式的行为更改。  
  
### <a name="view-items-permission-will-not-download-shared-datasets-sharepoint-mode"></a>“查看项”权限将不会下载共享数据集（SharePoint 模式）  
 **新行为：** 具有 "查看项" SharePoint 权限的用户无法再下载 Reporting Services 共享数据集的内容。 此行为更改现在与针对报表、数据源和模型的 "查看项" 权限一致。 具有 "查看项" 权限的用户可以查看和执行报表、数据源和模型，但无法下载其内容。  
  
 **以前的行为：** 具有 "查看项" SharePoint 权限的用户可以下载 Reporting Services 共享数据集的内容。  
  
 有关 SharePoint 权限级别的详细信息，请参阅 [用户权限和权限级别](https://technet.microsoft.com/library/cc721640.aspx)。  
  
### <a name="report-server-trace-logs-are-in-a-new-location-for-sharepoint-mode-sharepoint-mode"></a>报表服务器跟踪日志位于 SharePoint 模式的新位置（SharePoint 模式）  
 **新行为：** 对于在 SharePoint 模式下安装的 Report Server，Report Server 跟踪日志将位于%Programfiles%\Common Files\Microsoft Shared\Web Server Extensions\14\Web Services\reportserver\logfiles 下。  
  
 **以前的行为：** 报表服务器跟踪日志位于如下路径下：%Programfilesdir%\Microsoft SQL Server \\<RS_instance> \Reporting Services\LogFiles  
  
### <a name="getserverconfiginfo-soap-api-is-no-longer-supported-sharepoint-mode"></a>GetServerConfigInfo SOAP API 不再受支持（SharePoint 模式）  
 **新行为**：使用 PowerShell Cmdlet "get-sprsserviceapplicationservers"  
  
 **以前的行为：** 客户可以开发 SOAP 客户端代码以便直接与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 终结点进行通信，并 ( # A1 调用 GetReportServerConfigInfo。  
  
### <a name="report-server-configuration-and-management-tools"></a>报表服务器配置和管理工具  
  
#### <a name="configuration-manager-is-not-used-for-sharepoint-mode"></a>配置管理器不用于 SharePoint 模式  
 **新行为：**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Configuration Manager 不再支持 SharePoint 模式报表服务器。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式的配置现在可以通过使用 SharePoint 管理中心来完成，因此 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 配置管理器不再支持 SharePoint 模式。 配置管理器现在仅用于本机模式报表服务器。  
  
#### <a name="you-cannot-change-the-server-from-one-mode-to-another"></a>无法将服务器从一种模式更改为另一种模式  
 **新行为：** 无法更改服务器模式。 如果您以本机模式安装了报表服务器，则无法将其更改或重新配置为 SharePoint 模式。 如果在 SharePoint 模式中进行安装，则可以将报表服务器更改为本机模式。  
  
 **先前行为：** 客户在 SharePoint 模式中安装 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器。 如果客户想要将报表服务器切换为本机模式，可以打开 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 配置管理器，通过创建新的本机模式数据库或连接到现有的本机模式数据库，来切换为本机模式。 客户还可以使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 配置管理器从 SharePoint 模式切换为本机模式。  
  
##  <a name="sql-server-2008-r2-reporting-services-behavior-changes"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services 行为更改  
 本节介绍中的行为更改 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。  
  
> [!NOTE]  
>  因为 SQL Server 2008 R2 是 SQL Server 2008 的次版本升级，所以，我们建议您也查看 SQL Server 2008 部分的内容。  
  
### <a name="secureconnectionlevel-property-in-the-reporting-services-wmi-provider-library"></a>Reporting Services WMI 提供程序库中的 SecureConnectionLevel 属性  
 在的 WMI 提供程序库中 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ， **SecureConnectionLevel**属性允许、、、的值， `0` `1` `2` `3` `0` 它指示安全套接字层 (ssl) 对于任何 web 服务方法均不需要 ssl， `3` 指示所有 web 服务方法均需要 ssl，并 `1` `2` 指示需要 ssl 的 web 服务方法的子集。 在中 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ，这些值将只有两个可能的含义：  
  
-   `0` 指示对于任何 Web 服务方法均不需要 SSL。  
  
-   正整数指示对于所有 Web 服务方法均需要 SSL。  
  
 此更改将影响报表服务器响应 Web 服务调用的方式。 例如， <xref:ReportService2005.ReportingService2005.ListSecureMethods%2A> 如果**SecureConnectionLevel**设置为0，并且中的所有方法均 <xref:ReportService2005.ReportingService2005> 设置为**SecureConnectionLevel** `1` 、或，则返回 nothing `2` `3` 。  
  
## <a name="see-also"></a>另请参阅  
 [新增功能 &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [SQL Server 2014 的 SQL Server Reporting Services 中的不推荐使用的功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [SQL Server 2014 中的 SQL Server Reporting Services 已停止使用的功能](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [SQL Server 2014 的 SQL Server Reporting Services 中的重大更改](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)  
  
  
