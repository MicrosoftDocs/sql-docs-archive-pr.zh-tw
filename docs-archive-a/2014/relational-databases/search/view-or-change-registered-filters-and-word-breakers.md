---
title: 檢視或變更已註冊的篩選與斷詞工具 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], word breakers
- full-text search [SQL Server], filters
- filters [full-text search]
- word breakers [full-text search]
ms.assetid: f88c54df-b1aa-4701-807f-dc92c32363fd
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 79ad7f1f7df15fed21a132bbe253adc7185d8c06
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87697810"
---
# <a name="view-or-change-registered-filters-and-word-breakers"></a>檢視或變更已註冊的篩選與斷詞工具
  在系統上安裝或解除安裝任何斷詞工具或篩選器之後，這些變更不會自動在伺服器執行個體上生效。 此主題描述如何檢視目前已註冊的斷詞工具或篩選，以及如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上註冊新安裝的斷詞工具和篩選。  
  
### <a name="to-view-a-list-of-languages-whose-word-breakers-are-currently-registered"></a>若要檢視目前已註冊斷詞工具的語言清單  
  
1.  使用 [sys.fulltext_languages](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) 目錄檢視，如下所示：  
  
    ```  
    SELECT * FROM sys.fulltext_languages;   
    ```  
  
### <a name="to-view-a-list-of-the-filters-that-are-currently-registered"></a>若要檢視目前已註冊的篩選清單  
  
1.  使用 [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) 系統預存程序，如下所示：  
  
    ```  
    EXEC sp_help_fulltext_system_components 'filter';    
    ```  
  
### <a name="to-register-newly-installed-word-breakers-and-filters"></a>若要註冊新安裝的斷詞工具和篩選  
  
1.  使用 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql) 系統預存程序來更新語言的清單，如下所示：  
  
    ```  
    exec sp_fulltext_service 'update_languages';   
    ```  
  
### <a name="to-unregister-uninstalled-word-breakers-and-filters"></a>取消註冊已解除安裝的斷詞工具與篩選  
  
1.  使用 **sp_fulltext_service** 來更新語言的清單，如下所示：  
  
    ```  
    exec sp_fulltext_service 'update_languages'  
    ```  
  
2.  使用 **sp_fulltext_service** 重新啟動篩選背景程式主機處理序 (fdhost.exe)，如下所示：  
  
    ```  
    exec sp_fulltext_service 'restart_all_fdhosts';  
    ```  
  
### <a name="to-replace-existing-word-breakers-or-filters-when-installing-new-ones"></a>若要在安裝新的斷詞工具或篩選時取代現有的斷詞工具或篩選  
  
1.  準備安裝含有新斷詞工具或篩選的 DLL 檔案時，請確認它的檔案名稱與伺服器執行個體上安裝的任何現有 DLL 檔案不同。  
  
2.  將新的 DLL 檔案複製到包含伺服器執行個體之標準 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL 檔案的目錄中。 預設位置為：  
  
     C:\Program Files\Microsoft SQL Server\MSSQL.*執行個體名稱*\MSSQL\Binn  
  
    > [!IMPORTANT]  
    >  我們強烈建議您只載入已簽署且經過驗證的元件。 此外，我們建議您使用最低的可能權限，執行 FDHOST 啟動器 (MSSQLFDLauncher) 服務。  
  
3.  安裝新的斷詞工具或篩選。  
  
     **安裝並載入 Microsoft Filter Pack IFilters**  
  
    -   [How to register Microsoft Filter Pack IFilters with SQL Server (如何對 SQL Server 註冊 Microsoft Filter Pack IFilter)](https://go.microsoft.com/fwlink/?LinkId=130439)  
  
4.  使用 **sp_fulltext_service** 將新安裝的斷詞工具與篩選，載入伺服器執行個體中，如下所示：  
  
    ```  
    EXEC sp_fulltext_service @action='load_os_resources', @value=1;  
    ```  
  
5.  使用 **sp_fulltext_service** 來更新語言的清單，如下所示：  
  
    ```  
    EXEC sp_fulltext_service 'update_languages';  
    ```  
  
6.  使用 **sp_fulltext_service** 重新啟動篩選背景程式主機處理序 (fdhost.exe)，如下所示：  
  
    ```  
    EXEC sp_fulltext_service 'restart_all_fdhosts';   
    ```  
  
## <a name="see-also"></a>另請參閱  
 [設定全文檢索篩選背景程式啟動器的服務帳戶](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [設定及管理搜尋的篩選](configure-and-manage-filters-for-search.md)   
 [設定及管理搜尋的斷詞工具與字幹分析器](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
