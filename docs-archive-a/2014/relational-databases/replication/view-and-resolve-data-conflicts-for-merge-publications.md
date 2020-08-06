---
title: 查看和解決合併式發行集的資料衝突 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77aa9ece0073149c017f6eca35a756b22751a74b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594475"
---
# <a name="view-and-resolve-data-conflicts-for-merge-publications-sql-server-management-studio"></a>檢視並解決合併式發行集的資料衝突 (SQL Server Management Studio)
  合併式複寫中的衝突根據為每個發行項指定的解決器進行解決。 依預設，衝突的解決不需要使用者的介入。 但是可以在「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 複寫衝突檢視器」(Replication Conflict Viewer) 中檢視衝突並變更解決的結果。  
  
 複寫衝突檢視器可以在衝突保留期限指定的時間內使用衝突資料 (預設為 14 天)。 若要設定衝突保留期限，可以：  
  
-   為 **@conflict_retention** [Sp_addmergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)的參數指定保留值。  
  
-   為參數指定**conflict_retention**的值 **@property** ，並為 **@value** [sp_changemergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)指定保留值。  
  
 依預設，會儲存衝突資訊：  
  
-   如果發行集相容性層級為 90RTM 或更高，則是在「發行者」與「訂閱者」端。  
  
-   如果發行集相容性層級低於 80RTM，則是在發行者端。  
  
-   如果「訂閱者」執行 [!INCLUDE[ssEW](../../includes/ssew-md.md)]，則會儲存在「發行者」端。 衝突資料無法儲存在 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者上。  
  
 衝突資訊的儲存由 **conflict_logging** 發行集屬性控制。 如需詳細資訊，請參閱 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 和 [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)。  
  
 衝突也可以使用「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 互動式解決器」在同步處理期間以互動的方式解決。 互動解決器可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager 使用。 如需詳細資訊，請參閱[使用 Windows Synchronization Manager 同步處理訂閱 &#40;Windows Synchronization Manager&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
### <a name="to-view-and-resolve-conflicts-for-merge-publications"></a>若要檢視並解決合併式發行集衝突  
  
1.  如果中有適當的) ，請連接到發行者 (或訂閱者 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要檢視衝突的發行集，然後按一下 **[檢視衝突]** 。  
  
    > [!NOTE]  
    >  如果將 **conflict_logging** 屬性的值指定為 **'subscriber'** ，就無法使用 **[檢視衝突]** 功能表選項。 若要檢視衝突，請從命令提示字元啟動 ConflictViewer.exe。 依預設，ConflictViewer.exe 位於下列目錄：Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE。 如需有效的啟動參數清單，請執行 ConflictViewer.exe -?。  
  
4.  在 **[選取衝突資料表]** 對話方塊中，選取要檢視衝突的資料庫、發行集和資料表。  
  
5.  在複寫衝突檢視器中，您可以：  
  
    -   使用上方格右側按鈕篩選資料列。  
  
    -   在上方格內選取資料列，以便於下方格的該資料列顯示資訊。  
  
    -   在上方方格中選取一個或多個資料列，然後按一下 **[移除]**，這相當於按一下 **[提交成功者]** 按鈕 (不會對資料進行任何變更)。  
  
    -   按一下 [屬性] 按鈕 (**...** ]) 以查看涉及衝突之資料行的詳細資訊。  
  
    -   在提交資料之前，編輯 **[衝突成功者]** 或 **[衝突失敗者]** 資料行中的資料 (灰色資料行表示資料為唯讀)。  
  
    -   按一下 **[提交成功者]** 以接受指定為衝突成功者的資料列。  
  
    -   按一下 **[提交失敗者]** ，以覆寫解決並將指定為衝突失敗者的值傳播到拓撲中的所有節點。  
  
    -   選取 **[記錄此衝突的詳細資料]** 即可將衝突資料記錄到檔案中。 若要指定檔案的位置，請指向 **[檢視]** 功能表，然後按一下 **[選項]** 。 輸入值，或按一下瀏覽按鈕 ( **[...]** )，然後導覽至適當的檔案。 按一下 **[確定]** 即可結束 **[選項]** 對話方塊。  
  
6.  關閉複寫衝突檢視器。  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [指定合併發行項解析程式](publish/specify-a-merge-article-resolver.md)  
  
  
