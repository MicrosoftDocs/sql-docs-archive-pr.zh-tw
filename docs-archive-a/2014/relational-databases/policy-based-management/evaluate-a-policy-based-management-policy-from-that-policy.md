---
title: 根據原則式管理原則評估該原則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 207c86f1465c49238fc9b50ee75489b43d956caf
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597777"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>根據原則式管理原則評估該原則
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用某個原則來評估該原則。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來評估原則：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy"></a>若要評估原則  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要評估之原則的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]**。  
  
4.  按一下加號展開 **[原則]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要評估的原則，然後選取 [評估]****。  
  
6.  在 **[評估結果]**  對話方塊中，您可以查看原則評估的結果。 如果目標不符合此原則而且其屬性可透過原則式管理來重新設定，您可以按一下 [套用]**** 來強制符合原則。 如需有關 **[評估原則]** 對話方塊中之可用選項的詳細資訊，請參閱＜ [Evaluate Policies Dialog Box, Policy Selection Page](evaluate-policies-dialog-box-policy-selection-page.md) ＞和＜ [Evaluate Policies Dialog Box, Evaluation Results Page](evaluate-policies-dialog-box-evaluation-results-page.md)＞。  
  
7.  完成後，請按一下 **[關閉]** 。  
  
  
