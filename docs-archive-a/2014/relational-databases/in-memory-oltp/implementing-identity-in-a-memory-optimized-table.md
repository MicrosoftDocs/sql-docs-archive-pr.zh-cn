---
title: 在内存优化表中实现 IDENTITY | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: rothja
ms.author: jroth
ms.openlocfilehash: 955f9f1a905a9d0c71304320f60abe300e430e4f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580754"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>在内存优化的表中实现 IDENTITY
  内存优化表支持 IDENTITY(1, 1)。 但是，内存优化表不支持使用 IDENTITY(x, y)（其中 x != 1 或 y != 1 ）定义的标识列。 标识值的解决方法使用序列对象 ([序列号](../sequence-numbers/sequence-numbers.md)) 。  
  
 从要转换到内存中 OLTP 的表首先删除 IDENTITY 属性。 然后，为表中的列定义新的 SEQUENCE 对象。 作为标识列的 SEQUENCE 对象依赖为列创建 DEFAULT 值的能力，这些列使用 NEXT VALUE FOR 语法获取新的标识值。 因为在内存中 OLTP 中不支持 DEFAULT，您需要将新生成的 SEQUENCE 值传给 INSERT 语句或执行插入的本机编译存储过程。 下面的示例对此模式进行了演示。  
  
```sql  
-- Create a new In-Memory OLTP table to simulate IDENTITY insert  
-- Here the column C1 was the identity column in the original table  
--  
create table T1  
(  
  
[c1] integer not null primary key T1_c1 nonclustered,  
[c2] varchar(32) not null,  
[c3] datetime not null  
  
) with (memory_optimized = on)  
go  
  
-- This is a sequence provider that will give us values for column [c1]  
--  
create sequence usq_SequenceForT1 as integer start with 2 increment by 1  
go  
  
--   insert a sample row using the sequence  
--   note that a new value needs to be retrieved form   
--   the sequence object for every insert  
--  
declare @c1 integer = next value for [dbo].[usq_SequenceForT1]  
insert into T1 values (@c1, 'test', getdate())  
```  
  
 在执行几次插入后，您看到在列 [c1] 中单调增加的有效值。 此结果集是使用不带 `ORDER BY` 的表扫描和哈希索引生成的，因此行未排序。  
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  
