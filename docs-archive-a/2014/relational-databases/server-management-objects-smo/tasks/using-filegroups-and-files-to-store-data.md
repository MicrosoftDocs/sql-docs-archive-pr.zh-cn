---
title: 使用文件组和文件存储数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
author: stevestein
ms.author: sstein
ms.openlocfilehash: 15ac5fd0c43c9b58432a774ae11aeb6500f0403b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590137"
---
# <a name="using-filegroups-and-files-to-store-data"></a><span data-ttu-id="ccb5c-102">使用文件组和文件存储数据</span><span class="sxs-lookup"><span data-stu-id="ccb5c-102">Using Filegroups and Files to Store Data</span></span>
  <span data-ttu-id="ccb5c-103">数据文件可用于存储数据库文件。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-103">Data files are used to store database files.</span></span> <span data-ttu-id="ccb5c-104">数据文件可细分为文件组。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-104">The data files are subdivided into file groups.</span></span> <span data-ttu-id="ccb5c-105"> 对象具有  属性，该属性引用  对象。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-105">The <xref:Microsoft.SqlServer.Management.Smo.Database> object has a <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> property that references a <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection> object.</span></span> <span data-ttu-id="ccb5c-106">该集合中的每个 <xref:Microsoft.SqlServer.Management.Smo.FileGroup> 对象都具有 <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A> 属性。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-106">Each <xref:Microsoft.SqlServer.Management.Smo.FileGroup> object in that collection has a <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A> property.</span></span> <span data-ttu-id="ccb5c-107">此属性引用 <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> 集合，该集合包含属于数据库的所有数据文件。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-107">This property refers to a <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> collection that contains all the data files that belong to the database.</span></span> <span data-ttu-id="ccb5c-108">文件组主要用于将用于存储数据库对象的文件组合在起来。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-108">A file group is principally used to group files together that are used to store a database object.</span></span> <span data-ttu-id="ccb5c-109">将一个数据库对象分布到几个文件上的一个原因是，它可以提高性能，尤其是在文件存储在不同磁盘驱动器上时。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-109">One reason for spreading a database object over several files is that it can improve performance, especially if the files are stored on different disk drives.</span></span>  
  
 <span data-ttu-id="ccb5c-110">自动创建的每个数据库都具有一个名为“Primary”的文件组和一个与数据库同名的数据文件。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-110">Every database that is created automatically has a file group named "Primary" and a data file with the same name as the database.</span></span> <span data-ttu-id="ccb5c-111">其他文件和组可以添加到集合中。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-111">Additional files and groups can be added to the collections.</span></span>  
  
