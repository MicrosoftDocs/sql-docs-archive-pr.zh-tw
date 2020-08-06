---
title: 設定一般檔案目的地 (SQL Server 的匯入及匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2af8a1653d9a1aef0828aa112a25825ed23b8bf6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597942"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>設定一般檔案目的地 (SQL Server 匯入和匯出精靈)
  使用 [**設定**一般檔案目的地] 頁面，即可指定目的地一般檔案的格式化選項，並在繼續之前預覽結果。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解用來啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項  
 **來源一般檔案**  
 目的地檔案的名稱。  
  
 **資料列分隔符號**  
 從資料列分隔符號的清單中選取。  
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|資料列是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|資料列是以歸位字元分隔。|  
|**{LF}**|資料列是以換行字元分隔。|  
|**分號 {;}**|資料列是以分號分隔。|  
|**冒號 {:}**|資料列是以冒號分隔。|  
|**逗號 {,}**|資料列是以逗號分隔。|  
|**定位字元 {t}**|資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料列是以分隔號分隔。|  
  
 **資料行分隔符號**  
 從資料行分隔符號的清單中選取。  
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|資料行是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|資料行是以歸位字元分隔。|  
|**{LF}**|資料行是以換行字元分隔。|  
|**分號 {;}**|資料行是以分號分隔。|  
|**冒號 {:}**|資料行是以冒號分隔。|  
|**逗號 {,}**|資料行是以逗號分隔。|  
|**定位字元 {t}**|資料行是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料行是以分隔號分隔。|  
  
 **預覽**  
 在 [**預覽資料**] 對話方塊中，針對目的地一般檔案選取的格式化選項結果。  
  
 **編輯轉換**  
 使用 [資料行對應] 對話方塊，刪除資料列、附加資料列，以及設定目的地檔案**中的資料**行。  
  
  
