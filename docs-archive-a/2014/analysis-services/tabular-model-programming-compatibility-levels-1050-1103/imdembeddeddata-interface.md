---
title: IMDEmbedded 接口 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 9dba8c68-4bef-4c2b-815c-c286f1a1939b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 331f8c33f7748e6591acd6d6ecda7a03ef7d8137
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580426"
---
# <a name="imdembedded-interface"></a>IMDEmbedded 接口
  IMDEmbedded 接口是用于管理嵌入的 PowerPivot 数据库或表格模型数据库的公共接口。 此接口继承自 `IPersistStream` 接口。 此接口允许以下操作：  
  
-   获取对容器文档中嵌入流的标识符。  
  
-   设置包含文档的 URL。  
  
-   设置一个标志，以便指示嵌入应用程序是否处于宿主环境中。  
  
-   设置嵌入应用程序使用的临时文件的路径。  
  
-   取消当前嵌入的操作。  
  
-   获取用于保存嵌入对象的流的估计大小 (以字节为单位) 。 从 `IPersistStream` 继承。  
  
-   验证嵌入的数据库自上次保存后是否已更改。 从 `IPersistStream` 继承。  
  
-   将嵌入的数据库加载到本地或进程内引擎。 从 `IPersistStream` 继承。  
  
-   将本地或进程内数据库保存到容器文档中的嵌入流。 从 `IPersistStream` 继承。  
  
## <a name="reference"></a>参考  
 以下参考文档介绍了 `IMDEmbedded` **msmd.h**头文件中显示的接口。  
  
### <a name="source-file-pxoembeddeddataidl"></a>源文件：PXOEmbeddedData.idl  
  
```  
[  
  local,                            
  object,                           
  uuid(6B6691CF-5453-41c2-ADD9-4F320B7FD421),                       
  pointer_default(unique)           
]  
interface IMDEmbeddedData : IPersistStream  
{  
 [id(1), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in] BOOL in_fIsHosted);  
  
 [id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
  
 [id(3), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
  
 [id(4), helpstring("Set the path used by the embedding application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
  
 [id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
};  
```  
  
### <a name="imdembeddeddatagetstreamidentifier"></a>IMDEmbeddedData::GetStreamIdentifier  
  
```  
HRESULT GetStreamIdentifier (  
    [out, retval] BSTR * out_pbstrStreamId  
    )  
```  
  
#### <a name="description"></a>说明  
 获取宿主应用程序使用的针对容器文档中嵌入流的标识符。  
  
#### <a name="parameters"></a>参数  
 *out_pbstrStreamId*  
 指定流标识符的位置。  
  
#### <a name="return-value"></a>返回值  
 `S_OK`  
 流标识符已成功返回。  
  
 `S_FALSE`  
 没有流标识符。  
  
 `E_FAIL`  
 在访问流标识符时出现错误。  
  
#### <a name="remarks"></a>备注  
 为了确认当前连接是否包含嵌入数据库，用户应从 OLE DB 连接属性查看 DBPROP_MSMD_EMBEDDED_DATA 属性的值。  
  
 DBPROP_MSMD_EMBEDDED_DATA 的可能值包括：  
  
|名称|值|定义|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|没有可用的嵌入数据库|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|当前应用程序包含嵌入数据库|  
|DBPROPVAL_EMBED_LINKED|0x02|嵌入数据库在远程应用程序（例如 SharePoint Server）中承载|  
  
#### <a name="source"></a>源  
  
```  
[id(1), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
```  
  
### <a name="imdembeddeddatasetcontainerurl"></a>IMDEmbeddedData::SetContainerURL  
  
```  
HRESULT SetContainerURL (  
    [in] BSTR in_bstrURL  
    )  
```  
  
#### <a name="description"></a>说明  
 设置包含嵌入流的文件的 URL。  
  
#### <a name="parameters"></a>参数  
 *in_bstrURL*  
 指定包含文档的 URL。  
  
#### <a name="return-value"></a>返回值  
 `S_OK`  
 容器 URL 已成功设置。  
  
 `E_FAIL`  
 在设置容器 URL 时出错。  
  
#### <a name="source"></a>源  
  
```  
[id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
```  
  
### <a name="imdembeddeddatasethosted"></a>IMDEmbeddedData::SetHosted  
  