## <a name="examples"></a><span data-ttu-id="ccb5c-112">示例</span><span class="sxs-lookup"><span data-stu-id="ccb5c-112">Examples</span></span>  
 <span data-ttu-id="ccb5c-113">对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-113">For the following code examples, you will have to select the programming environment, programming template and the programming language to create your application.</span></span> <span data-ttu-id="ccb5c-114">有关详细信息，请参阅[在 Visual studio .net 中创建 VISUAL BASIC SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 visual Studio .Net 中创建 VISUAL C&#35; smo 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-114">For more information, see [Create a Visual Basic SMO Project in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) and [Create a Visual C&#35; SMO Project in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).</span></span>  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a><span data-ttu-id="ccb5c-115">在 Visual Basic 中将 FileGroups 和 DataFiles 添加到数据库</span><span class="sxs-lookup"><span data-stu-id="ccb5c-115">Adding FileGroups and DataFiles to a Database in Visual Basic</span></span>  
 <span data-ttu-id="ccb5c-116">主文件组和数据文件将自动使用默认属性值创建。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-116">The primary file group and data file are created automatically with default property values.</span></span> <span data-ttu-id="ccb5c-117">代码示例指定了一些可以使用的属性值。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-117">The code example specifies some property values that you can use.</span></span> <span data-ttu-id="ccb5c-118">否则，将使用默认属性值。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-118">Otherwise, the default property values are used.</span></span>  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups1](SMO How to#SMO_VBFileGroups1)]  -->  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a><span data-ttu-id="ccb5c-119">在 Visual C# 中将 FileGroups 和 DataFiles 添加到数据库</span><span class="sxs-lookup"><span data-stu-id="ccb5c-119">Adding FileGroups and DataFiles to a Database in Visual C#</span></span>  
 <span data-ttu-id="ccb5c-120">主文件组和数据文件将自动使用默认属性值创建。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-120">The primary file group and data file are created automatically with default property values.</span></span> <span data-ttu-id="ccb5c-121">代码示例指定了一些可以使用的属性值。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-121">The code example specifies some property values that you can use.</span></span> <span data-ttu-id="ccb5c-122">否则，将使用默认属性值。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-122">Otherwise, the default property values are used.</span></span>  
  
```csharp
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a><span data-ttu-id="ccb5c-123">在 PowerShell 中将 FileGroups 和 DataFiles 添加到数据库</span><span class="sxs-lookup"><span data-stu-id="ccb5c-123">Adding FileGroups and DataFiles to a Database in PowerShell</span></span>  
 <span data-ttu-id="ccb5c-124">主文件组和数据文件将自动使用默认属性值创建。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-124">The primary file group and data file are created automatically with default property values.</span></span> <span data-ttu-id="ccb5c-125">代码示例指定了一些可以使用的属性值。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-125">The code example specifies some property values that you can use.</span></span> <span data-ttu-id="ccb5c-126">否则，将使用默认属性值。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-126">Otherwise, the default property values are used.</span></span>  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a><span data-ttu-id="ccb5c-127">在 Visual Basic 中创建、更改和删除日志文件</span><span class="sxs-lookup"><span data-stu-id="ccb5c-127">Creating, Altering, and Removing a Log File in Visual Basic</span></span>  
 <span data-ttu-id="ccb5c-128">代码示例将创建 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 对象，更改其中一个属性，然后将其从数据库中删除。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-128">The code example creates a <xref:Microsoft.SqlServer.Management.Smo.LogFile> object, changes one of the properties, and then removes it from the database.</span></span>  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups3](SMO How to#SMO_VBFileGroups3)]  -->  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a><span data-ttu-id="ccb5c-129">在 Visual C# 中创建、更改和删除日志文件</span><span class="sxs-lookup"><span data-stu-id="ccb5c-129">Creating, Altering, and Removing a Log File in Visual C#</span></span>  
 <span data-ttu-id="ccb5c-130">代码示例将创建 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 对象，更改其中一个属性，然后将其从数据库中删除。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-130">The code example creates a <xref:Microsoft.SqlServer.Management.Smo.LogFile> object, changes one of the properties, and then removes it from the database.</span></span>  
  
```csharp
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.
            lf1.Drop();
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a><span data-ttu-id="ccb5c-131">在 PowerShell 中创建、更改和删除日志文件</span><span class="sxs-lookup"><span data-stu-id="ccb5c-131">Creating, Altering, and Removing a Log File in PowerShell</span></span>  
 <span data-ttu-id="ccb5c-132">代码示例将创建 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 对象，更改其中一个属性，然后将其从数据库中删除。</span><span class="sxs-lookup"><span data-stu-id="ccb5c-132">The code example creates a <xref:Microsoft.SqlServer.Management.Smo.LogFile> object, changes one of the properties, and then removes it from the database.</span></span>  
  
```powershell
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()
```  
  
## <a name="see-also"></a><span data-ttu-id="ccb5c-133">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ccb5c-133">See Also</span></span>  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [<span data-ttu-id="ccb5c-134">数据库文件和文件组</span><span class="sxs-lookup"><span data-stu-id="ccb5c-134">Database Files and Filegroups</span></span>](../../databases/database-files-and-filegroups.md)  
