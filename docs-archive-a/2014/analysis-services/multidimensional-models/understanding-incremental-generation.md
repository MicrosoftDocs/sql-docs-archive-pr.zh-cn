---
title: 了解增量生成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- incremental generation [Analysis Services]
- Schema Generation Wizard, incremental generation
- relational schema [Analysis Services], incremental generation
ms.assetid: 3ca0aa63-3eb5-4fe9-934f-8e96dee84eaa
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7a3bfef76d45d1d015e6f8a258b8df8b2ae639e9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588100"
---
# <a name="understanding-incremental-generation"></a><span data-ttu-id="94cbc-102">了解增量生成</span><span class="sxs-lookup"><span data-stu-id="94cbc-102">Understanding Incremental Generation</span></span>
  <span data-ttu-id="94cbc-103">在生成初始架构后，可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]更改多维数据集定义和维度定义，然后返回架构生成向导。</span><span class="sxs-lookup"><span data-stu-id="94cbc-103">Following the initial schema generation, you can change cube and dimension definitions by using [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], and then rerun the Schema Generation Wizard.</span></span> <span data-ttu-id="94cbc-104">向导会更新主题区域数据库和相关数据源视图中的架构以反映所做的更改，并且尽可能保留当前存在于要重新生成的表中的数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-104">The wizard updates the schema in the subject area database and in the associated data source view to reflect the changes, and retaining the data that currently exists in the tables to be regenerated, to the extent possible.</span></span> <span data-ttu-id="94cbc-105">如果在初始生成之后更改表，则架构生成向导会使用下列规则在可能的情况下保留这些更改：</span><span class="sxs-lookup"><span data-stu-id="94cbc-105">If you changed the tables after the initial generation, the Schema Generation Wizard preserves those changes when possible by using the following rules:</span></span>  
  
