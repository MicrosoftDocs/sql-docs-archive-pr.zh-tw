---
title: 遠端處理 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d58bcb3c-0b3f-4ab0-81eb-4fdcc86153af
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4e0d6ade25f5a321e49c748692a961abc369efad
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597408"
---
# <a name="remote-processing-analysis-services"></a>遠端處理 (Analysis Services)
  您可以執行遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的排程處理或自動處理，其只會處理某電腦所發出的要求，但會在同一網路中的另一部電腦上執行。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   您的每部電腦上若各自執行不同版本的 SQL Server，則用戶端程式庫的版本與處理此模型之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的版本必須相符。 例如，若處理在 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 執行個體上進行，則發出要求的電腦便須擁有和 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]相同的用戶端程式庫。 請參閱 [用於 Analysis Services 連接的資料提供者](../instances/data-providers-used-for-analysis-services-connections.md)。  
  
-   遠端伺服器必須啟用 [允許遠端連線到此電腦] **** ，而發出處理要求的帳戶必須列名為允許的使用者。  
  
-   Windows 防火牆規則必須設定為允許 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的傳入連線。 確認您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接遠端 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行個體。 請參閱 [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
-   解決現有的本機處理錯誤，然後再嘗試遠端處理。 確認當處理要求來自本機時，可以順利從外部關聯式資料來源擷取資料。 如需指定用來擷取資料之認證相關指示，請參閱[設定模擬選項 (SSAS - 多維度)](set-impersonation-options-ssas-multidimensional.md)。  
  
## <a name="on-demand-remote-processing"></a>隨選遠端處理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接受具有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系統管理員權限之使用者或應用程式帳戶所發出的處理要求。 您若是系統管理員，請確認您可以連接到遠端執行個體，並可透過遠端連接手動處理資料庫。  
  
1.  在要用於排程處理電腦上啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，並連接到遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
2.  在資料庫上按一下滑鼠右鍵，再選取 [處理序]**** 並指向 [指令碼]****，然後選擇 [編寫動作的指令碼至新增查詢視窗]****。 用於叫用處理的命令會出現在查詢視窗中。  
  
3.  按一下 [確定] **** 開始執行處理序。  
  
     此工作若是成功，將會提供 XMLA 查詢讓您嵌入排程的作業中。 此工作也會確認連接沒有問題。  
  
## <a name="schedule-remote-processing-using-sql-server-agent-service"></a>使用 SQL Server Agent 服務排程遠端處理  
 SQL Server Agent 服務預設會以虛擬帳戶執行，並使用電腦帳戶所建立的網路連接。 為避免授與遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上之電腦帳戶的系統管理權限，應將 SQL Server Agent 服務變更為以最低權限的網域使用者帳戶身分執行。  
  
 請務必授與帳戶所有必要的權限，包括提供此服務之 Database Engine 執行個體的 **sysadmin** 權限。  
  
 您可以使用下列連結來設定權限：  
  
-   [設定 SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)  
  
-   若無法授與[SQL Server Agent Components](../../ssms/agent/sql-server-agent.md#Components) 權限， **SQL Server Agent Components** 建議使用替代的固定伺服器角色。  
  
 設定帳戶權限之後，請繼續執行下列步驟。  
  
#### <a name="grant-the-sql-server-agent-account-administrator-permission-on-ssas"></a>授與 SSAS 上之 SQL Server Agent 帳戶的系統管理員權限  
  
1.  使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]連接到遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
2.  在伺服器名稱上按一下滑鼠右鍵，再按一下 [屬性]****，然後按一下 [安全性]****。  
  
3.  按一下 [加入] **** ，以加入 SQL Server Agent 帳戶。  
  
#### <a name="create-the-job"></a>建立作業  
  
1.  在 Management Studio 中，連接到本機 Database Engine 執行個體。 SQL Server Agent 是物件總管中的最後一個項目。 如有必要，請啟動該服務。  
  
2.  在 [作業]**** 上按一下滑鼠右鍵，再按一下 [新增作業]****，然後輸入名稱。  
  
3.  在步驟中按一下 [新增] **** ，然後輸入名稱。  
  
4.  在 [類型] 中，選取 [SQL Server Analysis Services 命令] ****。  
  
5.  在 [伺服器] 中，輸入遠端名稱 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。  
  
6.  在 [命令] 中，貼上用以處理資料庫的 XMLA 命令。 這就是您在隨選遠端處理之驗證步驟中所產生的 XMLA 指令碼。 按一下 **[確定]** 以儲存作業。  
  
#### <a name="start-sql-server-profiler"></a>啟動 SQL Server Profiler  
  
1.  在遠端電腦上，啟動 SQL Server Profiler。 連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，然後按一下 [執行] **** ，以啟動使用預設事件的追蹤。  
  
     您將使用 SQL Server Profiler 監視所發生旳處理事件。  
  
2.  (選擇性) 您可以設定追蹤屬性，將追蹤傳送至檔案或資料庫中的資料表。  
  
#### <a name="run-the-job"></a>執行作業  
  
1.  在執行此作業的電腦上，確認此作業可以執行基本作業。 在物件總管中的 SQL Server Agent 下，先展開 [作業]****，再於剛才所建立的作業上按一下滑鼠右鍵，然後按一下 [從下列步驟啟動作業]****。 作業會立即啟動。 您可以在 SQL Server Profiler 中監視進度。  
  
2.  最後一個步驟是將作業修改成依照您所義的排程執行，並新增管理作業所需的警示或通知。 您也可能想要精簡處理指令碼，或在作業中建立多個步驟來單獨處理物件。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 元件](../../ssms/agent/sql-server-agent.md#Components)   
 [使用 SQL Server Agent 排程 SSAS 管理工作](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [批次處理 &#40;Analysis Services&#41;](batch-processing-analysis-services.md)   
 [多維度模型物件處理](processing-a-multidimensional-model-analysis-services.md)   
 [處理物件 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)  
  
  
