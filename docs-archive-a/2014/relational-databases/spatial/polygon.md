---
title: Polygon | Microsoft Docs
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 040bb8a2558cc57b1b99a3ce984bec3c8925bc0d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590656"
---
# <a name="polygon"></a>Polygon
  `Polygon`是存储为一系列点的二维表面，这些点定义一个外部边界环和零个或多个内部环。

## <a name="polygon-instances"></a>Polygon 实例
 可以从至少具有三个不同点的环中构建一个 `Polygon` 实例。 `Polygon` 实例也可以为空。

 `Polygon` 的外部环和任意内部环定义了其边界。 环内部的空间定义了 `Polygon` 的内部。

 下图显示了 `Polygon` 实例的示例。

 ![几何 Polygon 实例的示例](../../database-engine/media/polygon.gif "几何 Polygon 实例的示例")

 如图中所示：

1.  图 1 是由外部环定义其边界的 `Polygon` 实例。

2.  图 2 是由外部环和两个内部环定义其边界的 `Polygon` 实例。 内部环内的面积是 `Polygon` 实例的外部环的一部分。

3.  图 3 是一个有效的 `Polygon` 实例，因为其内部环在单个切点处相交。

### <a name="accepted-instances"></a>接受的实例
 已接受的 `Polygon` 实例是可以在不引发异常的情况下存储到 `geometry` 或 `geography` 变量中的实例。 下面是一些已接受的 `Polygon` 实例：

-   空的 `Polygon` 实例

-   具有一个可接受的外部环和零个或多个可接受的内部环的 `Polygon` 实例

 要使环可接受，需要满足以下条件。

-   `LineString` 实例必须是已接受的实例。

-   `LineString` 实例至少必须有四个点。

-   `LineString` 实例的起始点和结束点必须相同。

 下面的示例显示接受的 `Polygon` 实例。

```
DECLARE @g1 geometry = 'POLYGON EMPTY';
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';
```

 `@g4` 和 `@g5` 显示接受的 `Polygon` 实例可能不是有效的 `Polygon` 实例。 `@g5` 还显示 Polygon 实例只需包含一个具有任意四个点的环便可以被接受。

 下面的示例引发 `System.FormatException`，因为 `Polygon` 实例未被接受。

```
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';
```

 `@g1` 未被接受，因为外部环的 `LineString` 实例不包含足够的点。 `@g2` 未被接受，因为外部环 `LineString` 实例的起始点与结束点不同。 下面的示例有一个可接受的外部环，但内部环不可接受。 这也会引发 `System.FormatException`。

```
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';
```

### <a name="valid-instances"></a>有效实例
 `Polygon` 的内部环在单个切点处既可与自身接触也可彼此接触，但如果 `Polygon` 的内部环交叉，则该实例无效。

 下面的示例显示有效的 `Polygon` 实例。

```
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();
```

 `@g3` 有效，因为两个内部环在一个点相切并且没有相互交叉。 下面的示例显示无效的 `Polygon` 实例。

```
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();
```

 `@g1` 无效，因为内部环在两个位置接触外部环。 `@g2` 无效，因为第二个内部环位于第一个内部环的内部。 `@g3` 无效，因为两个内部环在多个连续点接触。 `@g4` 无效，因为两个内部环的内部重叠。 `@g5` 无效，因为外部环不是第一个环形。 `@g6` 无效，因为环未至少具有三个不同的点。

## <a name="examples"></a>示例
 下面的示例创建了一个带有孔和 SRID 为 10 的简单 `geometry``Polygon` 实例。

```
DECLARE @g geometry;
SET @g = geometry::STPolyFromText('POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))', 10);
```

 可能输入无效的实例并转换为有效的 `geometry` 实例。 在下列 `Polygon`示例中，内部环和外部环重叠且该实例无效。

```
DECLARE @g geometry;
SET @g = geometry::Parse('POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))');
```

 在下面的示例中，无效实例通过 `MakeValid()`成为有效实例。

```
SET @g = @g.MakeValid();
SELECT @g.ToString();
```

 以上示例中返回的 `geometry` 实例为 `MultiPolygon`。

```
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)), ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))
```

 下面是另一个演示将无效实例转换为有效的几何图形实例的示例。 在下面的示例中，已经使用完全相同的三个点创建了 `Polygon` 实例：

```sql
DECLARE @g geometry
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');
SET @g = @g.MakeValid();
SELECT @g.ToString()
```

 上面返回的几何图形实例是 `Point(1 3)`。  如果给出的 `Polygon` 是 `POLYGON((1 3, 1 5, 1 3, 1 3))` ，则 `MakeValid()` 将返回 `LINESTRING(1 3, 1 5)`。

## <a name="see-also"></a>另请参阅
 [STArea &#40;Geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type) [STExteriorRing &#40;geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type) [STNumInteriorRing &#40;geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type) [STInteriorRingN &#40;Geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type) [STCentroid &#40;geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type) [STPointOnSurface &#40;geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type) [MultiPolygon](../spatial/polygon.md) [空间数据 &#40;SQL Server](../spatial/spatial-data-sql-server.md)&#41;[STIsValid &#40;geography 数据类型&#41;](/sql/t-sql/spatial-geography/stisvalid-geography-data-type) [STIsValid &#40;geometry 数据类型&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)


