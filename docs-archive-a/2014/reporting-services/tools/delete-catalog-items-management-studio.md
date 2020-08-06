---
title: 刪除目錄項目 (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.deleteitems.f1
ms.assetid: b0599e01-6dc3-4484-80d4-022a412e0ebd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d2a1824f2611165c9ae891fcb702418244f3621e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87594936"
---
# <a name="delete-catalog-items-management-studio"></a>刪除目錄項目 (Management Studio)
  您可以使用這個頁面刪除共用排程和角色定義。  
  
 如果您刪除了多個報表和訂閱所使用的共用排程，報表伺服器將會針對先前使用此共用排程的每個報表和訂閱建立個別的排程。 每個新的個別排程將包含共用排程中原本指定的日期、時間和循環模式。 請注意， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供個別排程的集中管理功能。 如果您刪除了共用排程，現在就必須針對每個個別項目維護排程資訊。 刪除共用排程之前，請使用 [報表頁面](schedule-properties-reports-page.md) 來判斷哪些報表目前正在使用共用排程。  
  
 若為角色定義，您只能刪除目前並未在角色指派中使用的角色定義。 如果您嘗試刪除目前使用中的角色，報表伺服器將不會刪除該角色，而且您會看見描述此一情況的錯誤訊息。 如果這個頁面包含目前未使用中的單一角色定義，當您按一下 **[確定]** 時，系統就會刪除它。 如果這個頁面包含多個角色，您無法選取要保留或移除的角色。 當您按一下 **[確定]** 時，系統將刪除所有未使用的角色定義。  
  
 您無法恢復刪除作業。 如果想要復原已刪除的項目，您就必須重新建立它，或是用報表伺服器資料庫的備份副本來還原。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定您正在刪除之項目的名稱。  
  
 **型別**  
 顯示您正在刪除之項目的類型。  
  
 **擁有者**  
 顯示擁有者的名稱。 在大多數情況下，這就是 System。  
  
 **狀態**  
 顯示刪除作業的進度資訊。  
  
 **錯誤**  
 如果在刪除項目時發生錯誤，則顯示錯誤碼。  
  
## <a name="see-also"></a>另請參閱  
 [刪除項目 &#40;Management Studio&#41;](delete-an-item-management-studio.md)   
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [建立、修改和刪除排程](../subscriptions/create-modify-and-delete-schedules.md)  
  
  
