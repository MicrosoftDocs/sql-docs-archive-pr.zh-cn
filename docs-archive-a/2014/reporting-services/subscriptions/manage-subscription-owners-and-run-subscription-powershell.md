---
title: 使用 PowerShell 更改和列出 Reporting Services 订阅所有者并运行订阅 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0fa6cb36-68fc-4fb8-b1dc-ae4f12bf6ff0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b274dc190d8830a2cf7b55110f15267a00c581e2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587165"
---
# <a name="use-powershell-to-change-and-list-reporting-services-subscription-owners-and-run-a-subscription"></a>Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription
  从 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 开始，可通过编程方式将 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 订阅的所有权从一个用户转移给另一个用户。 本主题提供多个 Windows PowerShell 脚本，这些脚本可用于更改订阅所有权，或只是列出订阅所有权。 每个示例都包含本机模式和 SharePoint 模式的语法示例。 更改订阅的所有者后，订阅将在新所有者的安全上下文中执行，并且报表中的 User!UserID 字段将显示新所有者的值。 有关 PowerShell 示例调用的对象模型的详细信息，请参阅 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>

 ![PowerShell 相关内容](../media/rs-powershellicon.jpg "PowerShell 相关内容")

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式|

 **本主题内容：**

-   [如何使用脚本](#bkmk_how_to)

-   [脚本：列出所有订阅的所有权](#bkmk_list_ownership_all)

-   [脚本：列出特定用户拥有的全部订阅](#bkmk_list_all_one_user)

-   [脚本：更改特定用户拥有的全部订阅的所有权](#bkmk_change_all)

-   [脚本：列出与特定报表关联的全部订阅](#bkmk_list_for_1_report)

-   [脚本：更改特定订阅的所有权](#bkmk_change_all_1_subscription)

-   [脚本：运行（触发）单个订阅](#bkmk_run_1_subscription)

##  <a name="how-to-use-the-scripts"></a><a name="bkmk_how_to"></a> 如何使用脚本

### <a name="permissions"></a>权限
 本节总结了使用各本机模式和 SharePoint 模式 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]方法所需的权限级别。 本主题中的脚本使用以下 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 方法：

-   [ReportingService2010.ListSubscriptions 方法](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listsubscriptions.aspx)

-   [ReportingService2010.ChangeSubscriptionOwner 方法](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.changesubscriptionowner.aspx)

-   [ReportingService2010.ListChildren](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listchildren.aspx)

-   [ReportingService2010.FireEvent](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.fireevent.aspx) 方法仅在最后一个脚本中使用，以触发特定订阅运行。 如果不计划使用该脚本，则可以忽略针对 FireEvent 方法的权限要求。

 **本机模式：**

-   列出订阅：报表上 ( HYPERLINK " https://technet.microsoft.com/library/microsoft.reportingservices.interfaces.reportoperation.aspx " READSUBSCRIPTION，用户是订阅所有者) 或 ReadAnySubscription

-   更改订阅：用户必须是 BUILTIN\Administrators 组的成员

-   列出子级：项上的 ReadProperties

-   触发事件：GenerateEvents（系统）

 **SharePoint 模式：**

-   列出订阅：报表上的 Managealerts or 或 ( HYPERLINK " https://technet.microsoft.com/library/microsoft.sharepoint.spbasepermissions.aspx " CREATEALERTS，用户是订阅所有者，订阅是计时订阅) 。

-   更改订阅：ManageWeb

-   列出子级：ViewListItems

-   触发事件：ManageWeb

 有关详细信息，请参阅 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)。

### <a name="script-usage"></a>脚本使用情况
 **创建脚本文件 (.ps1)**

1.  创建一个名为 **c:\scripts**的文件夹。 如果选择不同的文件夹，则请修改命令行语法语句示例中使用的文件夹名称。

2.  为每个脚本创建文本文件并将文件保存至 c:\scripts 文件夹。 创建 .ps1 时，请使用各命令行语法示例中的名称。

3.  使用管理员权限打开命令提示符。

4.  使用各示例提供的示例命令行语法运行各脚本文件。

 **经测试的环境**

 本主题中的脚本已在 PowerShell 版本 3 上和以下版本的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]上进行了测试：

-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]

-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]

-   [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]

##  <a name="script-list-the-ownership-of-all-subscriptions"></a><a name="bkmk_list_ownership_all"></a> 脚本：列出全部订阅的所有权
 此脚本列出站点上的所有订阅。 可以使用此脚本测试连接或验证在其他脚本中使用的报表路径和订阅 ID。 这也是用于轻松审核存在哪些订阅以及它们的所有者是谁的一个有用脚本。

### <a name="native-mode-syntax"></a>纯模式语法

```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/reportserver" "/"
```

### <a name="sharepoint-mode-syntax"></a>SharePoint 模式语法

```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/_vti_bin/reportserver" "http://[server]"
```

### <a name="script"></a>Script

```powershell
# Parameters
#    server   - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)

Param(
    [string]$server,
    [string]$site
   )

$rs2010 += New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;
$subscriptions += $rs2010.ListSubscriptions($site); # use "/" for default native mode site

Write-Host " "
Write-Host "----- $server's Subscriptions: "
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted, Status
```

> [!TIP]
>  要在 SharePoint 模式下验证站点 URL，请使用 SharePoint cmdlet **Get-SPSite**。 有关详细信息，请参阅 [Get-SPSite](https://technet.microsoft.com/library/ff607950\(v=office.15\).aspx)。

##  <a name="script-list-all-subscriptions-owned-by-a-specific-user"></a><a name="bkmk_list_all_one_user"></a> 脚本：列出特定用户拥有的全部订阅
 此脚本列出特定用户拥有的全部订阅。 可以使用此脚本测试连接或验证在其他脚本中使用的报表路径和订阅 ID。 当有人离开您的组织，而您想要验证他们拥有哪些订阅，以便更改所有者或删除订阅时，此脚本非常有用。

### <a name="native-mode-syntax"></a>纯模式语法

```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]" "[server]/reportserver" "/"
```

### <a name="sharepoint-mode-syntax"></a>SharePoint 模式语法

```cmd
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]"  "[server]/_vti_bin/reportserver" "http://[server]"
```

### <a name="script"></a>Script

```powershell
# Parameters:
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change
#    server        - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)
#    site        - use "/" for default native mode site
Param(
    [string]$currentOwner,
    [string]$server,
    [string]$site
)

$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;
$subscriptions += $rs2010.ListSubscriptions($site);

Write-Host " "
Write-Host " "
Write-Host "----- $currentOwner's Subscriptions: "
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.owner -eq $currentOwner}
```

##  <a name="script-change-ownership-for-all-subscriptions-owned-by-a-specific-user"></a><a name="bkmk_change_all"></a> 脚本：更改特定用户拥有的全部订阅的所有权
 此脚本将特定用户拥有的全部订阅的所有权更改为新所有者参数。

### <a name="native-mode-syntax"></a>纯模式语法

```cmd
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\current owner]" "[Domain]\[new owner]" "[server]/reportserver"
```

### <a name="sharepoint-mode-syntax"></a>SharePoint 模式语法

```cmd
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\{current owner]" "[Domain]\[new owner]" "[server]/_vti_bin/reportserver"
```

### <a name="script"></a>Script

```powershell
# Parameters:
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change
#    newOwner      - DOMAIN\USER that will own the subscriptions you wish to change
#    server        - server and instance name (e.g. myserver/reportserver, myserver/reportserver_db2, myserver/_vti_bin/reportserver)

Param(
    [string]$currentOwner,
    [string]$newOwner,
    [string]$server
)

$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;
$items = $rs2010.ListChildren("/", $true);

$subscriptions = @();

ForEach ($item in $items)
{
    if ($item.TypeName -eq "Report")
    {
        $curRepSubs = $rs2010.ListSubscriptions($item.Path);
        ForEach ($curRepSub in $curRepSubs)
        {
            if ($curRepSub.Owner -eq $currentOwner)
            {
                $subscriptions += $curRepSub;
            }
        }
    }
}

Write-Host " "
Write-Host " "
Write-Host -foregroundcolor "green" "-----  $currentOwner's Subscriptions changing ownership to $newOwner : "
$subscriptions | select SubscriptionID, Owner, Path, Description,  Status  | format-table -AutoSize

ForEach ($sub in $subscriptions)
{
    $rs2010.ChangeSubscriptionOwner($sub.SubscriptionID, $newOwner);
}

$subs2 = @();

ForEach ($item in $items)
{
    if ($item.TypeName -eq "Report")
    {
        $subs2 += $rs2010.ListSubscriptions($item.Path);
    }
}
```

##  <a name="script-list-all-subscriptions-associated-with-a-specific-report"></a><a name="bkmk_list_for_1_report"></a> 脚本：列出与特定报表关联的全部订阅
 此脚本列出与特定报表关联的全部订阅。 报表路径语法是需要完整 URL 的不同 SharePoint 模式。 语法示例中使用的报表名称是“title only”，包含一个空格，因此报表名称两边需要带单引号。

### <a name="native-mode-syntax"></a>纯模式语法

```cmd
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/reportserver" "'/reports/title only'" "/"
```

### <a name="sharepoint-mode-syntax"></a>SharePoint 模式语法

```cmd
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/_vti_bin/reportserver"  "'http://[server]/shared documents/title only.rdl'" "http://[server]"
```

### <a name="script"></a>Script

```powershell
# Parameters:
#    server      - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)
#    reportpath  - path to report in the report server, including report name e.g. /reports/test report >> pass in  "'/reports/title only'"
#    site        - use "/" for default native mode site
Param
(
      [string]$server,
      [string]$reportpath,
      [string]$site
)

$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;
$subscriptions += $rs2010.ListSubscriptions($site);

Write-Host " "
Write-Host " "
Write-Host "----- $reportpath 's Subscriptions: "
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.path -eq $reportpath}
```

##  <a name="script-change-ownership-of-a-specific-subscription"></a><a name="bkmk_change_all_1_subscription"></a> 脚本：更改特定订阅的所有权
 此脚本更改特定订阅的所有权。 订阅由传递到脚本中的 SubscriptionID 标识。 可以使用所列订阅脚本之一来确定正确的 SubscriptionID。

### <a name="native-mode-syntax"></a>纯模式语法

```cmd
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/reportserver" "/" "ac5637a1-9982-4d89-9d69-a72a9c3b3150"
```

### <a name="sharepoint-mode-syntax"></a>SharePoint 模式语法

```cmd
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/_vti_bin/reportserver" "http://[server]" "9660674b-f020-453f-b1e3-d9ba37624519"
```

### <a name="script"></a>Script

```powershell
# Parameters:
#    newOwner       - DOMAIN\USER that will own the subscriptions you wish to change
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)
#    site        - use "/" for default native mode site
#    subscriptionID - guid for the single subscription to change

Param(
    [string]$newOwner,
    [string]$server,
    [string]$site,
    [string]$subscriptionid
   )
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;

$subscription += $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid};

Write-Host " "
Write-Host "----- $subscriptionid's Subscription properties: "
$subscription | select Path, report, Description, SubscriptionID, Owner, Status

$rs2010.ChangeSubscriptionOwner($subscription.SubscriptionID, $newOwner)

#refresh the list
$subscription = $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid}; # use "/" for default native mode site
Write-Host "----- $subscriptionid's Subscription properties: "
$subscription | select Path, report, Description, SubscriptionID, Owner, Status
```

##  <a name="script-run-fire-a-single-subscription"></a><a name="bkmk_run_1_subscription"></a> 脚本：运行（触发）单个订阅
 此脚本将使用 FireEvent 方法运行特定订阅。 无论为订阅配置的计划如何，该脚本都将立即运行订阅。 EventType 与在报表服务器配置文件 **rsreportserver.config** 中定义的一组已知事件匹配。该脚本为标准订阅使用以下事件类型：

 `<Event>`

 `<Type>TimedSubscription</Type>`

 `</Event>`

 有关配置文件的详细信息，请参阅 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)。

 脚本包括延迟逻辑“`Start-Sleep -s 6`”，因此事件触发后尚有时间可供更新状态用于 ListSubscription 方法。

### <a name="native-mode-syntax"></a>纯模式语法

```cmd
powershell c:\scripts\FireSubscription.ps1 "[server]/reportserver" $null "70366e82-2d3c-4edd-a216-b97e51e26de9"
```

### <a name="sharepoint-mode-syntax"></a>SharePoint 模式语法

```cmd
powershell c:\scripts\FireSubscription.ps1 "[server]/_vti_bin/reportserver" "http://[server]" "c3425c72-580d-423e-805a-41cf9799fd25"
```

### <a name="script"></a>Script

```powershell
# Parameters
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)
#    site           - use $null for a native mode server
#    subscriptionid - subscription guid

Param(
  [string]$server,
  [string]$site,
  [string]$subscriptionid
  )

$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;
#event type is case sensative to what is in the rsreportserver.config
$rs2010.FireEvent("TimedSubscription",$subscriptionid,$site)

Write-Host " "
Write-Host "----- Subscription ($subscriptionid) status: "
#get list of subscriptions and filter to the specific ID to see the Status and LastExecuted
Start-Sleep -s 6 # slight delay in processing so ListSubscription returns the updated Status and LastExecuted
$subscriptions = $rs2010.ListSubscriptions($site); 
$subscriptions | select Status, Path, report, Description, Owner, SubscriptionID, EventType, lastexecuted | where {$_.SubscriptionID -eq $subscriptionid}
```

## <a name="see-also"></a>另请参阅
 <xref:ReportService2010.ReportingService2010.ListSubscriptions%2A> <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A> 
 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 
 <xref:ReportService2010.ReportingService2010.FireEvent%2A>
