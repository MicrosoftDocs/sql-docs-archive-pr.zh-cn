---
title: 选择目标（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e4bf9b717ef9de20d84d32c18eb3caa4c54cad87
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588644"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>选择目标（SQL Server 导入和导出向导）
  使用 "**选择目标**" 页可以指定要复制的数据的目标。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解用于启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="static-options"></a>静态选项  
 **目标**  
 选择与目标的数据存储格式相匹配的数据访问接口。 可用于数据源的访问接口可能不止一个。 例如，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、用于 SQL Server 的 .NET Framework 数据提供程序或用于 SQL Server 的 Microsoft OLE DB 提供程序。  
  
> [!NOTE]  
>  若要将数据保存到 ODBC 目标，请选择用于 ODBC 的 .NET Framework 数据访问接口。  
  
 "**数据源**" 属性的选项数量可变，这取决于计算机上安装的提供程序。 下表列出了一些常用目标的选项。 有关其他访问接口的信息，请参阅访问接口特定的文档。  
  
## <a name="dynamic-options"></a>动态选项  
 以下部分显示了可用于几种数据源的选项。 此处并未列出“目标”下拉列表中的所有可用目标。  
  
### <a name="destination--sql-server-native-client-or-microsoft-ole-db-provider-for-sql-server"></a>目标 = SQL Server Native Client 或 Microsoft OLE DB Provider for SQL Server  
 **服务器名称**  
 键入接收数据的服务器的名称，或者从列表中选择服务器。  
  
 **Use Windows Authentication**  
 指定包是否应使用 Microsoft Windows 身份验证登录数据库。 为了实现更好的安全性，建议使用 Windows 身份验证。  
  
 **Use SQL Server Authentication**  
 指定包是否应使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录数据库。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
 **用户名**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，指定数据库连接的用户名。  
  
 **密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，提供数据库连接的密码。  
  
 **Database**  
 从的指定实例上的数据库列表中进行选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，或单击 "**新建**" 创建新的数据库。  
  
 **“刷新”**  
 通过单击“刷新”****，还原可用数据库的列表。  
  
 **新建**  
 使用 "**创建数据库**" 对话框创建新的目标数据库。  
  
### <a name="destination--flat-file-destination"></a>目标 = 平面文件目标  
 **文件名**  
 指定要存储数据的文件的路径和文件名。 或者，单击 **“浏览”** 定位文件。  
  
 **“浏览”**  
 使用“打开”**** 对话框定位文件。  
  
 **区域设置**  
 指定定义字符排序顺序以及日期和时间格式的区域设置 ID (LCID)。  
  
 **Unicode**  
 指示是否使用 Unicode。 如果使用 Unicode，则不必指定代码页。  
  
 **代码页**  
 指定所需使用的语言的代码页。  
  
 **格式**  
 指示是否使用带分隔符、固定宽度或右边未对齐的格式。  
  
|值|说明|  
|-----------|-----------------|  
|带分隔符|各列之间由在 **“列”** 页上指定的分隔符隔开。|  
|固定宽度|列的宽度固定。|  
|右边未对齐|在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由行分隔符进行分隔。|  
  
 **文本限定符**  
 键入要使用的文本限定符。 例如，您可以指定每个文本列均包含在引号中。  
  
 **第一个数据行中的列名称**  
 指示是否希望在第一个数据行中显示列名称。  
  
### <a name="destination--microsoft-excel"></a>目标 = Microsoft Excel  
  
> [!NOTE]  
>  仅当要连接到使用 Excel 2003 或更早版本的数据源时，才选择 " **Microsoft Excel** "。 若要连接到使用 Excel 2007 的数据源，请选择**Microsoft Office 12.0 Access 数据库引擎 OLE DB 提供程序**，单击 "**属性**"，然后在 "**数据链接属性**" 对话框的 "**全部**" 选项卡上，对于 "**扩展属性**"，输入 `Excel 12.0` 。  
  
 **Excel 文件路径**  
 指定要在其中存储数据的工作簿的路径和文件名 (例如，C:\MyData.xls， \\\Sales\Database\Northwind.xls) 。 或者，单击 **“浏览”** 定位工作簿。  
  
 **“浏览”**  
 使用 "**打开**" 对话框定位到 Excel 工作簿。  
  
 **Excel 版本**  
 选择目标工作簿使用的 Excel 版本。  
  
> [!NOTE]  
>  将数据导出到 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 目标时，向导将使用“ [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel 目标”组件。 有关某些使用注意事项和已知问题的信息，请参阅[Excel Destination](../data-flow/excel-destination.md)。  
  
### <a name="destination--microsoft-access"></a>目标 = Microsoft Access  
  
> [!NOTE]  
>  仅当要连接到使用 Access 2003 或更早版本的数据库时，才选择 " **Microsoft Access** "。 若要连接到使用 Access 2007 的数据库，请选择 " **Microsoft Office 12.0 访问数据库引擎 OLE DB 提供程序**"。  
  
 **文件名**  
 指定要在其中存储 (数据的数据库文件的路径和文件名，例如 C:\MyData.mdb、 \\ \Sales\Database\Northwind.mdb) 。 或者，单击 **“浏览”** 定位数据库文件。  
  
 **“浏览”**  
 使用 "**打开**" 对话框浏览到数据库文件。  
  
 **用户名**  
 当工作组信息文件与数据库关联时，为数据库连接指定一个有效的用户名。  
  
 **密码**  
 当工作组信息文件与数据库关联时，为数据库连接提供相应的用户密码。 但是，如果对于所有用户都使用一个密码保护数据库，则必须在 **“数据链接属性”** 对话框（可通过 **“高级”** 按钮访问）中提供此值。  
  
 **高级**  
 通过使用“数据链接属性”**** 对话框指定高级选项，例如数据库密码或非默认工作组信息文件。 有关 OLE DB 访问接口属性的详细信息，请在 [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553)的“Data Access”（数据访问）部分中进行搜索。  
  
  
