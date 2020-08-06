---
title: OLE DB 自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ee45740af06d0b9d89bcbd8f3e428308c8b43b88
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593484"
---
# <a name="ole-db-custom-properties"></a>OLE DB 自訂屬性
  **來源自訂屬性**  
  
 OLE DB 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 OLE DB 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數|用來存取資料庫的模式。 可能的值為**開啟**資料列集、**來引數的開啟**資料列集， `SQL Command` 以及**來引數的 SQL 命令**。 預設值為 **[開啟資料列集]** 。|  
|AlwaysUseDefaultCodePage|Boolean|一個值，指出要針對每個資料行使用 `DefaultCodePage` 屬性的值，還是嘗試從每個資料行的地區設定中衍生字碼頁。 此屬性的預設值為 `False`。|  
|CommandTimeout|整數|命令逾時之前的秒數。值為 0 表示無限逾時。<br /><br /> 注意:雖然您無法在 [OLE DB 來源編輯器]  中使用這個屬性，但是可以使用 [進階編輯器]  來設定這個屬性。|  
|DefaultCodePage|整數|無法從資料來源中取得字碼頁資訊時要使用的字碼頁。|  
|[OpenRowset]|String|用來開啟資料列集之資料庫物件的名稱。|  
|OpenRowsetVariable|String|變數，其中包含用來開啟資料列集之資料庫物件的名稱。|  
|ParameterMapping|String|從 SQL 命令中的參數到變數的對應。|  
|SqlCommand|String|要執行的 SQL 命令。|  
|SqlCommandVariable|String|變數，其中包含要執行的 SQL 命令。|  
  
 OLE DB 來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [OLE DB Source](ole-db-source.md)。  
  
 **目的地自訂屬性**  
  
 OLE DB 目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 OLE DB 目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
> [!NOTE]  
>  此處所列的 FastLoad 選項 (FastLoadKeepIdentity、FastLoadKeepNulls 和 FastLoadOptions) 會對應至 Microsoft OLE DB Provider for SQL Server (SQLOLEDB) 所實作之 `IRowsetFastLoad` 介面所公開的類似名稱屬性。 如需詳細資訊，請在 MSDN Library 中搜尋 IRowsetFastLoad。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|一個值，指定目的地如何存取其目的地資料庫。<br /><br /> 此屬性可以有下列其中一個值：<br /><br /> `OpenRowset` (0) ：您可以提供資料表或視圖的名稱。<br />`OpenRowset from Variable` (1) ：您可以提供包含資料表或視圖名稱之變數的名稱。<br />`OpenRowset Using Fastload` (3) ：您可以提供資料表或視圖的名稱。<br />`OpenRowset Using Fastload from Variable` (4) ：您可以提供包含資料表或視圖名稱之變數的名稱。<br />`SQL Command` (2) ：您提供 SQL 語句。|  
|AlwaysUseDefaultCodePage|Boolean|一個值，指出要針對每個資料行使用 `DefaultCodePage` 屬性的值，還是嘗試從每個資料行的地區設定中衍生字碼頁。 此屬性的預設值為 `False`。|  
|CommandTimeout|整數|逾時之前 SQL 命令可以執行的秒數上限。值為 0 指出無限的時間。 這個屬性的預設值為 0。<br /><br /> 注意:雖然您無法在 [OLE DB 目的地編輯器]  中使用這個屬性，但是可以使用 [進階編輯器]  來設定這個屬性。|  
|DefaultCodePage|整數|與 OLE DB 目的地相關聯的預設字碼頁。|  
|FastLoadKeepIdentity|Boolean|一個值，指定載入資料時是否要複製識別值。 這個屬性只能搭配其中一個快速載入選項使用。 此屬性的預設值為 `False`。 這個屬性會對應至 OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)屬性 `SSPROP_FASTLOADKEEPIDENTITY` 。|  
|FastLoadKeepNulls|Boolean|一個值，指定載入資料時是否要複製 Null 值。 這個屬性只能搭配其中一個快速載入選項使用。 此屬性的預設值為 `False`。 這個屬性會對應至 OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)屬性 `SSPROP_FASTLOADKEEPNULLS` 。|  
|FastLoadMaxInsertCommitSize|整數|一個值，指定快速載入作業期間，OLE DB 目的地嘗試認可的批次大小。 預設值 **0**表示處理所有資料列之後的單一認可作業。|  
|FastLoadOptions|String|快速載入選項的集合。 快速載入選項包括資料表的鎖定和條件約束的檢查。 您可以指定其中一個選項、兩個選項或不指定任何選項。 這個屬性會對應至 OLE DB 的 IRowsetFastLoad 屬性 `SSPROP_FASTLOADOPTIONS` ，並接受字串選項，例如 `CHECK_CONSTRAINTS` 和 `TABLOCK` 。<br /><br /> 注意:雖然您無法在 [Excel 目的地編輯器]  中使用這個屬性的某些選項，但是可以使用 [進階編輯器]  來設定這些選項。|  
|[OpenRowset]|String|當 AccessMode 為時，就是 `OpenRowset` OLE DB 目的地所存取之資料表或視圖的名稱。|  
|OpenRowsetVariable|String|當 AccessMode 為時，就是 `OpenRowset from Variable` 包含 OLE DB 目的地所存取之資料表或視圖名稱的變數名稱。|  
|SqlCommand|String|當 AccessMode 為時 `SQL Command` ，OLE DB 目的地用來指定資料之目的地資料行的 transact-sql 語句。|  
  
 OLE DB 目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [OLE DB Destination](ole-db-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