```  
HRESULT SetHosted (  
    [in] BOOL in_fIsHosted  
    )  
```  
  
#### <a name="description"></a>说明  
 设置一个标志，以便指示嵌入应用程序是否处于宿主环境中。  
  
#### <a name="parameters"></a>参数  
 *in_ftHosted*  
 如果调用方在服务应用程序（例如 IIS）中承载，则为 TRUE。  
  
#### <a name="return-value"></a>返回值  
 `S_OK`  
 该标志已成功设置。  
  
 `E_FAIL`  
 在设置标志时出错。  
  
#### <a name="source"></a>源  
  
```  
[id(5), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in]  BOOL in_fIsHosted);  
```  
  
### <a name="imdembeddeddatasettempdirpath"></a>IMDEmbeddedData::SetTempDirPath  
  
```  
HRESULT SetTempDirPath (  
    [in] BSTR in_bstrPath  
    )  
```  
  
#### <a name="description"></a>说明  
 设置嵌入应用程序使用的临时文件的路径。  
  
#### <a name="parameters"></a>参数  
 *in_bstrPath*  
 宿主应用程序用于临时文件的路径。  
  
#### <a name="return-value"></a>返回值  
 `S_OK`  
 临时文件目录已成功设置。  
  
 `E_FAIL`  
 在设置路径时出错。  
  
#### <a name="source"></a>源  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>说明  
 取消当前嵌入的数据库操作  
  
#### <a name="parameters"></a>参数  
 无。  
  
#### <a name="return-value"></a>返回值  
 `S_OK`  
 操作已成功取消。  
  
 `DB_E_CANTCANCEL`  
 当前没有正在进行中的可取消操作。  
  
 `E_FAIL`  
 在取消嵌入的操作时出错。  
  
#### <a name="source"></a>源  
  
```  
[id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
```  
  
### <a name="imdembeddeddatagetsizemax-ipersiststreamgetsizemax"></a>IMDEmbeddedData::GetSizeMax (IPersistStream::GetSizeMax)  
  
```  
HRESULT GetSizeMax (  
    [out] ULARGE_INTEGER * out_pcbSize  
    )  
```  
  
#### <a name="description"></a>说明  
 获取流的估计大小（以字节为单位）以便保存嵌入的对象。 从 `IPersistStream` 继承。  
  
#### <a name="parameters"></a>参数  
 *in_bstrPath*  
 嵌入的数据库图像的估计大小（以字节为单位）。  
  
#### <a name="return-value"></a>返回值  
 `S_OK`  
 该大小已成功获取。  
  
 `E_FAIL`  
 在获取大小时出错。  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>说明  
 确认自上次保存后嵌入的数据库是否已更改。 从 `IPersistStream` 继承。  
  
#### <a name="parameters"></a>参数  
 无  
  
#### <a name="return-values"></a>返回值 (s)   
 `S_OK`  
 自上次保存后数据库已更改。  
  
 `S_FALSE`  
 自上次保存后数据库未更改。  
  
 `E_FAIL`  
 在获取数据库状态时出错。  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>说明  
 将嵌入的数据库加载到本地或进程内引擎。 从 `IPersistStream` 继承。  
  
#### <a name="parameters"></a>参数  
 *in_pStm*  
 指向从其加载嵌入的数据库的流接口的指针。  
  
#### <a name="return-values"></a>返回值 (s)   
 `S_OK`  
 数据库已成功加载。  
  
 `E_OUTOFMEMORY`  
 没有足够的内存可用来加载数据库。  
  
 `E_FAIL`  
 在加载数据库时出错，不同于 `E_OUTOFMEMORY`。  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>说明  
 将本地或进程内数据库保存到容器文档中的嵌入流中。 从 `IPersistStream` 继承。  
  
#### <a name="parameters"></a>参数  
 *in_pStm*  
 指向将嵌入的数据库保存到的流接口的指针。  
  
 *in_fClearDirty*  
 一个标志，该标志指示在此操作后是否应清除脏标志。  
  
#### <a name="return-values"></a>返回值 (s)   
 `S_OK`  
 数据库已成功保存。  
  
 `STG_E_CANTSAVE`  
 在保存数据库时出错，不同于 `STG_E_MEDIUMFULL`。  
  
 `STG_E_MEDIUMFULL`  
 因为在存储设备上没有剩余空间，所以该数据库无法保存。  
  
  
