---
title: 還原資料庫 (一般頁面) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoredb.general.f1
ms.assetid: 160cf58c-b06a-475f-9a69-2b051e5767ab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2a497e6a6e4584aa064783eba2076b7e50b36e8f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598460"
---
# <a name="restore-database-general-page"></a>還原資料庫 (一般頁面)
  使用 [一般] 頁面，為資料庫還原作業指定目標和來源資料庫的相關資訊。  
  
 **若要使用 SQL Server Management Studio 還原資料庫備份**  
  
-   [還原資料庫備份 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  當您使用指定還原工作時 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，可以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 按一下 [**腳本**]，然後選取腳本的目的地，以產生對應的[還原](/sql/t-sql/statements/restore-statements-transact-sql)腳本。  
  
## <a name="permissions"></a>權限  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，則 RESTORE 權限預設為 **系統管理員** 和 **dbcreator** 固定伺服器角色的成員，以及資料庫的擁有者 (**dbo**)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
 從加密備份還原，需要憑證的 `VIEW DEFINITION` 權限或在備份期間用於加密的非對稱金鑰。  
  
## <a name="options"></a>選項。  
  
### <a name="source"></a>來源  
 [還原來源] 面板的選項會識別資料庫備份組的位置以及您想要還原的備份組。  
  
|詞彙|定義|  
|----------|----------------|  
|**Database**|從下拉式清單中選取要還原的資料庫。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。|  
|**裝置**|選取內含您要還原之一個或多個備份的邏輯或實體備份裝置 (磁帶、URL 或檔案)。 如果在其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上建立資料庫備份，就需要這個選項。<br /><br /> 若要選取一個或多個邏輯或實體備份裝置，請按一下瀏覽按鈕以開啟 **[選取備份裝置]** 對話方塊。 您可以在這個對話方塊中選取屬於單一媒體集的裝置，最多可選取 64 個裝置。 磁帶裝置必須實際連接到執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的電腦。 備份檔案可位於本機磁碟裝置或抽取式磁碟裝置上。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。 您也可以選取 [URL] 作為裝置類型，以將備份檔案儲存在 Azure 儲存體中。<br /><br /> 當您結束 [選取備份裝置] 對話方塊時，選取的裝置將會以唯讀值的形式顯示在 [裝置] 清單中。|  
|**Database**|從下拉式清單中選取應該從中還原備份的資料庫名稱。<br /><br /> 注意:這份清單只能在選取 **[裝置]** 時使用。 只有在所選取裝置上有備份的資料庫才可供使用。|  
  
### <a name="destination"></a>Destination  
 **[還原至]** 面板的選項會識別資料庫和還原點。  
  
|詞彙|定義|  
|----------|----------------|  
|**Database**|輸入清單中要還原的資料庫。 您可以輸入新的資料庫，或者從下拉式清單中選擇現有的資料庫。 清單包含伺服器上的所有資料庫，排除系統資料庫 **master** 和 **tempdb**。<br /><br /> 注意:若要還原受密碼保護的備份，必須使用 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 陳述式。|  
|**[還原至]**|**[還原至]** 方塊預設為 [到上次建立的備份]。 您也可以按一下 **[時間表]** 顯示 **[備份時間表]** 對話方塊，這個對話方塊會以時間表的形式顯示資料庫備份記錄。 按一下 [**時程表**]，指定 `datetime` 您要還原資料庫的特定。 然後，資料庫將還原至這個指定之時間點的狀態。 請參閱 [Backup Timeline](backup-timeline.md)。|  
  
### <a name="restore-plan"></a>還原計畫  
  
|詞彙|定義|  
|----------|----------------|  
|**要還原的備份組**|顯示指定的位置可使用的備份組。 每個備份組 (即單一備份作業的結果) 都會分散放在媒體集中的所有裝置上。 根據預設，建議以還原計畫達到還原作業的目標 (此作業是根據必要備份組的選取項目而定)。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用 **msdb** 中的備份記錄識別還原資料庫所需的備份，並建立還原計畫。 例如，以資料庫還原而言，還原計畫會選取最近的完整資料庫備份，之後再加上最近的後續差異資料庫備份 (若有的話)。 在完整復原模式之下，還原計畫會接著選取所有後續的記錄備份。<br /><br /> 若要覆寫建議的復原計畫，您可以變更方格中的下列選項。 任何相依於已取消選取備份的備份，會自動被取消選取。<br /><br /> **還原**：<br />                          選取的核取方塊會指出要還原的備份組。<br />**名稱**：備份組的名稱。<br />**元件**：備份的元件：交易記錄) 的**資料庫** **、檔案**或 **\<blank>** (。<br />**類型**：執行的備份類型：[完整]、[差異] 或 [交易記錄]。<br />**伺服器**：[!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行備份作業的  執行個體名稱。<br />**Database**：與備份作業相關的資料庫名稱。<br />**位置**：備份組在磁碟區中的位置。<br />**第一個 LSN**：備份組中第一個交易的記錄序號。 針對檔案備份為空白。<br />**最後一個 LSN**：備份組中最後一個交易的記錄序號。 針對檔案備份為空白。<br />**檢查點 LSN**：建立備份時最近檢查點)  (LSN 的記錄序號。<br />**完整 LSN**：最新完整資料庫備份的記錄序號。<br />**開始日期**：備份作業開始的日期和時間，出現在用戶端的地區設定中。<br />**完成日期**：備份作業完成時的日期和時間，顯示在用戶端的地區設定中。<br />**大小**：備份組的大小（以位元組為單位）。<br />**使用者名稱**：執行備份作業的使用者名稱。<br /><br /> **到期**日：備份組到期的日期和時間。<br /><br /> 只有當您核取 **[手動選擇]** 方塊時，這些核取方塊才會啟用。 這可讓您選取要還原的備份組。<br /><br /> 核取 **[手動選取]** 方塊之後，每次修改 [還原計畫] 時，都會檢查其正確性。 如果備份的順序不正確，就會顯示錯誤訊息。|  
|**驗證備份媒體**|針對選取的備份組呼叫 RESTORE VERIFY_ONLY 陳述式。<br /><br /> 注意：這是一項長時間執行的作業，而且您可以使用對話方塊架構上的進度監視器來追蹤和取消其進度。<br /><br /> 這個按鈕可讓您先檢查選取之備份檔案的完整性，然後再進行還原。<br /><br /> 檢查備份組的完整性時，位於對話方塊左下方的進度狀態會顯示「驗證中」而非「執行中」。|  
  
## <a name="compatibility-support"></a>相容性支援  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您可以從使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本所建立的資料庫備份還原使用者資料庫。 但是， **無法還原使用**至 **所建立的** master **、** model [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] msdb [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]備份。 此外，任何舊版 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 都無法還原在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中建立的備份。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用與之前版本不同的預設路徑。 因此，若要還原在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之預設位置中所建立的資料庫，就必須使用 MOVE 選項。  
  
 將舊版資料庫還原成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，資料庫會自動升級。 通常，資料庫立即變為可用。 不過，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫具有全文檢索索引，升級程序就會根據 [全文檢索升級選項] 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為 [匯入] 或 [重建]，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。  
  
## <a name="restoring-from-an-encrypted-backup"></a>從加密備份還原  
 您要還原的目的地執行個體上，必須提供原本用於建立備份的憑證或非對稱金鑰，才能進行還原。 執行還原的帳戶應擁有憑證的 `VIEW DEFINITIONS` 權限或非對稱金鑰。 您不應該更新用於加密備份的憑證。  
  
## <a name="restoring-from-azure-storage"></a>從 Azure 儲存體還原  
 還原儲存在 Azure 儲存體中的備份時，還原 UI 會有新的 [備份裝置] 選項。 **[選取備份裝置]** ] 對話方塊上的 **[URL]** 。 當您按一下 [**新增**] 時，這會帶您前往 [**連接到 Azure** ] 對話方塊，讓您指定要向儲存體帳戶驗證的 SQL 認證資訊。  連線到儲存體帳戶後，備份檔案會顯示在 [在**Azure 中尋找備份檔案**] 對話方塊中，您可以在其中選取要用於還原的檔案。  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [從裝置還原備份 &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)   
 [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [還原交易記錄備份 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE 引數 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)   
 [套用交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
