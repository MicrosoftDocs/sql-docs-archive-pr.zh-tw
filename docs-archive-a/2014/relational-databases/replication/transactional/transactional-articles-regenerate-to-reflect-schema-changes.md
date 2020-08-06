---
title: 重新產生自訂交易程序以反映結構描述變更 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom procedures [SQL Server replication]
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b41b5309816e037ce3619e880b796e0653c7506
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706369"
---
# <a name="regenerate-custom-transactional-procedures-to-reflect-schema-changes"></a>重新產生自訂交易程序以反映結構描述變更
  依預設，異動複寫可透過預存程序在「訂閱者」上進行所有資料變更，該預存程序由發行集中每個資料表發行項的內部程序所產生。 將插入、更新或刪除複寫至「訂閱者」時，會將三個程序 (插入、更新和刪除各一個) 複製給「訂閱者」並執行。 在對「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者」上的資料表進行結構描述變更時，複寫將透過呼叫相同的內部指令碼程序組以自動重新產生這些程序，以便新程序與新的結構描述相符 (「Oracle 發行者」不支援結構描述變更複寫)。  
  
 也可以將自訂程序指定為取代一個或多個預設程序。 如果結構描述變更影響程序，則應變更自訂程序。 例如，如果程序參考在結構描述變更中卸除的資料行，則應從程序中移除資料行參考。 複寫可透過兩種方式將新的自訂程序傳播給「訂閱者」：  
  
-   第一種方式是使用自訂指令碼程序以取代複寫所使用的預設值：  
  
    1.  [&#40;transact-sql&#41;執行 sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)時，請確定 **@schema_option** 0x02 位為**true**。  
  
    2.  執行[sp_register_custom_scripting &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql) ，並為參數指定 ' insert '、' update ' 或 ' delete ' 的值， **@type** 並為參數指定自訂腳本程式的名稱 **@value** 。  
  
     在下次變更結構描述時，複寫將呼叫此預存程序以為新使用者自訂預存程序的定義編寫指令碼，然後將此程序傳播給每個「訂閱者」。  
  
-   第二個選項是使用包含新自訂程序定義的指令碼：  
  
    1.  [&#40;transact-sql&#41;執行 sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)時，請將 **@schema_option** 0x02 位設定為**false** ，如此複寫就不會在「訂閱者」端自動產生自訂程式。  
  
    2.  在變更每個結構描述之前，會建立新的指令碼檔案並透過執行 [sp_register_custom_scripting &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql) 使用複寫註冊指令碼。 為參數指定 ' custom_script ' 的值 **@type** ，並為參數指定發行者的腳本路徑 **@value** 。  
  
     在下次變更相關結構描述時，此指令碼在相同交易中於每個「訂閱者」上做為 DDL 命令執行。 在變更結構描述後，指令碼將取消註冊。 您必須重新註冊指令碼，以便在隨後變更結構描述後執行該指令碼。  
  
## <a name="see-also"></a>另請參閱  
 [指定交易式發行項變更的傳播方式](transactional-articles-specify-how-changes-are-propagated.md)   
 [對發行集資料庫進行結構描述變更](../publish/make-schema-changes-on-publication-databases.md)  
  
  
