---
title: 複寫資料分割資料表及索引 | Microsoft Docs
ms.custom: ''
ms.date: 09/10/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- partitioned indexes [SQL Server], replicating
- partitioned tables [SQL Server], replicating
- replication [SQL Server], partitioned tables
- publishing [SQL Server replication], partitioned tables
- transactional replication, partitioned tables
ms.assetid: c9fa81b1-6c81-4c11-927b-fab16301a8f5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 616707bfb11b48b170fc8f0e8872076d2cd09d1c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592600"
---
# <a name="replicate-partitioned-tables-and-indexes"></a>複寫資料分割資料表及索引
  分割大型資料表或索引將更易於管理，因為分割可讓您快速並有效率地管理及存取資料子集，同時又可維護資料收集的完整性。 如需詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md)＞。 複寫可支援資料分割，其方式是提供一組屬性來指定應該如何處理資料分割資料表和索引。  
  
## <a name="article-properties-for-transactional-and-merge-replication"></a>交易式和合併式複寫的發行項屬性  
 下表列出用來分割資料的物件。  
  
|Object|建立的方法|  
|------------|----------------------|  
|資料分割資料表或索引|CREATE TABLE 或 CREATE INDEX|  
|分割區函數|CREATE PARTITION FUNCTION|  
|分割區配置|CREATE PARTITION SCHEME|  
  
 與資料分割有關的第一組屬性是發行項結構描述選項，這些選項可決定是否應將資料分割物件複製到訂閱者。 可透過下列方式來設定這些結構描述選項：  
  
-   在新增發行集精靈的 **[發行項屬性]** 頁面中，或是在 [發行集屬性] 對話方塊中。 若要複製上表所列的物件，請 `true` 針對 [**複製資料表資料分割**配置] 和 [**複製索引資料分割**配置] 屬性指定的值。 如需如何存取 [發行項屬性]  頁面的詳細資訊，請參閱[檢視和修改發行集屬性](view-and-modify-publication-properties.md)。  
  
-   藉由使用下列其中一個預存程序的 *schema_option* 參數：  
  
    -   用於異動複寫的[sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 或 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) f或 transactional replication  
  
    -   用於合併式複寫的[sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 或 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) f或 merge replication  
  
     若要複製上表所列的物件，請指定適當的結構描述選項值。 如需有關如何指定結構描述選項的詳細資訊，請參閱＜ [Specify Schema Options](specify-schema-options.md)＞。  
  
 複寫會在初始同步處理期間將物件複製到訂閱者。 如果資料分割配置使用 PRIMARY 以外的檔案群組，這些檔案群組必須在初始同步處理之前存在於訂閱者上。  
  
 在初始化訂閱者之後，資料變更會傳播到訂閱者，並套用到適當的資料分割。 但是，不支援資料分割配置的變更。 交易式及合併複寫無法複寫下列命令：ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME 或 ALTER INDEX 的 REBUILD WITH PARTITION 陳述式。  這些命令所關聯的變更不會自動複寫到訂閱者。 使用者必須在訂閱者中手動進行類似的變更。  
  
## <a name="replication-support-for-partition-switching"></a>資料分割切換的複寫支援  
 資料表資料分割的其中一個重要優點，就是能夠快速及有效率地在資料分割之間移動資料子集。 資料的移動是利用 SWITCH PARTITION 命令。 根據預設，當啟用資料表進行複寫時，會基於以下理由而封鎖 SWITCH PARTITION 作業：  
  
-   如果資料移入或移出存在於發行者上但不存在於訂閱者上的資料表，則發行者和訂閱者彼此可能會不一致。 當資料移入或移出臨時資料表時，通常會發生這個問題。  
  
-   如果訂閱者對於資料分割資料表的定義與發行者不同，則當散發代理程式嘗試在訂閱者上套用變更時，將會失敗。  
  
 雖然有這些潛在的問題，還是可以啟用資料分割切換來進行異動複寫。 在您啟用資料分割切換之前，請確定與資料分割切換有關的所有資料表都存在於發行者和訂閱者上，並確定資料表定義和資料分割定義是相同的。  
  
 當資料分割在發行者端和訂閱者端擁有完全相同的資料分割配置時，您可以開啟僅將資料分割切換陳述式複寫至訂閱者的 *allow_partition_switch* 和 *replication_partition_switch* 。 您也可以在不複寫 DDL 的情況下，開啟 *allow_partition_switch* 。 當您想要將舊的月份傳出資料分割，但針對其他年份，則將複寫的資料分割保留在原位以便在訂閱者端進行備份時，這非常實用。  
  
 若您透過目前的版本啟用了 SQL Server 2008 R2 的資料分割切換功能，您可能很快就會需要執行分割及合併作業。 對複寫的資料表執行分割或合併作業之前，請確定有問題的分割區上沒有任何暫止的複寫命令。 此外也必須確定未在分割及合併作業期間，對分割區執行任何 DML 作業。 如有交易的記錄讀取器未處理，或在執行分割或合併作業時，對複寫資料表的資料分割執行了 DML 作業 (對象均為同一個資料分割)，可能會導致記錄讀取器代理程式發生處理錯誤。 若要更正此錯誤，可能需要重新初始化訂閱。  
  
> [!WARNING]  
>  由於用來偵測並解決衝突之隱藏資料行的緣故，您不得為點對點發行集啟用資料分割切換。  
  
### <a name="enabling-partition-switching"></a>啟用資料分割切換  
 交易式發行集的下列屬性可讓使用者控制複寫環境中的資料分割切換行為：  
  
-   ** \@ allow_partition_switch**，當設定為時 `true` ，switch partition 可以針對發行集資料庫來執行。  
  
-   ** \@ replicate_partition_switch**決定是否應將 switch partition DDL 語句複寫至訂閱者。 只有當** \@ allow_partition_switch**設定為時，這個選項才有效 `true` 。  
  
 您可以在建立發行集時使用 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 來設定這些屬性，或是在建立發行集之後使用 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) 來設定。 如前所述，合併式複寫不支援資料分割切換。 若要在已啟用合併式複寫的資料表上執行 SWITCH PARTITION，請從發行集中移除此資料表。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](publish-data-and-database-objects.md)  
  
  
