---
title: 取消報表伺服器作業 (Management Studio) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d0ef8ada32aab4ac368871da711d0fe63fff7620
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706182"
---
# <a name="cancel-report-server-jobs-management-studio"></a>取消報表伺服器作業 (Management Studio)
  您可以使用 [取消報表伺服器作業]  對話方塊來檢視或取消進行中的報表。 這個對話方塊會顯示目前正在報表伺服器上執行的所有作業。 雖然您無法暫停或重新啟動目前正在處理中的作業，但是如果完成作業需要花太長的時間，您就可以取消所有作業或個別作業。  
  
 您可以取消使用者作業和系統作業。  
  
-   使用者作業是由個別使用者起始的任何作業。 這種作業包括視需要執行報表、手動建立報表記錄快照集，或者手動建立報表執行快照集。 進行中標準訂閱也是使用者作業。  
  
-   系統作業是由報表伺服器起始的作業。 系統作業包括排程的報表處理。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，連接至報表伺服器，以滑鼠右鍵按一下 [作業]  ，然後按一下 [取消所有作業]  。 您也可以開啟 [作業]  ，以滑鼠右鍵按一下正在報表伺服器上執行的作業，然後選取 [取消作業]  。  
  
 取消作業之前，您可以檢視其屬性，以便判斷該作業的開始時間。 如需詳細資訊，請參閱[作業屬性 &#40;Management Studio&#41;](job-properties-management-studio.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services 不支援這項功能。 因此，當您執行 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]時，不會出現此頁面。  
  
## <a name="options"></a>選項。  
 **名稱**  
 顯示報表的名稱。 依據描述來識別訂閱。  
  
 **型別**  
 有效值為 [使用者]  和 [系統]  。  
  
 **Start Time**  
 顯示作業的開始時間。  
  
 **使用者名稱**  
 若為使用者所起始的作業，這個資料行會顯示該使用者的名稱。  
  
 **狀態**  
 顯示作業的狀態。 有效值為 **[新增]** 和 **[正在執行]** 。 當作業啟動時，狀態永遠是 **[新增]** 。 60 秒之後，狀態會變更為 **[正在執行]** 。 您必須重新整理此頁面，才能收取變更。  
  
 **確定**  
 取消單一作業或多項作業。 作業會立即取消而且無法繼續進行。 如果您不小心取消了作業，就必須再次要求報表或訂閱，才能啟動新的作業。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [管理執行中的處理序](../subscriptions/manage-a-running-process.md)  
  
  
