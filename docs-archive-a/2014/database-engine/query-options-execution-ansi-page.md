---
title: 查詢選項執行 (ANSI 頁面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.ansi.f1
ms.assetid: c90d7cdf-3309-46f4-b900-220521bb9552
author: rothja
ms.author: jroth
ms.openlocfilehash: 013a7a318ed7f8db9156700f789ae64cf3e4e017
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87704370"
---
# <a name="query-options-execution-ansi-page"></a>查詢選項執行 (ANSI 頁面)
  使用此頁面來指定 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將使用 ISO (ANSI) standard 中指定的全部或部分設定來執行查詢。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **SET ANSI_DEFAULTS**  
 選取所有的預設 ANSI 設定。 依預設，此方塊無法使用，因為只設定了某些 ISO 設定。  
  
 **SET QUOTED_IDENTIFIER**  
 用引號來圍住物件識別碼。 預設會選取這個選項。  
  
 **SET ANSI_NULL_DFLT_ON**  
 針對在 CREATE TABLE 或 ALTER TABLE 陳述式期間未明確定義為 NOTNULL 的所有使用者自訂的資料類型或資料行，允許 Null 值 (預設的狀態)。 預設會選取這個選項。  
  
 **SET IMPLICIT_TRANSACTIONS**  
 依預設，不會選取這個選項。  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 在認可交易之後，會自動關閉任何開啟的資料指標 (符合 ISO)。 在清除之後 (設定為 OFF)，資料指標會在交易界限之間保持開啟，只有在關閉連接或明確關閉資料指標時才會關閉。 依預設，不會選取這個選項。  
  
 **SET ANSI_PADDING**  
 控制資料行用來儲存值的方式，比資料行的定義大小還短，以及資料行儲存**char**、 **Varchar**、 **binary**和**Varbinary**資料尾端空白之值的方式。 這項設定只會影響新資料行的定義。 建立好資料行之後， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會根據建立資料行之時的設定來儲存值。 這項設定後來的變更並不會影響現有的資料行。 依預設，這個核取方塊為已選取。  
  
 **SET ANSI_WARNINGS**  
 指定數個錯誤狀況的 ISO 標準行為：  
  
-   如果選取此核取方塊，而 Null 值出現在彙總函式 (例如，SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP 或 COUNT) 中，就會產生警告訊息。 當**關閉**時，不會發出任何警告。  
  
-   在清除了這個核取方塊之後，除以零及算術溢位錯誤，都會造成陳述式的復原並產生錯誤訊息。 設定為 OFF 時，除以零及算術溢位錯誤會造成傳回 Null 值。 如果在 character、Unicode 或 binary 資料行中嘗試 INSERT 或 UPDATE 作業，且新值長度超過資料行的大小上限時，除以零或算術溢位錯誤會造成傳回 Null 值。 如果**SET ANSI_WARNINGS**是 ON，則會依 ISO 標準的指定取消插入或更新作業。 字元資料行尾端的空格會被忽略，二進位資料行尾端的 Null 也會被忽略。 當它是 OFF 時，便會將資料截斷成為資料行大小，陳述式會繼續作業。  
  
 預設會選取這個選項。  
  
 **SET ANSI_NULLS**  
 指定搭配 null 值一起使用時，等於 (`=`) 和不等於 (`<>`) 比較運算子的 ISO 相容行為。 如果選取 **SET ANSI_NULLS** ，所有針對 Null 值的比較，都會評估為 UNKNOWN，也就是符合 ISO 的行為。 如果未選取 **SET ANSI_NULLS** ，且如果資料值為 NULL，則所有資料針對 Null 值比較，都會評估為 TRUE。 預設會選取這個選項。  
  
 **重設為預設值**  
 將此頁面上的所有值重設為原始預設值。  
  
  
