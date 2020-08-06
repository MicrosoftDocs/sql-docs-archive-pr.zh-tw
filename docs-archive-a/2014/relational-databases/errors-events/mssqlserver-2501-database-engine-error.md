---
title: MSSQLSERVER_2501 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 200997dcfe7bf8a5933b9fce492daabd5baffd04
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702930"
---
# <a name="mssqlserver_2501"></a>MSSQLSERVER_2501
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2501|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_NO_SUCH_TABLE_NAME|  
|訊息文字|找不到名為 'NAME' 的資料表或物件。 請檢查系統目錄。|  
  
## <a name="explanation"></a>說明  
 找不到指定的物件。  
  
### <a name="possible-causes"></a>可能的原因  
 這項錯誤可能是由於下列其中一個問題所造成：  
  
-   未正確地指定物件。  
  
-   物件不存在，或是在陳述式嘗試使用之前已經卸除物件。  
  
-   物件可能存在，但是無法向使用者顯示物件。 例如，使用者可能沒有物件的權限，或是物件是使用者看不到的內部資料表。  
  
## <a name="user-action"></a>使用者動作  
  
-   確認目前的資料庫內容是否正確。 如需詳細資訊，請參閱 [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)。  
  
-   確認資料表或物件名稱拚字是否正確。  
  
-   驗證包含物件的結構描述名稱。 如果物件所屬的結構描述不是預設的結構描述 (**dbo**)，您就必須使用 *schema_name.object_name* 的兩部分格式來指定資料表或物件名稱。  
  
-   確認物件是否存在系統資料表中。 若要確認資料表或其他結構描述範圍物件是否存在，請查詢 [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql) 目錄檢視。 如果物件不在系統資料表中，表示物件已經刪除，或是使用者沒有檢視物件中繼資料的權限。 如需如何檢視物件中繼資料的詳細資訊，請參閱[中繼資料可見性組態](../security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
  
