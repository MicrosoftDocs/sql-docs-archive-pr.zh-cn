---
title: 访问 DQS 操作数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 88dfb9ea-6321-4eaf-b9e4-45d36ef048f6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 515b087a8d16e44314d1a21d3dfbd6f13c767f5c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690174"
---
# <a name="access-data-for-the-dqs-operations"></a>访问 DQS 操作数据
  若要将您的源数据用于 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 操作并导出已处理的数据，您可以执行以下任一操作：  
  
-   将您的源数据复制到 DQS_STAGING_DATA 数据库中的某个表/视图，然后再将其用于 DQS 操作。 还可以将已处理的数据导出到 DQS_STAGING_DATA 数据库的新表中。 为此，必须向您的 Windows 用户帐户授予对 DQS_STAGING_DATA 数据库的读/写访问权限。  
  
-   使用您自己的数据库作为 DQS 操作的源数据，以及导出已处理的数据的目标。 为此，请确保你的数据库与数据质量服务器数据库在同一个 SQL Server 实例中。 否则，该数据库将无法在数据质量客户端中用于 DQS 操作。 此外，为导出匹配结果，必须向你的 Windows 用户帐户授予对 DQS_STAGING_DATA 数据库的访问权限，因为匹配结果分为两个阶段进行导出：首先，匹配结果导出到 DQS_STAGING_DATA 数据库的临时表中，然后移到你的目标数据库的表中。  
  
## <a name="prerequisites"></a>先决条件  
  
-   您必须已通过运行 DQSInstaller.exe 文件完成了 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安装。 有关详细信息，请参阅 [运行 DQSInstaller.exe 以便完成数据质量服务器安装](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
-   为授予/修改对数据库上 SQL 登录名的访问权限，您的 Windows 用户帐户必须是数据库引擎实例中相应固定服务器角色（例如 securityadmin、serveradmin 或 sysadmin）的成员。  
  
### <a name="to-grant-readwrite-access-to-a-user-on-the-dqs_staging_data-database"></a>向用户授予对 DQS_STAGING_DATA 数据库的读/写访问权限  
  
1.  启动 Microsoft SQL Server Management Studio。  
  
2.  在 Microsoft SQL Server Management Studio 中，依次展开您的 SQL Server 实例、 **“安全性”** 和 **“登录名”**。  
  
3.  右键单击某一 SQL 登录名，然后单击 **“属性”**。  
  
4.  在 **“登录属性”** 对话框的左侧窗格中，单击 **“用户映射”** 页。  
  
5.  在右侧窗格中，选中 **DQS_STAGING_DATA** 数据库的 **“映射”** 列下的复选框，然后在 **“数据库角色成员身份: DQS_STAGING_DATA”** 窗格中选择以下角色：  
  
    -   **db_datareader**：从表/视图中读取数据。  
  
    -   **db_datawriter**：在表中添加、删除或更改数据。  
  
    -   **db_ddladmin**：创建、修改或删除表/视图。  
  
6.  在 **“登录属性”** 对话框中，单击 **“确定”** 以应用所做的更改。  
  
## <a name="next-steps"></a>后续步骤  
 尝试执行 DQS 操作，这些操作访问数据库来作为 DQS 操作的数据源，然后将处理后的数据导出到数据库。  
  
## <a name="see-also"></a>另请参阅  
 [安装 Data Quality Services](install-data-quality-services.md)  
  
  