-   <span data-ttu-id="94cbc-106">如果表由向导在先前生成，则会被覆盖。</span><span class="sxs-lookup"><span data-stu-id="94cbc-106">If a table was previously generated by the wizard, the table is overwritten.</span></span> <span data-ttu-id="94cbc-107">通过将数据源视图中表的 `AllowChangesDuringGeneration` 属性更改为 `false`，可以防止覆盖由向导生成的表。</span><span class="sxs-lookup"><span data-stu-id="94cbc-107">You can prevent a table that was generated by the wizard from being overwritten by changing the `AllowChangesDuringGeneration` property for the table in the data source view to `false`.</span></span> <span data-ttu-id="94cbc-108">如果可对表进行控制，则该表与任何其他用户定义表的处理方式相同，并且在重新生成过程中不受影响。</span><span class="sxs-lookup"><span data-stu-id="94cbc-108">When you take control of a table, the table is treated like any other user-defined table and is not affected during regeneration.</span></span> <span data-ttu-id="94cbc-109">从生成中删除表之后，您可以稍后将数据源视图中表的 `AllowChangesDuringGeneration` 属性更改为 `true`，并重新打开该表以便向导对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="94cbc-109">After you remove a table from generation, you can later change the `AllowChangesDuringGeneration` property for the table in the data source view to `true` and reopen the table for changes by the wizard.</span></span> <span data-ttu-id="94cbc-110">有关详细信息，请参阅[在数据源视图中更改属性 (Analysis Services)](change-properties-in-a-data-source-view-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="94cbc-110">For more information, see [Change Properties in a Data Source View &#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md).</span></span>  
  
-   <span data-ttu-id="94cbc-111">如果表是通过向导以外的工具添加到数据源视图或基础数据库中，则不会被覆盖。</span><span class="sxs-lookup"><span data-stu-id="94cbc-111">If a table was added to the data source view or to the underlying database by something other than the wizard, the table is not overwritten.</span></span>  
  
 <span data-ttu-id="94cbc-112">当架构生成向导重新生成先前在主题区域数据库中生成的表时，您可以选择让向导保留这些表中的现有数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-112">When the Schema Generation Wizard regenerates tables that were previously generated in the subject area database, you can choose to have the wizard preserve existing data in those tables.</span></span>  
  
## <a name="supporting-data-preservation"></a><span data-ttu-id="94cbc-113">支持数据保留</span><span class="sxs-lookup"><span data-stu-id="94cbc-113">Supporting Data Preservation</span></span>  
 <span data-ttu-id="94cbc-114">作为通用规则，架构生成向导会保留存储在由其生成的表中的数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-114">As a general rule, the Schema Generation Wizard preserves data that is stored in the tables that it generated.</span></span> <span data-ttu-id="94cbc-115">此外，如果将列添加到向导生成的表中，则向导也会保留这些数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-115">In addition, if you add columns to tables that the wizard generated, the wizard preserves that data as well.</span></span> <span data-ttu-id="94cbc-116">您可以使用这项功能添加或修改维度和多维数据集，然后重新生成基础对象而不必重新加载存储在基础表中的数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-116">You can use this capability to add or modify your dimensions and cubes and then regenerate the underlying objects without having to reload the data stored in the underlying tables.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="94cbc-117">如果要加载分隔的文本文件中的数据，则还可以选择架构生成向导在重新生成过程中是否覆盖这些文件及其包含的数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-117">If you are loading data from delimited text files, you can also choose whether the Schema Generation Wizard overwrites these files and the data contained in them during regeneration.</span></span> <span data-ttu-id="94cbc-118">文本文件既可以完全覆盖，也可以根本不覆盖。</span><span class="sxs-lookup"><span data-stu-id="94cbc-118">Text files are either overwritten completely or not at all.</span></span> <span data-ttu-id="94cbc-119">架构生成向导不会部分覆盖这些文件。</span><span class="sxs-lookup"><span data-stu-id="94cbc-119">The Schema Generation Wizard does not partially overwrite these files.</span></span> <span data-ttu-id="94cbc-120">默认情况下，这些文件不被覆盖。</span><span class="sxs-lookup"><span data-stu-id="94cbc-120">By default, these files are not overwritten.</span></span>  
  
### <a name="partial-preservation"></a><span data-ttu-id="94cbc-121">部分保留</span><span class="sxs-lookup"><span data-stu-id="94cbc-121">Partial Preservation</span></span>  
 <span data-ttu-id="94cbc-122">在某些情况下，架构生成向导不会保留现有的数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-122">The Schema Generation Wizard cannot preserve existing data under some circumstances.</span></span> <span data-ttu-id="94cbc-123">下表提供了一些示例，用于说明在哪些情况下，向导不会在重新生成过程中保留基础表中的所有现有数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-123">The following table provides examples of situations in which the wizard cannot preserve all the existing data in the underlying tables during regeneration.</span></span>  
  
|<span data-ttu-id="94cbc-124">数据类型更改</span><span class="sxs-lookup"><span data-stu-id="94cbc-124">Type of data change</span></span>|<span data-ttu-id="94cbc-125">处理方式</span><span class="sxs-lookup"><span data-stu-id="94cbc-125">Treatment</span></span>|  
|-------------------------|---------------|  
|<span data-ttu-id="94cbc-126">不兼容的数据类型更改</span><span class="sxs-lookup"><span data-stu-id="94cbc-126">Incompatible data type change</span></span>|<span data-ttu-id="94cbc-127">架构生成向导会尽可能使用标准 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型转换，将现有数据从一种类型转换为另一种类型。</span><span class="sxs-lookup"><span data-stu-id="94cbc-127">The Schema Generation Wizard uses standard [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data type conversions, whenever possible, to convert existing data from one data type to another.</span></span> <span data-ttu-id="94cbc-128">但是，当您将属性的数据类型更改为与现有数据不兼容的类型时，向导会删除受影响列的数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-128">However, when you change an attribute's data type to a type that is incompatible with the existing data, the wizard drops the data for the affected column.</span></span>|  
|<span data-ttu-id="94cbc-129">引用完整性错误</span><span class="sxs-lookup"><span data-stu-id="94cbc-129">Referential integrity errors</span></span>|<span data-ttu-id="94cbc-130">如果在重新生成过程中更改包含数据的维度或多维数据集，并且更改导致引用完整性错误，则架构生成向导会删除外键表中的所有数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-130">If you change a dimension or cube that contains data and the change causes a referential integrity error during regeneration, the Schema Generation Wizard drops all data in the foreign key table.</span></span> <span data-ttu-id="94cbc-131">删除的数据并不限于导致违反外键约束的列或包含引用完整性错误的行。</span><span class="sxs-lookup"><span data-stu-id="94cbc-131">The data that is dropped is not limited to the column that caused the foreign key constraint violation or to the rows that contain the referential integrity errors.</span></span> <span data-ttu-id="94cbc-132">例如，如果将维度键更改为具有非唯一数据或空数据的属性，则会删除外键表中的所有现有数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-132">For example, if you change the dimension key to an attribute that has non-unique or null data, all existing data in the foreign key table is dropped.</span></span> <span data-ttu-id="94cbc-133">此外，删除某个表中的所有数据可能会产生级联影响，并可能会导致其他引用完整性被破坏。</span><span class="sxs-lookup"><span data-stu-id="94cbc-133">Furthermore, dropping all the data in one table can have a cascading effect and can cause other referential integrity violations.</span></span>|  
|<span data-ttu-id="94cbc-134">已删除的属性或维度</span><span class="sxs-lookup"><span data-stu-id="94cbc-134">Deleted attribute or dimension</span></span>|<span data-ttu-id="94cbc-135">如果从维度中删除属性，则架构生成向导会删除映射到已删除属性的列。</span><span class="sxs-lookup"><span data-stu-id="94cbc-135">If you delete an attribute from a dimension, the Schema Generation Wizard deletes the column that is mapped to the deleted attribute.</span></span> <span data-ttu-id="94cbc-136">如果删除维度，则向导会删除映射到已删除维度的表。</span><span class="sxs-lookup"><span data-stu-id="94cbc-136">If you delete a dimension, the wizard deletes the table that is mapped to the deleted dimension.</span></span> <span data-ttu-id="94cbc-137">在这些情况下，向导会删除包含在已删除列或表中的数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-137">In these cases, the wizard drops the data that is contained in the deleted column or table.</span></span>|  
  
 <span data-ttu-id="94cbc-138">架构生成向导在删除任何数据之前会发出警告，以便您可以取消向导而不丢失任何数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-138">The Schema Generation Wizard issues a warning before it drops any data so that you can cancel the wizard without losing any data.</span></span> <span data-ttu-id="94cbc-139">但是，架构生成向导不能区别预料到的数据丢失和未预料到的数据丢失。</span><span class="sxs-lookup"><span data-stu-id="94cbc-139">However, the Schema Generation Wizard is not able to differentiate between anticipated data loss and unanticipated data loss.</span></span> <span data-ttu-id="94cbc-140">当您运行向导时，便会出现一个对话框，列出包含要删除的数据的表和列。</span><span class="sxs-lookup"><span data-stu-id="94cbc-140">When you run the wizard, a dialog box lists the tables and columns that contain data that will be dropped.</span></span> <span data-ttu-id="94cbc-141">您既可以让向导继续运行并删除数据，也可以取消向导并修改对表和列所做的更改。</span><span class="sxs-lookup"><span data-stu-id="94cbc-141">You can either have the wizard continue and drop the data, or you can cancel the wizard and revise the changes you made to the tables and columns.</span></span>  
  
## <a name="supporting-cube-and-dimension-changes"></a><span data-ttu-id="94cbc-142">支持多维数据集和维度更改</span><span class="sxs-lookup"><span data-stu-id="94cbc-142">Supporting Cube and Dimension Changes</span></span>  
 <span data-ttu-id="94cbc-143">当您更改维度和多维数据集的属性时，架构生成向导会在基础主题区域数据库以及相关数据源视图中重新生成相应的对象，如下表中所述。</span><span class="sxs-lookup"><span data-stu-id="94cbc-143">When you change the properties of dimensions and cubes, the Schema Generation Wizard regenerates the appropriate objects in the underlying subject area database, as well as in the related data source view, as described in the following table.</span></span>  
  
 <span data-ttu-id="94cbc-144">删除对象，如维度、多维数据集或属性。</span><span class="sxs-lookup"><span data-stu-id="94cbc-144">Deleting an object, such as a dimension, cube, or attribute.</span></span>  
 <span data-ttu-id="94cbc-145">架构生成向导会删除已删除对象映射到的基础对象。</span><span class="sxs-lookup"><span data-stu-id="94cbc-145">The Schema Generation Wizard deletes the underlying objects to which the deleted object is mapped.</span></span> <span data-ttu-id="94cbc-146">如果将列添加到向导生成的表中，则新列并不会阻止该表被删除。</span><span class="sxs-lookup"><span data-stu-id="94cbc-146">If you add columns to a table that the wizard generated, the new columns do not prevent that table from being deleted.</span></span> <span data-ttu-id="94cbc-147">删除对象会导致存储在基础对象中的数据被删除，并且如果出现引用完整性错误，则还会导致其他数据被删除。</span><span class="sxs-lookup"><span data-stu-id="94cbc-147">Deleting an object causes the data stored in the underlying objects to be dropped, and may also cause other data to be dropped if referential integrity errors occur.</span></span>  
  
 <span data-ttu-id="94cbc-148">重命名对象，如维度、多维数据集或属性。</span><span class="sxs-lookup"><span data-stu-id="94cbc-148">Renaming an object, such as a dimension, cube, or attribute.</span></span>  
 <span data-ttu-id="94cbc-149">架构生成向导会重命名已重命名对象映射到的基础对象。</span><span class="sxs-lookup"><span data-stu-id="94cbc-149">The Schema Generation Wizard renames the underlying objects to which the renamed object is mapped.</span></span> <span data-ttu-id="94cbc-150">向导还会重命名所有受影响的对象，如主键。</span><span class="sxs-lookup"><span data-stu-id="94cbc-150">The wizard also renames all affected objects, such as primary keys.</span></span> <span data-ttu-id="94cbc-151">存储在基础对象中的现有数据将被保留。</span><span class="sxs-lookup"><span data-stu-id="94cbc-151">Existing data stored in the underlying objects is preserved.</span></span>  
  
 <span data-ttu-id="94cbc-152">修改对象，如更改其数据类型。</span><span class="sxs-lookup"><span data-stu-id="94cbc-152">Modifying an object, such as changing its data type.</span></span>  
 <span data-ttu-id="94cbc-153">架构生成向导会修改已更改对象映射到的基础对象。</span><span class="sxs-lookup"><span data-stu-id="94cbc-153">The Schema Generation Wizard modifies the underlying objects to which the changed object is mapped.</span></span> <span data-ttu-id="94cbc-154">除非新的数据类型与现有数据不兼容，否则将保留存储在数据库内基础对象中的现有数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-154">Existing data stored in the underlying objects in the databases is preserved, unless the new data type is incompatible with the existing data.</span></span>  
  
 <span data-ttu-id="94cbc-155">添加新对象，如维度、多维数据集或属性。</span><span class="sxs-lookup"><span data-stu-id="94cbc-155">Adding a new object, such as a dimension, cube, or attribute.</span></span>  
 <span data-ttu-id="94cbc-156">架构生成向导会添加新对象映射到的基础对象。</span><span class="sxs-lookup"><span data-stu-id="94cbc-156">The Schema Generation Wizard adds underlying objects to which the new object is mapped.</span></span>  
  
 <span data-ttu-id="94cbc-157">如果架构生成向导因主题区域数据库中存在用户对象而无法进行所需的更改（因为数据库引擎返回错误），则架构生成向导会失败并显示由数据库引擎返回的错误。</span><span class="sxs-lookup"><span data-stu-id="94cbc-157">If the Schema Generation Wizard cannot make the required change because of the presence of a user object in the subject area database (because the Database Engine returns an error), the Schema Generation Wizard fails and displays the error returned by the Database Engine.</span></span> <span data-ttu-id="94cbc-158">例如，如果您在向导生成表后对表创建 primary key 约束或非聚集索引，则架构生成向导不会删除该表，因为它未创建约束或索引。</span><span class="sxs-lookup"><span data-stu-id="94cbc-158">For example, if you create a primary key constraint or a nonclustered index on a table after the wizard generated the table, the Schema Generation Wizard does not drop that table because it did not create the constraint or the index.</span></span>  
  
## <a name="supporting-schema-changes"></a><span data-ttu-id="94cbc-159">支持架构更改</span><span class="sxs-lookup"><span data-stu-id="94cbc-159">Supporting Schema Changes</span></span>  
 <span data-ttu-id="94cbc-160">当您更改主题区域数据库或相关数据源视图中表或列的属性时，架构生成向导将按照下表所述处理更改。</span><span class="sxs-lookup"><span data-stu-id="94cbc-160">When you change the properties of the tables or columns in the subject area database or in the associated data source view, the Schema Generation Wizard treats the changes as described in the following table.</span></span>  
  
 <span data-ttu-id="94cbc-161">删除由架构生成向导生成的表或列。</span><span class="sxs-lookup"><span data-stu-id="94cbc-161">Deleting a table or a column generated by the Schema Generation Wizard.</span></span>  
 <span data-ttu-id="94cbc-162">如果您删除由架构生成向导生成的表或列，则向导会重新生成已删除的表。</span><span class="sxs-lookup"><span data-stu-id="94cbc-162">If you delete a table or a column generated by the Schema Generation Wizard, the wizard regenerates the deleted table.</span></span> <span data-ttu-id="94cbc-163">重新生成已删除的表或列时，向导不会发出警告。</span><span class="sxs-lookup"><span data-stu-id="94cbc-163">The wizard provides no warning that the deleted table or column will be regenerated.</span></span>  
  
 <span data-ttu-id="94cbc-164">更改由架构生成向导生成的表或列的属性。</span><span class="sxs-lookup"><span data-stu-id="94cbc-164">Changing the properties of a table or column generated by the Schema Generation Wizard.</span></span>  
 <span data-ttu-id="94cbc-165">如果修改由架构生成向导生成的表或列的属性，则该向导不会对表进行更改，而直接重新生成更改后的表。</span><span class="sxs-lookup"><span data-stu-id="94cbc-165">If you modify the properties of a table or a column generated by the Schema Generation Wizard, the wizard regenerates the changed table without the change.</span></span> <span data-ttu-id="94cbc-166">例如，如果更改由架构生成向导生成的列的数据类型或为空性，或者更改该向导生成的表的文件组，则在重新生成后不会保留这些更改。</span><span class="sxs-lookup"><span data-stu-id="94cbc-166">For example, if you change the data type or nullability of a column, or the filegroup of a table generated by the Schema Generation Wizard, the change does not survive the regeneration.</span></span> <span data-ttu-id="94cbc-167">在不对对象进行更改，而直接重新生成更改后的对象时，向导不会发出警告。</span><span class="sxs-lookup"><span data-stu-id="94cbc-167">The wizard provides no warning that the changed object will be regenerated without the change.</span></span>  
  
 <span data-ttu-id="94cbc-168">将列添加到由架构生成向导生成的表中，或者将表添加到主题区域数据库或临时区域数据库中。</span><span class="sxs-lookup"><span data-stu-id="94cbc-168">Adding a column to a table generated by the Schema Generation Wizard or adding a table to the subject area database or staging area database.</span></span>  
 <span data-ttu-id="94cbc-169">如果您将列添加到由架构生成向导生成的表中，则该向导会在重新生成过程保留附加的列以及该列中存储的所有数据。</span><span class="sxs-lookup"><span data-stu-id="94cbc-169">If you add a column to a table generated by the Schema Generation Wizard, the wizard preserves the additional column, along with any data stored in it, during regeneration.</span></span> <span data-ttu-id="94cbc-170">但是，如果您将表添加到主题区域数据库或临时区域数据库中，则架构生成向导不会合并新表。</span><span class="sxs-lookup"><span data-stu-id="94cbc-170">However, if you add a table to the subject area database or the staging area database, the Schema Generation Wizard does not incorporate the new table.</span></span> <span data-ttu-id="94cbc-171">已添加的列或已添加的表不会在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库、DTS 包、数据源视图或者所生成架构中的任何其他位置上得以反映。</span><span class="sxs-lookup"><span data-stu-id="94cbc-171">The added column, or the added table, is not reflected in the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] project, the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database, the DTS packages, the data source view, or any other place in the schema that is generated.</span></span>  
  
## <a name="supporting-data-source-and-data-source-view-changes"></a><span data-ttu-id="94cbc-172">支持数据源和数据源视图更改</span><span class="sxs-lookup"><span data-stu-id="94cbc-172">Supporting Data Source and Data Source View Changes</span></span>  
 <span data-ttu-id="94cbc-173">在重新运行架构生成向导时，它重用初始生成使用的相同数据源和数据源视图。</span><span class="sxs-lookup"><span data-stu-id="94cbc-173">When the Schema Generation Wizard is rerun, it reuses the same data source and data source view that it used for the original generation.</span></span> <span data-ttu-id="94cbc-174">如果您添加数据源或数据源视图，则向导不会使用该数据源或数据源视图。</span><span class="sxs-lookup"><span data-stu-id="94cbc-174">If you add a data source or a data source view, the wizard does not use it.</span></span> <span data-ttu-id="94cbc-175">如果您在初始生成后删除原始数据源或数据源视图，则必须从头运行向导。</span><span class="sxs-lookup"><span data-stu-id="94cbc-175">If you delete the original data source or data source view after the initial generation, you must run the wizard from the beginning.</span></span> <span data-ttu-id="94cbc-176">向导中的所有先前设置也会被删除。</span><span class="sxs-lookup"><span data-stu-id="94cbc-176">All previous settings in the wizard are also deleted.</span></span> <span data-ttu-id="94cbc-177">下次运行架构生成向导时，基础数据库中任何绑定到已删除数据源或数据源视图的现有对象都被视为用户创建的对象。</span><span class="sxs-lookup"><span data-stu-id="94cbc-177">Any existing objects in an underlying database that were bound to a deleted data source or data source view are treated as user-created objects the next time you run the Schema Generation Wizard.</span></span>  
  
 <span data-ttu-id="94cbc-178">如果数据源视图并未反映基础数据库生成时的实际状态，则架构生成向导在生成主题区域数据库架构或临时区域数据库架构时可能会遇到错误。</span><span class="sxs-lookup"><span data-stu-id="94cbc-178">If the data source view does not reflect the actual state of the underlying database at the time of generation, the Schema Generation Wizard may encounter errors when it generates the schemas for the subject area database and the staging area database.</span></span> <span data-ttu-id="94cbc-179">例如，如果数据源视图指定将列的数据类型设置为 `int`，但该列的数据类型实际设置为 `string`，则架构生成向导会将外键的数据类型设置为 `int` 以便与数据源视图相匹配，而在创建关系时会失败，因为实际的数据类型为 `string`。</span><span class="sxs-lookup"><span data-stu-id="94cbc-179">For example, if the data source view specifies that the data type for a column is set to `int`, but the data type for the column is actually set to `string`, the Schema Generation Wizard sets the data type for the foreign key to `int` to match the data source view and then fails when it creates the relationship because the actual data type is `string`.</span></span>  
  
 <span data-ttu-id="94cbc-180">另一方面，如果您将数据源连接字符串更改为先前生成的其他数据库，则不会生成任何错误。</span><span class="sxs-lookup"><span data-stu-id="94cbc-180">On the other hand, if you change the data source connection string to a different database from the previous generation, no error is generated.</span></span> <span data-ttu-id="94cbc-181">将会使用新的数据库，并且不会对先前数据库进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="94cbc-181">The new database is used, and no change is made to the previous database.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="94cbc-182">另请参阅</span><span class="sxs-lookup"><span data-stu-id="94cbc-182">See Also</span></span>  
 <span data-ttu-id="94cbc-183">[管理对数据源视图和数据源所做的更改](manage-changes-to-data-source-views-and-data-sources.md) </span><span class="sxs-lookup"><span data-stu-id="94cbc-183">[Manage Changes to Data Source Views and Data Sources](manage-changes-to-data-source-views-and-data-sources.md) </span></span>  
 [<span data-ttu-id="94cbc-184">架构生成向导 (Analysis Services)</span><span class="sxs-lookup"><span data-stu-id="94cbc-184">Schema Generation Wizard &#40;Analysis Services&#41;</span></span>](schema-generation-wizard-analysis-services.md)  
  
  