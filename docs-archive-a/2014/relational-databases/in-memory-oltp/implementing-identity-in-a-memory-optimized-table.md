---
title: 在記憶體最佳化資料表中實作 IDENTITY | Microsoft Docs
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594562"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>在記憶體最佳化資料表中實作 IDENTITY
  記憶體最佳化資料表支援 IDENTITY(1, 1)。 但是，記憶體最佳化資料表不支援定義為 IDENTITY(x, y) (其中 x != 1 或 y != 1) 的識別欄位。 識別值的因應措施會使用順序物件 ([序號](../sequence-numbers/sequence-numbers.md)) 。  
  
 首先將 IDENTITY 屬性從您要轉換成 In-Memory OLTP 的資料表中移除。 接著在資料表中為資料行定義新的 SEQUENCE 物件。 做為識別資料行的 SEQUENCE 物件需倚賴使用 NEXT VALUE FOR 語法建立資料行之 DEFAULT 值的能力取得新的識別值。 由於 In-Memory OLTP 中不支援 DEFAULT，因此您必須將新產生的 SEQUENCE 值傳遞至 INSERT 陳述式或執行插入作業的原生編譯預存程序。 下列範例示範此模式。  
  
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
  
 執行插入作業數次之後，您會在資料行 [c1] 中看見有效的單純遞增值。 此結果集是使用資料表掃描和沒有 `ORDER BY` 的雜湊索引所產生，因此資料列並未排序。  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
