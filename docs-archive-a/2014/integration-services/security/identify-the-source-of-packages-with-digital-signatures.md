---
title: 使用数字签名标识包的源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 90c0e2e3db13ba4b228b70ccfffddbc2ff221774
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694508"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>使用数字签名标识包的源
  可以使用数字证书对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 进行签名以标识其来源。 使用数字证书对包进行签名后，可以让 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在加载包之前先检查数字签名。 若要让 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 能够检查签名，请在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 **dtexec** 实用工具 (dtexec.exe) 中设置一个选项，或设置一个可选的注册表值。  
  
## <a name="signing-a-package-with-a-digital-certificate"></a>使用数字证书对包进行签名  
 必须首先获取或创建数字证书，才能使用该证书对包进行签名。 获取证书后，即可使用该证书对包进行签名。 有关如何获取证书以及如何使用该证书对包进行签名的详细信息，请参阅 [使用数字证书对包签名](../sign-a-package-by-using-a-digital-certificate.md)。  
  
## <a name="setting-an-option-to-check-the-package-signature"></a>设置选项以检查包的签名  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 **dtexec** 实用工具都提供了用于将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 配置为检查签名包的数字签名的选项。 使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 还是 **dtexec** 实用工具取决于你是想检查所有包，还是只想检查特定的包：  
  
-   若要在设计时加载包之前检查所有包的数字签名，请在 **中设置** “加载包时检查数字签名” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项。 此选项是针对 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中所有包的全局设置。 有关详细信息，请参阅 [General Page](../general-page-of-integration-services-designers-options.md)。  
  
-   若要检查个别包的数字签名，请在 `/VerifyS[igned]` 使用**dtexec**实用工具运行包时指定选项。 有关详细信息，请参阅 [dtexec Utility](../packages/dtexec-utility.md)。  
  
## <a name="setting-a-registry-value-to-check-the-package-signature"></a>设置注册表值以检查包的签名  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]还支持可选的注册表值**BlockedSignatureStates**，可以使用它来管理组织用于加载签名包和未签名包的策略。 如果包未签名、签名无效或不可信，使用该注册表值将不允许加载该包。 有关如何设置此注册表值的详细信息，请参阅 [通过设置注册表值实现签名策略](../implement-a-signing-policy-by-setting-a-registry-value.md)。  
  
> [!NOTE]  
>  可选的 **BlockedSignatureStates** 注册表值可指定比在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中或 **dtexec** 命令行中设置的数字签名选项限制性更强的设置。 在这种情况下，限制性更强的注册表设置将覆盖其他设置。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS&#41; 包](../integration-services-ssis-packages.md)   
 [安全性概述 (Integration Services)](security-overview-integration-services.md)  
  
  
