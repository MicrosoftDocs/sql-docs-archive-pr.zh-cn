---
title: 创建主数据管理器 Web 服务代理类 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c4f25d749f829357f6541f14073e654bade27215
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591922"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>创建主数据管理器 Web 服务代理类
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服务可让您通过任何能访问 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 网站的计算机以编程方式使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的功能。 在开始编写访问 Web 服务的代码之前，必须先生成代理类。 您用于执行 Web 服务操作的主代理类是 <xref:Microsoft.MasterDataServices.ServiceClient> 类，它可实现 <xref:Microsoft.MasterDataServices.IService> 接口。  
  
## <a name="enable-web-service-metadata-publishing"></a>启用 Web 服务元数据发布  
 在可以生成代理类之前，必须启用 Web 服务元数据发布。 请按照下列步骤完成此操作：  
  
1.  在文本编辑器中打开 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.配置文件。 此文件位于 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装路径的 WebApplication 文件夹中。  
  
2.  查找 `mdsWsHttpBehavior` 下面的部分 **\<serviceBehaviors>** 。 对于 **\<serviceMetadata>** 元素，将设置 `httpGetEnabled` 为 `true` 。  
  
    > [!NOTE]  
    >  如果您想要通过安全套接字层 (SSL) 启用 Web 服务，请在 web.config 文件的 `httpsGetEnabled` 部分中将 `true` 设置为 `mdsWsHttpBehavior`。 您还需要更改 `mdsWsHTTPBinding`，以便也为 SSL 配置它，并且注释掉非 SSL 部分。  
  
3.  保存对文件的更改。  
  
4.  通过浏览服务 URL 来测试元数据发布，例如：http://yourserver/MDS/service/service.svc。 如果启用元数据发布，则会显示一个以   
    “你已创建服务”开头的页面。  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>通过使用 Visual Studio 创建代理类  
 如果已安装了 Visual Studio 2010，则生成代理类的最简方法是将“服务引用”添加到项目中****。 服务引用的地址为 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序的 URL，后面追加 /service/service.svc。 例如： http://yourserver/MDS/service/service.svc。 有关详细信息，请参阅[如何添加、更新或删除服务引用](https://go.microsoft.com/fwlink/?LinkId=221167)。  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>使用 Svcutil.exe 创建代理类  
 必须 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 安装或 Windows SDK，才能在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 计算机上 Svcutil.exe。 如果使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，必须使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 命令提示符运行该命令。 有关详细信息，请参阅 [ServiceModel 元数据实用工具 (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027) 和[根据服务元数据生成 WCF 客户端](https://go.microsoft.com/fwlink/?LinkId=164821)。  
  
 若要使用 Svcutil.exe 创建一组 C# 代理类，请使用如下命令：  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 其中：  
  
-   servername:port 是承载 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的计算机名称和端口号****。  
  
-   virtual_path 是 Internet 信息服务 (IIS) 中 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的虚拟路径**。  
  
-   proxy_name 是生成的代理文件名称**。  
  
## <a name="see-also"></a>另请参阅  
 [分类的 Web 服务操作 &#40;Master Data Services&#41;](categorized-web-service-operations-master-data-services.md)  
  
  
