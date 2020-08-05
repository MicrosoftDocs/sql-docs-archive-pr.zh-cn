---
title: 在 SharePoint 集成模式下 (Reporting Services 上设置已发布报表的参数) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- report parameters [Reporting Services]
ms.assetid: dec5d985-a6c1-4dd8-8a66-a848e89a2e18
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4d0a2b1a23f382adb9e0cdddbebcded0050d34bc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577277"
---
# <a name="set-parameters-on-a-published-report-reporting-services-in-sharepoint-integrated-mode"></a>设置已发布报表的参数（SharePoint 集成模式下的 Reporting Services）
  参数化报表可以在运行报表时接受用于筛选数据的输入值。 参数是在创建报表时定义的。 根据报表定义中报表参数的定义方式，参数可以接受单值、多值或者根据上一选择而变化的动态值（例如，选择产品类别后，下一选择可能是该类别中的特定产品）。 参数可以具有默认值，该值可用于自动运行经过筛选的报表，也可以由不同的值来代替。  
  
 这些属性可在报表定义中设置，也可以在报表发布后设置。 虽然可以在已发布报表中修改某些参数属性以更改值和显示属性，但是不能更改参数名或数据类型。 参数名称和数据类型只能由报表作者在报表定义中更改。  
  
 若要运行参数化报表，通常必须知道要键入哪些值（尽管报表可能包含用于从中选择有效值的下拉列表）。  
  
 若要设置已发布报表的参数属性，必须拥有报表的“编辑项”权限。 对于通过 SharePoint 站点运行的报表，您可以设置其部分或全部参数属性。 不可以通过保存希望重复使用的参数值组合来对报表进行个性化设置。 您指定的任何默认值都将由打开报表的所有用户使用。  
  
 如果报表嵌入报表查看器 Web 部件中，并且此部件已配置为始终显示该报表，则可以设置报表查看器 Web 部件的属性。 有关详细信息，请参阅[将报表查看器 Web 部件添加到网页（SharePoint 集成模式下的 Reporting Services）](../report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
### <a name="to-run-a-parameterized-report"></a>运行参数化报表  
  
1.  打开包含该报表的库。  
  
2.  单击报表名称。 您必须事先知道哪些报表具有参数。 报表没有表明它是参数化报表的可视标识符。  
  
3.  打开报表时，指定要使用的参数。 参数区域可能处于可见、折叠或隐藏状态，具体取决于对报表查看器 Web 部件的属性设置。  
  
    1.  如果参数区域可见，则为每个参数选择一个值。  
  
    2.  如果沿报表长度有一条细的彩条且中间带有箭头，则表明参数区域处于折叠状态。 可以单击箭头将其展开。  
  
    3.  如果参数区域是隐藏的，则不能指定值。  
  
4.  单击参数区域底部的 **“应用”** 以运行报表。  
  
     指定的值组合可能无法让您获得所需的结果。 如果您无法获得所需信息，则报表作者可能需要修改报表。  
  
5.  单击“确定”。   
  
### <a name="to-set-parameter-properties"></a>设置参数属性  
  
1.  打开包含报表的库或文件夹。  
  
2.  指向报表，然后单击向下箭头。  
  
3.  单击 **“管理参数”** 。 如果报表包含参数，页面上将列出每个参数。 此列表显示参数名称、数据类型、默认情况下使用的数据值以及打开报表时参数在参数区域中是否可见。  
  
4.  单击列表中的参数可修改其设置。  
  
5.  在“默认值”中，为参数输入值。 系统不会验证该值，因此请确保提供的值对于报表是有效的。  
  
    1.  如果希望使用创建报表时定义的默认值，请选择 **“使用报表定义中指定的值表达式”** 。 如果报表定义没有提供默认值，此选项将不可用。  
  
    2.  如果希望指定一个报表定义默认值的替换值，请选择 **“覆盖报表默认值”** 。 （可选）对于接受 Null 值的报表参数，可以选中 **Null** 复选框以防止基于该参数进行筛选。  
  
    3.  如果希望在处理报表前由每个用户来指定值，请选择 **“参数没有默认值”** 。 如果选择此选项，则应设定提示用户指定值的显示设置。  
  
     请注意，如果所有参数值都具有默认值，当用户打开报表时，报表将使用这些值自动运行。 但是，如果显示了参数区域，用户可以覆盖默认值并重新运行报表。  
  
6.  设置显示选项以确定参数是否可见。  
  
    1.  选择 **“提示用户”** 以在页面上显示参数。 您可以指定出现在字段中的提示文本，以提供有关用户必须提供的数据格式或类型的简短说明。  
  
    2.  如果使用默认值且不希望在参数区域中显示参数，请选择 **“隐藏”** 。  
  
    3.  如果使用默认值且不希望在参数区域中或订阅页上显示参数，请选择 **“内部”** 。  
  
7.  单击“应用”  。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器项的 SharePoint 站点和列表权限参考](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
  
  
