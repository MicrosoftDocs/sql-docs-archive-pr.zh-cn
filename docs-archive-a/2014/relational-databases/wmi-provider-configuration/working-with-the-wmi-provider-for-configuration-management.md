---
title: 使用 WMI 提供程序进行配置管理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 80f311fb0abae2337f6ea4a5d5d85aaa0d320b94
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586538"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>使用 WMI 提供程序进行配置管理
  在使用用于计算机管理的 WMI 提供程序编程之前，请考虑下列事项：  
  
## <a name="binding"></a>绑定  
 用于配置管理的 WMI 提供程序是一个 COM 对象模型，它支持早期绑定和后期绑定。 借助后期绑定，您可以使用脚本语言（如 VBScript）以编程方式操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、网络设置和别名。  
  
 有关使用脚本语言对 WMI 提供程序实现进行编程的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN[网站](https://go.microsoft.com/fwlink/?linkid=15426)。  
  
## <a name="specifying-a-connection-string"></a>指定连接字符串  
 应用程序通过连接到 WMI 提供程序所定义的 WMI 命名空间，将用于配置管理的该提供程序定向到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 Windows WMI 服务将此命名空间映射到提供程序 DLL 并将其加载到内存。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例均由一个 WMI 命名空间表示。 默认命名空间为  
  
```  
\\.\root\Microsoft\SqlServer\ComputerManagement12\instance_name  
```  
  
 其中 `instance_name` 默认为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认安装中的 `MSSQLSERVER`。  
  
 **注意：** 如果要通过 Windows 防火墙进行连接，则需要确保计算机配置正确。 请参阅 MSDN 网站上 Windows Management Instrumentation 文档中的 "通过 Windows 防火墙连接" 一文 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。 [Web site](https://go.microsoft.com/fwlink/?linkid=15426)  
  
## <a name="permissions-and-server-authentication"></a>权限和服务器身份验证  
 若要访问用于配置管理的 WMI 提供程序，客户端 WMI 管理脚本必须在目标计算机上的管理员上下文中运行。 您需要具有要管理的计算机上的本地 Windows Administrators 组的成员身份。  
  
 管理员可以设置组策略以控制用户对 WMI 提供程序的访问。 有关设置组策略的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器帮助中的“组策略和 MMC”。  
  
 WMI 管理脚本可用于更新运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务所使用的帐户。  
  
 用于配置管理的 WMI 提供程序支持安全证书。 有关证书的详细信息，请参阅[加密层次结构](../security/encryption/encryption-hierarchy.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 配置管理器](../sql-server-configuration-manager.md)  
  
  
