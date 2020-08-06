---
title: 连接到服务器（“登录”页）(Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttodtsserver.login.f1
- sql12.swb.connecttodts.login.f1
ms.assetid: 402c2de4-f4ea-40b0-909f-3ddf3bd59950
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 285518f4a1f3d9180d2c3c07a41bf75a00ea3593
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693067"
---
# <a name="connect-to-server-login-page-integration-services"></a>连接到服务器（“登录”页）(Integration Services)
  在连接到时，使用此选项卡可以查看或指定以下选项 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
## <a name="options"></a>选项  
 **服务器类型**  
 从对象资源管理器进行服务器注册时，请选择要连接到何种类型的服务器： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”  框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择[!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。  
  
 **服务器名称**  
 选择要连接到的服务器。 默认情况下，显示上次连接到的服务器实例。  
  
> [!NOTE]  
>  不要使用 *\<servername>* \\ *\<instancename>* ，因为不 [!INCLUDE[ssIS](../includes/ssis-md.md)] 支持计算机上的多个实例。  
  
 **身份验证**  
 只有 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 身份验证可用于 [!INCLUDE[ssIS](../includes/ssis-md.md)]。 Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。  
  
 **用户名**  
 由于只有 Windows 身份验证可用于 [!INCLUDE[ssIS](../includes/ssis-md.md)]，因此此选项不可用。  
  
 **密码**  
 由于只有 Windows 身份验证可用于 [!INCLUDE[ssIS](../includes/ssis-md.md)]，因此此选项不可用。  
  
 **记住密码**  
 由于只有 Windows 身份验证可用于 [!INCLUDE[ssIS](../includes/ssis-md.md)]，因此此选项不可用。  
  
 **“连接”**  
 连接到在上面选择的服务器。  
  
 **选项**  
 单击此项可更改对话框并隐藏其他服务器连接选项，例如记住密码。  
  
  
