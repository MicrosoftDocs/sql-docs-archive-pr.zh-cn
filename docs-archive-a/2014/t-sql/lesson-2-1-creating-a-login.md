---
title: 创建登录名 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 400a57693fbea10270a51f5735a19b9639112ce9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692064"
---
# <a name="creating-a-login"></a>创建登录名
  若要访问 [!INCLUDE[ssDE](../includes/ssde-md.md)]，用户需要有登录名。 登录名可以将用户身份表示为 Windows 帐户或 Windows 组成员，登录名也可以是仅存在于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登录名。 应该尽可能使用 Windows 身份验证。  
  
 默认情况下，计算机上的管理员具有对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的完全访问权限。 在本课中，我们需要一个具有更少特权的用户；因此，您将在计算机上创建一个新的本地 Windows 身份验证帐户。 为此，您必须是计算机上的管理员。 然后您将授予该新用户访问 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的权限。  
  
### <a name="to-create-a-new-windows-account"></a>创建新的 Windows 帐户  
  
1.  单击 "**开始**"，再单击 "**运行**"，在 "**打开**" 框中键入 `%SystemRoot%\system32\compmgmt.msc /s` ，然后单击 **"确定"** 以打开 "计算机管理" 程序。  
  
2.  在“系统工具”下，展开“本地用户和组”，右键单击“用户”，再单击“新建用户”。****************  
  
3.  在“用户名”框中，键入“Mary”。********  
  
4.  在“密码”和“确认密码”框中，键入强密码，再单击“创建”创建新的本地 Windows 用户。************  
  
### <a name="to-create-a-login"></a>创建登录名  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的查询编辑器窗口中，键入并执行以下代码（将 `computer_name` 替换为您计算机的名称）。 `FROM WINDOWS` 表示 Windows 对用户进行身份验证。 除非连接字符串指示其他数据库，否则可选的 `DEFAULT_DATABASE` 参数将 `Mary` 连接到 `TestData` 数据库。 此语句引入了分号作为 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句的可选结束符。  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
     这将授权通过计算机的身份验证的用户名 `Mary`访问此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。 如果计算机上存在多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，则必须在 `Mary` 必须访问的每个实例上创建登录名。  
  
    > [!NOTE]  
    >  因为 `Mary` 不是域帐户，所以此用户名只能在此计算机上进行身份验证。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [授予访问数据库的权限](lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a>另请参阅  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [选择身份验证模式](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
