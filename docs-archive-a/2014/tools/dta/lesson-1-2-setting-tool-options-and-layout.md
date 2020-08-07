---
title: 设置工具选项和布局 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96d853a85b8ee4d451c55d7ea59af3755887be22
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690967"
---
# <a name="setting-tool-options-and-layout"></a>设置工具选项和布局
  您可以设置用于配置数据库引擎优化顾问图形用户界面 (GUI) 在启动时的显示内容、使用的字体以及其他工具功能的选项，从而为您的使用方式提供最佳支持。 通过本页的练习将让您熟悉可设置的各选项及其设置方式。  
  
### <a name="set-the-tool-options"></a>设置工具选项  
  
1.  启动数据库引擎优化顾问。 在 Windows“开始”**** 菜单中，依次指向“所有程序”****、[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] 和“性能工具”****，然后单击“数据库引擎优化顾问”****。  
  
2.  在“工具”  菜单上，单击“选项”  。  
  
3.  在“选项”**** 对话框中，查看下列选项：  
  
    -   展开“启动时”**** 列表，查看数据库引擎优化顾问在启动时可显示的内容。 默认情况下，选择“显示新会话”****。  
  
    -   单击 "**更改字体**"，查看在 "**常规**" 选项卡上可以为数据库和表的列表选择的字体。在执行优化后，为此选项选择的字体也将用于数据库引擎优化顾问建议网格和报告。 默认情况下，数据库引擎优化顾问使用系统字体。  
  
    -   “最近使用的列表中的项数”**** 可设置为 **1** 到 **10** 之间的数字。 此选项设置在单击“文件”**** 菜单上的“最近使用的会话”**** 或“最近使用的文件”**** 时，列表中可以显示的最大项数。 默认情况下，此选项设置为 **4**。  
  
    -   选中“记住我上次的优化选项”**** 时，默认情况下，数据库引擎优化顾问会将为上一优化会话指定的优化选项用于下一优化会话中。 清除此复选框，以便使用数据库引擎优化顾问优化选项的默认设置。 默认情况下选择此选项。  
  
    -   默认情况下，将选中“在永久删除会话之前询问”****，避免意外删除优化会话。  
  
    -   默认情况下，将选中“在停止会话分析之前询问”****，避免在数据库引擎优化顾问完成工作负载分析之前意外停止优化会话。  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：使用数据库引擎优化顾问](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
