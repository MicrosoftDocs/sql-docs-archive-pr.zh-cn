---
title: 空间数据类型概述 | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c0548d974e83bfe2b1e103d4458b17078fba8014
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691148"
---
# <a name="spatial-data-types-overview"></a>空间数据类型概述
  有两种类型的空间数据。  数据类型支持平面或欧几里得（平面球）数据。 `geometry` 数据类型符合开放地理空间联盟 (OGC) 的 SQL 简单特征规范 1.1.0 版 并符合 SQL MM（ISO 标准）。

 另外，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持 `geography` 数据类型，该数据类型可存储诸如 GPS 纬度和经度坐标之类的椭圆体（圆球）数据。

> [!IMPORTANT]
>  有关 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引入的空间功能的详细说明和示例（包括对空间数据类型的改进），请下载白皮书 [SQL Server Code-Named "Denali" 中的新空间功能](https://go.microsoft.com/fwlink/?LinkId=226407)。

##  <a name="spatial-data-objects"></a><a name="objects"></a> 空间数据对象
 `geometry` 和 `geography` 数据类型支持十六种空间数据对象或实例类型。 但是，这些实例类型中只有十一种  “可实例化”；可以在数据库中创建并使用这些实例（或可对其进行实例化）。 这些实例从其父数据类型派生某些属性，这些属性将它们作为 `Points` 、 **linestring、circularstring**、 `CompoundCurves` 、 `Polygons` `CurvePolygons` 或作为中的多个 `geometry` 或 `geography` 实例 `GeometryCollection` 加以区分。  类型具有附加实例类型 。

 下图描述了 `geometry` 和 `geometry` 数据类型所基于的 `geography` 层次结构。 和的可实例化类型 `geometry` `geography` 以蓝色表示。

 ![几何类型的层次结构](../../database-engine/media/geom-hierarchy.gif "几何类型的层次结构")

 如图所示， `geometry` 和数据类型的十种可实例化类型 `geography` 为 `Point` 、、、、、、、、 `MultiPoint` `LineString` `CircularString` `MultiLineString` `CompoundCurve` `Polygon` `CurvePolygon` `MultiPolygon` 和 `GeometryCollection` 。 geography 数据类型有一个附加可实例化类型：`FullGlobe`。 `geometry`和 `geography` 类型可以识别特定的实例，只要它是格式正确的实例，即使未显式定义该实例也是如此。 例如，如果 `Point` 使用 ( STPointFromText 显式定义了一个实例，则 `geometry` `geography` `Point` 只要方法输入的格式正确，就会将该实例识别为。 如果您使用 `STGeomFromText()` 方法定义了相同的实例，则 `geometry` 和 `geography` 数据类型都将该实例识别为 `Point`。

 geometry 和 geography 类型的子类型分为简单类型和集合类型。  类似 `STNumCurves()` 的一些方法仅适用于简单类型。

 简单类型包括：

-   [Point](../spatial/point.md)

-   [LineString](../spatial/linestring.md)

-   [CircularString](../spatial/circularstring.md)

-   [CompoundCurve](../spatial/compoundcurve.md)

-   [多边形](../spatial/polygon.md)

-   [CurvePolygon](../spatial/curvepolygon.md)

 集合类型包括：

-   [MultiPoint](../spatial/multipoint.md)

-   [MultiLineString](../spatial/multilinestring.md)

-   [MultiPolygon](../spatial/multipolygon.md)

-   [GeometryCollection](../spatial/geometrycollection.md)


##  <a name="differences-between-the-geometry-and-geography-data-types"></a><a name="differences"></a> GEOMETRY 和 GEOGRAPHY 数据类型之间的差异
 两种空间数据类型的行为经常非常相似，但在数据存储方式和操作方式上存在某些重要的差别。

### <a name="how-connecting-edges-are-defined"></a>如何定义连接边
 用于 `LineString` 和 `Polygon` 类型的定义数据仅限顶点。  geometry 类型中两个顶点之间的连接边是直线。  但是，geography 类型中两个顶点之间的连接边是两个顶点之间的短的大椭圆弧。  大椭圆是具有穿过其中心的投影的椭圆体的相交部分，大椭圆弧是大椭圆上的弧形线段。

### <a name="how-circular-arc-segments-are-defined"></a>如何定义圆弧线段
 在 XY 笛卡尔坐标平面上定义 geometry 类型的圆弧线段（Z 值被忽略）。 geography 类型的圆弧线段由参考球上的曲线段定义。 参考球上的任何平行面可以由两个互补圆弧（两个弧的点有一个恒定的纬度角）定义。

### <a name="measurements-in-spatial-data-types"></a>空间数据类型中的度量
 在平面（或平面球）系统中，均以相同的度量单位为坐标测量距离和面积。 如果使用 `geometry` 数据类型，(2, 2) 和 (5, 6) 之间的距离为 5 个单位，与所用的单位无关。

 在椭圆体（或圆球）系统中，坐标以经度和纬度的度数给定。 但是，即使测量可能依据的是 `geography` 实例的空间引用标识符 (SRID)，长度和面积的测量单位也通常为米或平方米。  数据类型最常见的度量单位为米。

### <a name="orientation-of-spatial-data"></a>空间数据的方向
 在平面系统中，多边形的环方向并非重要因素。 例如，((0, 0), (10, 0), (0, 20), (0, 0)) 描述的多边形与 ((0, 0), (0, 20), (10, 0), (0, 0)) 描述的多边形相同。 SQL 规范的 OGC 简单特征未规定环顺序，并且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会强制环的顺序。

 在椭圆体系统中，多边形无意义，或者模糊不清，没有方向。 例如，赤道周围的环是否描述了北半球或南半球？ 如果我们使用 `geography` 数据类型存储空间实例，必须指定环的方向并准确地描述实例的位置。 椭圆体系统中多边形的内部由左侧规则定义。

 如果兼容级别为100或更低， [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 则 `geography` 数据类型具有以下限制：

-   每个 `geography` 实例必须能够容纳在单个半球的内部。 任何大于半球的对象都无法存储。

-   使用开放地理空间联盟 (OGC) 熟知文本 (Well-Known Text, WKT) 或熟知二进制 (Well-Known Binary, WKB) 表示形式并且会产生大于一个半球的对象的任何 `geography` 实例都会引发一个 `ArgumentException` 异常。

-   `geography`需要输入两个实例的数据类型方法（ `geography` 如 STIntersection ( # A1、STUnion ( # A3、STDifference ( # A5 和 STSymDifference ( # A7）将返回 null （如果这些方法的结果不能容纳在单个半球内）。 如果输出超过单个半球，STBuffer() 也将返回 Null。

 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中，`FullGlobe` 是一种特殊类型的多边形，涵盖了整个球体。 `FullGlobe` 有面积，但是没有边框或顶点。

### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>在 geography 数据类型中外环和内环并不重要
 SQL 规范的 OGC 简单功能讨论了外环和内环，但此差别对数据类型来说几乎毫无意义 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `geography` ; 多边形的任何环都可以作为外环。

 有关 OGC 规范的详细信息，请参阅以下内容：

-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture（OGC 规范：简单特征访问第 1 部分 - 公共体系结构）](https://go.microsoft.com/fwlink/?LinkId=93627)

-   [OGC Specifications, Simple Feature Access Part 2 - SQL Options（OGC 规范：简单特征访问第 2 部分 - SQL 选项）](https://go.microsoft.com/fwlink/?LinkId=93628)


##  <a name="circular-arc-segments"></a><a name="circular"></a> 圆弧线段
 三种可实例化类型可以采用圆弧线段：`CircularString`、`CompoundCurve` 和 `CurvePolygon`。  圆弧线段在二维平面中由三个点定义；第三个点不能与第一个点相同。

 图 A 和 B 显示典型的圆弧线段。 请注意这三个点如何落在圆周上。

 图 C 和 D 显示直线线段如何定义为圆弧线段。  请注意仍需要三个点定义圆弧线段，不像普通直线线段只需要两个点来定义。

 针对圆弧线段类型的方法使用直线线段来近似圆弧。用于近似圆弧的直线线段数量将取决于弧的长度和曲率。可以为每个圆弧线段类型存储 Z 值；但是，方法将不在计算中使用 Z 值。

> [!NOTE]
>  如果为圆弧线段指定 Z 值，则这些值对于圆弧线段中的所有点必须相同，才接受输入。 例如，接受 `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` ，但是不接受 `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` 。

### <a name="linestring-and-circularstring-comparison"></a>LineString 和 CircularString 的比较
 下图显示相同的等腰三角形（三角形 A 使用直线线段定义，三角形 B 使用圆弧线段定义）：

 ![](../../database-engine/media/7e382f76-59da-4b62-80dc-caf93e637c14.png "7e382f76-59da-4b62-80dc-caf93e637c14")

 此示例显示如何使用 `LineString` 实例和 `CircularString` 实例存储上述等腰三角形：

```sql
DECLARE @g1 geometry;
DECLARE @g2 geometry;
SET @g1 = geometry::STGeomFromText('LINESTRING(1 1, 5 1, 3 5, 1 1)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(1 1, 3 1, 5 1, 4 3, 3 5, 2 3, 1 1)', 0);
IF @g1.STIsValid() = 1 AND @g2.STIsValid() = 1
  BEGIN
      SELECT @g1.ToString(), @g2.ToString()
      SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length]
  END
```

 请注意，`CircularString` 实例需要七个点来定义三角形，但是 `LineString` 实例只需要四个点定义三角形。 原因是 `CircularString` 实例存储的是圆弧线段而非直线线段。 因此，存储在 `CircularString` 实例中的三角形边是 ABC、CDE 和 EFA，而存储在 `LineString` 实例中的三角形边是 AC、CE 和 EA。

 请思考以下代码片段：

```sql
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];
```

 此代码段将生成以下结果：

```
LS LengthCS Length
5.65685...6.28318...
```

 下图显示了如何将每种类型存储 (红线显示 `LineString``@g1` ，蓝线显示 `CircularString``@g2`) ：

 ![](../../database-engine/media/e52157b5-5160-4a4b-8560-50cdcf905b76.png "e52157b5-5160-4a4b-8560-50cdcf905b76")

 如上图所示，`CircularString` 实例与 `LineString` 实例相比，使用更少的点来存储曲线边界，而且更精确。 `CircularString` 实例对于存储圆边界（如针对特定点的二十英里搜索半径）很有用。 `LineString` 实例则适合存储线性边界（如方形城市街区）。

### <a name="linestring-and-compoundcurve-comparison"></a>LineString 和 CompoundCurve 的比较
 以下代码示例显示如何使用 `LineString` 和 `CompoundCurve` 实例存储相同的图形：

```sql
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');
```

 或

 在上述示例中，`LineString` 实例或 `CompoundCurve` 实例都可以存储该图形。  下一个示例使用 `CompoundCurve` 存储饼图切片：

```sql
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');
```

  实例可以直接存储圆弧线段 (2 2, 1 3, 0 2)，而  实例则必须将曲线转换为几个更小的直线线段。

### <a name="circularstring-and-compoundcurve-comparison"></a>CircularString 和 CompoundCurve 的比较
 以下代码示例显示如何将饼图切片存储在 `CircularString` 实例中：

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');
SELECT @g.ToString(), @g.STLength();
```

 要使用 `CircularString` 实例存储饼图切片，要求每个直线线段使用三个点。  如果一个中间点未知，必须计算它或必须将直线线段的端点加倍，如以下代码段所示：

```sql
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');
```

 `CompoundCurve` 实例允许 `LineString` 和  `CircularString` 组件，因此只需要知道饼图切片的直线线段的两个点。  此代码示例显示如何使用 `CompoundCurve` 存储相同的图形：

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');
SELECT @g.ToString(), @g.STLength();
```

### <a name="polygon-and-curvepolygon-comparison"></a>Polygon 和 CurvePolygon 的比较
 在定义外部环和内部环时，`CurvePolygon` 实例可以使用 `CircularString` 和 `CompoundCurve` 实例。  `Polygon` 实例不能使用圆弧线段类型：`CircularString` 和 `CompoundCurve`。


## <a name="see-also"></a>另请参阅
 [空间数据 &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md) [Geometry 数据类型方法引用](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql) [geography 数据类型方法引用](/sql/t-sql/spatial-geography/spatial-types-geography) [STNumCurves &#40;Geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stnumcurves-geometry-data-type) [STNumCurves &#40;geography 数据](/sql/t-sql/spatial-geography/stnumcurves-geography-data-type)类型&#41;[STGeomFromText &#40;geometry](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)数据类型&#41;[STGeomFromText &#40;geography 数据类型&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)


