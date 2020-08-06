---
title: 備份資料庫 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1c315c827e1c8b206b2098009510bf6468bd7d74
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606932"
---
# <a name="back-up-database-general-page"></a>備份資料庫 (一般頁面)
  使用 **[備份資料庫]** 對話方塊上的 **[一般]** 頁面，檢視或修改資料庫備份作業設定。  
  
 如需基本備份概念的詳細資訊，請參閱[備份概觀 &#40;SQL Server&#41;](backup-overview-sql-server.md)。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定備份工作時，您可以按下 [指令碼]  按鈕，然後選取指令碼的目的地，以產生相對應的 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) 指令碼。  
  
 **若要使用 SQL Server Management Studio 建立備份**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  您可以定義資料庫維護計畫來建立資料庫備份。 如需詳細資訊，請參閱《 [線上叢書》中的](../maintenance-plans/maintenance-plans.md) 資料庫維護計畫 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。  
  
 **建立部分備份**  
  
-   如需部分備份，您必須使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) 陳述式搭配 PARTIAL 選項。  
  
## <a name="options"></a>選項。  
  
### <a name="source"></a>來源  
 **[來源]** 面板的選項會識別資料庫，並指定備份作業的備份類型和元件。  
  
 **Database**  
 選取要備份的資料庫。  
  
 **復原模式**  
 檢視選取的資料庫所顯示的復原模式 (SIMPLE、FULL 或 BULK_LOGGED)。  
  
 **備份類型**  
 選取要在指定的資料庫上執行的備份類型。  
  
|備份類型|可使用於|限制|  
|-----------------|-------------------|------------------|  
|完整|資料庫、檔案及檔案群組|在 **master** 資料庫上，只能使用完整備份。<br /><br /> 在簡單復原模式之下，檔案和檔案群組備份只可用於唯讀檔案群組。|  
|差異|資料庫、檔案及檔案群組|在簡單復原模式之下，檔案和檔案群組備份只可用於唯讀檔案群組。|  
|交易記錄|交易記錄|交易記錄備份無法使用於簡單復原模式。|  
  
 **只複製備份**  
 選取此選項，即可建立只複製備份。 「只複製備份」  是與傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份順序無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](copy-only-backups-sql-server.md)。  
  
> [!NOTE]  
>  選取 **[差異]** 選項時，您無法建立「只複製」備份。  
  
 **備份元件**  
 選取要備份的資料庫元件。 如果 **[備份類型]** 清單中已選取 **[交易記錄]** ，則不會啟動此選項。  
  
 選取下列選項按鈕之一：  
  
|||  
|-|-|  
|**Database**|指定備份整個資料庫。|  
|**檔案與檔案群組**|指定備份指定的檔案和 (或) 檔案群組。<br /><br /> 選取這個選項會開啟 **[選取檔案與檔案群組]** 對話方塊。 在選取了要備份的檔案群組或檔案，並按一下 **[確定]** 之後，選取項目就會出現在 **[檔案群組與檔案]** 方塊中。|  
  
### <a name="destination"></a>Destination  
 **[目的地]** 面板的選項可讓您指定備份作業的備份裝置類型，並尋找現有的邏輯或實體備份裝置。  
  
> [!NOTE]  
>  如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份裝置的相關資訊，請參閱[備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)。  
  
 **備份至**  
 選取下列要備份之媒體類型的其中之一。 您選取的目的地會出現在 **[備份至]** 清單中。  
  
|||  
|-|-|  
|**磁碟**|備份至磁碟。 這可能是針對資料庫所建立的系統檔案，或以磁碟為基礎的邏輯備份裝置。 目前選取的磁碟會出現在 **[備份至]** 清單中。 您最多可以為備份作業選取 64 個磁碟裝置。|  
|**磁帶**|備份至磁帶。 這可能是針對資料庫所建立的本機磁帶機，或以磁帶為基礎的邏輯備份裝置。 目前選取的磁帶會出現在 **[備份至]** 清單中。 最大數目是 64。 如果伺服器上沒有附加磁帶裝置，則會停用此選項。 您選取的磁帶會列在 **[備份至]** 清單中。<br /><br /> 注意:未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中將會移除磁帶備份裝置的支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。|  
|**URL**|備份至 Azure Blob 儲存體。|  
  
 所顯示的下一組選項取決於選取的目的地類型。 如果選取 [磁碟] 或 [磁帶]，則會顯示下列選項。  
  
 **加入**  
 將檔案或裝置加入至 **[備份至]** 清單。 您在本機磁碟或遠端磁碟上，最多可以同時備份到 64 個裝置。 若要指定遠端磁碟上的檔案，請使用完整的通用命名慣例 (UNC) 名稱。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。  
  
 **移除**  
 從 **[備份至]** 清單中，移除一個或多個目前選取的裝置。  
  
 **Contents**  
 顯示選取之裝置的媒體內容。  
  
 如果選取 URL 做為備份目的地，則會顯示下列選項：  
  
 **檔案名稱**  
 指定備份檔案的名稱。  
  
 **SQL 認證**  
 選取用來驗證 Azure 儲存體的 SQL 認證。 如果沒有現有可用的 SQL 認證，請按一下 **[建立]** 按鈕建立新的 SQL 認證。  
  
> [!IMPORTANT]  
>  在您按一下 **[建立]** 時開啟的對話方塊需要管理憑證或訂閱的發行設定檔。 如果您無法存取管理憑證或發行設定檔，可以使用 Transact-SQL 或 SQL Server Management Studio 來指定儲存體帳戶名稱和存取金鑰資訊，藉以建立 SQL 認證。 請參閱中的範例程式碼，[以建立認證](../security/authentication-access/create-a-credential.md#Credential)主題，以使用 transact-sql 來建立認證。 或者，使用 SQL Server Management Studio，在資料庫引擎執行個體中，以滑鼠右鍵按一下 **[安全性]**、選取 **[新增]**，然後選取 **[認證]**。 針對 **[識別]** 指定儲存體帳戶名稱，並且在 **[密碼]** 欄位中指定存取金鑰。  
  
 **Azure 儲存體容器**  
 指定 Azure 儲存體容器的名稱  
  
 **URL 前置詞：**  
 這會根據儲存在 SQL 認證中的儲存體帳戶資訊，以及您指定的 Azure 儲存體容器名稱自動產生。 建議您除非使用的網域採用 **\<storage account>.blob.core.windows.net** 以外的格式，否則請勿編輯此欄位中的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [備份檔案和檔案群組 &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [復原模式 &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
