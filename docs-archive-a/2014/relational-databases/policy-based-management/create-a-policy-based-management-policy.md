---
title: 建立原則式管理原則 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policies
ms.assetid: b28bf963-89f9-4941-b6c1-6004fec347f1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e76b4dce17e00bae5e8ca4fcf071868c0641c786
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596671"
---
# <a name="create-a-policy-based-management-policy"></a>建立原則式管理原則
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立原則式管理原則。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來建立原則：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-policy"></a>若要建立原則  
  
1.  在物件總管  中，按一下加號，展開您想要建立新原則式管理原則的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]** 。  
  
4.  以滑鼠右鍵按一下 [原則]  資料夾，然後選取 [新增原則]  。  
  
5.  在 **[建立新原則]** 對話方塊的 **[名稱]** 方塊中，輸入新原則的名稱。  
  
6.  如果您想要在建立原則時立即啟用原則，請選取 **[已啟用]** 核取方塊。 如果評估模式為 **[視需要]** ，就無法使用 **[已啟用]** 核取方塊。  
  
7.  在 **[檢查條件]** 清單中，選取其中一個現有的條件，或選取 **[新增條件]** 。 若要編輯條件，請選取該條件，然後按一下省略符號 (...)  。如需詳細資訊，請參閱[建立新的原則式管理條件](create-a-new-policy-based-management-condition.md)或[檢視或修改原則式管理條件的屬性](view-or-modify-the-properties-of-a-policy-based-management-condition.md)。  
  
8.  在 **[針對目標]** 方塊中，針對此原則選取一個或多個目標類型。 某些條件和 Facet 只能套用至特定目標類型。 可用的目標集會顯示在相關聯的方塊中。 展開 **[全部]** ，針對某些目標類型選取篩選條件。 如果此方塊中沒有出現任何目標，這表示檢查條件的範圍設定為伺服器層級。  
  
9. 在 **[評估模式]** 方塊中，選取這個原則的行為方式。 不同的條件可以有不同的有效評估模式。 如需哪些評估模式有效的詳細資訊，請參閱 [使用原則式管理來管理伺服器](administer-servers-by-using-policy-based-management.md)。  
  
10. 如果此原則將依排程來評估，請將評估模式設定為 **[按排程時間]** ，然後按一下 **[挑選]** 選取排程，或是按一下 **[新增]** 建立新的排程。  
  
11. 若要將此原則限制為目標類型的子集，請在 **[伺服器限制]** 方塊中，選取限制條件或建立新的條件。  
  
     如需有關 **[建立新原則]** 對話方塊可用之選項的詳細資訊，請參閱＜ [建立新原則或開啟原則對話方塊，一般頁面](../../integration-services/general-page-of-integration-services-designers-options.md) ＞或＜ [建立新原則或開啟原則對話方塊，描述頁面](create-new-policy-or-open-policy-dialog-box-description-page.md)＞。  
  
12. 完成後，請按一下 **[確定]** 。  
  
  
