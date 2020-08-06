---
title: MSSQLSERVER_1418 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1418 (Database Engine error)
ms.assetid: 6e9c7241-0201-44e0-9f8b-b3c4e293f0f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1fcac03f044aacce5e907824862eb589c97a07d2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87702945"
---
# <a name="mssqlserver_1418"></a>MSSQLSERVER_1418
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|1418|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_PARTNERNOTFOUND|  
|訊息文字|伺服器網路位址 "%.*ls" 無法連上或不存在。 請檢查網路位址名稱，並檢查本機和遠端端點的連接埠是否可正常運作。|  
  
## <a name="explanation"></a>說明  
 伺服器網路端點未回應，因為指定的伺服器網路位址無法連上或不存在。  
  
> [!NOTE]  
>  根據預設，[!INCLUDE[msCoName](../../includes/msconame-md.md)] 作業系統會封鎖所有通訊埠。  
  
## <a name="user-action"></a>使用者動作  
 檢查網路位址名稱，然後重新發出命令。  
  
 您可能必須同時在兩個夥伴上執行更正動作。 例如，如果嘗試在主體伺服器執行個體上執行 SET PARTNER 時引發了這個訊息，訊息中可能暗示您只需要在鏡像伺服器執行個體上採取更正動作。 但是您可能必須同時在兩個夥伴上執行更正動作。  
  
### <a name="additional-corrective-actions"></a>其他更正動作  
  
-   確定鏡像資料庫是否已做好鏡像的準備。  
  
-   確定鏡像伺服器執行個體的名稱和通訊埠是否正確。  
  
-   確定目標鏡像伺服器執行個體不在防火牆後面。  
  
-   確定主體伺服器執行個體不在防火牆後面。  
  
-   使用 **sys.database_mirroring_endpoints** 目錄檢視中的 **state** 或 **state_desc** 資料行來驗證夥伴上的端點是否已經啟動。 如果其中一個端點並未啟動，請執行 ALTER ENDPOINT 陳述式來啟動它。  
  
-   確定主體伺服器執行個體是否正在接聽指派給其資料庫鏡像端點的通訊埠，以及鏡像伺服器執行個體是否正在接聽其通訊埠。 如需詳細資訊，請參閱本主題稍後的「驗證通訊埠可用性」。 如果夥伴並未接聽其指派的通訊埠，請將資料庫鏡像端點改為接聽不同的通訊埠。  
  
    > [!IMPORTANT]  
    >  安全性設定不正確可能會導致一般安裝錯誤訊息。 伺服器執行個體通常會卸除不正確的連接要求，而不會回應。 對於呼叫者，安全性組態錯誤可能由於其他各種原因所造成，例如鏡像資料庫狀態不正確或不存在、權限不正確等等。  
  
### <a name="using-the-error-log-file-for-diagnosis"></a>使用錯誤記錄檔進行診斷  
 在某些情況下，您只能使用錯誤記錄檔來進行調查。 在這些情況下，請判斷錯誤記錄檔是否包含有關資料庫鏡像端點 TCP 通訊埠的錯誤訊息 26023。 這是嚴重性 16 的錯誤，可能代表資料庫鏡像端點並未啟動。 即使 **sys.database_mirroring_endpoints** 顯示端點狀態已經啟動，還是有可能引發這個訊息。  
  
 解決您遇到的任何問題之後，請在主體伺服器上重新執行 ALTER DATABASE *database_name* SET PARTNER 陳述式。  
  
### <a name="verifying-port-availability"></a>驗證通訊埠可用性  
 設定資料庫鏡像工作階段的網路時，請確定只有資料庫鏡像處理序會使用每個伺服器執行個體的資料庫鏡像端點。 如果有另一個處理序正在接聽指派給資料庫鏡像端點的通訊埠，其他伺服器執行個體的資料庫鏡像處理序便無法連接到該端點。  
  
 若要顯示 Windows 伺服器正在接聽的所有連接埠，請使用 **netstat** 命令提示字元公用程式。 **netstat** 語法依 Windows 作業系統的版本而定。 如需詳細資訊，請參閱作業系統文件集。  
  
#### <a name="windows-server-2003-service-pack-1-sp1"></a>Windows Server 2003 Service Pack 1 (SP1)  
 若要列出接聽通訊埠，以及已經開啟這些通訊埠的處理序，請在 Windows 命令提示字元下輸入下列命令：  
  
 **netstat -abn**  
  
#### <a name="windows-server-2003-pre-sp1"></a>Windows Server 2003 (pre-SP1)  
 若要識別接聽通訊埠，以及已經開啟這些通訊埠的處理序，請遵循下列步驟：  
  
1.  取得處理序識別碼。  
  
     若要取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的處理序識別碼，請連接到該執行個體並使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SELECT SERVERPROPERTY('ProcessID')   
    ```  
  
     如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜SERVERPROPERTY (Transact-SQL)＞。  
  
2.  比對處理序識別碼與下列 **netstat** 命令的輸出：  
  
     **netstat -ano**  
  
## <a name="see-also"></a>另請參閱  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)   
 [資料庫鏡像端點 &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)   
 [指定伺服器網路位址 &#40;資料庫鏡像&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)   
 [疑難排解資料庫鏡像組態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
