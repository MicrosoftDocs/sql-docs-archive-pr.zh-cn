---
title: 第 2 课：创建事务发布的订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: rothja
ms.author: jroth
ms.openlocfilehash: dbf40fa259302dffdd6c0b8e8717b7c35b0cf92d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578059"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>第 2 课：创建事务发布的订阅
  在本课程中，将使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创建一个订阅。 本课程要求已完成上一课， [第 1 课：使用事务复制发布数据](lesson-1-publishing-data-using-transactional-replication.md)。  
  
### <a name="to-create-the-subscription"></a>创建订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”**** 文件夹。  
  
2.  在“本地发布”**** 文件夹中，右键单击“AdvWorksProductTrans”**** 发布，然后单击“新建订阅”****。  
  
     新建订阅向导将启动。  
  
3.  在“发布”页上，选择“AdvWorksProductTrans”****，然后单击“下一步”****。  
  
4.  在“分发代理位置”页上，选择“在分发服务器上运行所有代理”****，然后单击“下一步”****。  
  
5.  在“订阅服务器”页上，如果未显示订阅服务器实例名称，请单击“添加订阅服务器”****，然后单击“添加 SQL Server 订阅服务器”****，在“连接到服务器”**** 对话框中输入订阅服务器实例名称，然后单击“连接”****。  
  
6.  在 "订阅服务器" 页上，选择订阅服务器的实例名称，然后 **\<New Database>** 在 "**订阅数据库**" 下选择。  
  
7.  在“新建数据库”**** 对话框的“数据库名称”**** 框中输入“ProductReplica”****，然后依次单击“确定”**** 和“下一步”****。  
  
8.  在 "**分发代理安全性**" 对话框中，单击省略号 (**...** ") 按钮， \<_Machine_Name> 在"**进程帐户**"框中输入 _**\ repl_distribution** ，输入此帐户的密码，单击 **" 确定**"，然后单击"**下一步**"。  
  
9. 单击“完成”**** 以接受其余页中的默认值并完成向导。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在订阅服务器上设置数据库权限  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的订阅服务器，依次展开“数据库”****、“ProductReplica”**** 和“安全性”****，右键单击“用户”****，然后选择“新建用户”****。  
  
2.  在“常规”**** 页的“用户类型”**** 列表中选择“Windows 用户”****。  
  
3.  选择 "**用户名**" 框，然后单击省略号 ( ... ) "按钮，在"**输入要选择的对象名称 "** 框中键入 <Machine_Name **>\ Repl_distribution**中，单击"**检查名称**"，然后单击 **" 确定 "**。  
  
4.  在“成员资格”**** 页的“数据库角色成员资格”**** 区域中，选择“db_owner”****，然后单击“确定”**** 以创建用户。  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>查看订阅的同步状态  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”**** 文件夹。  
  
2.  在“本地发布”**** 文件夹中，展开“AdvWorksProductTrans”**** 发布，右键单击“ProductReplica”**** 数据库中的订阅，然后单击“查看同步状态”****。  
  
     系统将显示订阅的当前同步状态。  
  
3.  如果订阅未在“AdvWorksProductTrans”**** 下出现，请按 F5 刷新列表。  
  
## <a name="next-steps"></a>后续步骤  
 您已经成功创建了对事务发布的订阅。 因为此订阅的分发代理持续运行，所以订阅一经创建就进行了初始化。 接下来，您将用跟踪令牌来验证更改是否已复制到订阅服务器并确定滞后时间。 请参阅 [第 3 课：验证订阅和测量滞后时间](lesson-3-validating-the-subscription-and-measuring-latency.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用快照初始化订阅](initialize-a-subscription-with-a-snapshot.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
