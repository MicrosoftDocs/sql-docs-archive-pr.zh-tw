---
title: 使用複合定義域中的值關聯 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.cdvaluerelations.f1
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 135934ec99fed612609e5e1b962f08bb93b98ede
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87709946"
---
# <a name="use-value-relations-in-a-composite-domain"></a>使用複合定義域中的值關聯
  此主題描述如何檢視在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 的知識探索程序期間針對複合定義域找到的值組合。 這個頁面會顯示值組合出現的次數。 複合定義域不支援值管理，所以您無法針對這些值執行任何作業。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 若要檢視值關聯，您必須已建立及開啟複合定義域。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能檢視複合定義域中的值關聯。  
  
##  <a name="view-value-relations"></a><a name="Use"></a>視圖值關聯  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，開啟或建立知識庫。 選取 **[定義域管理]** 當做活動，然後按一下 **[開啟]** 或 **[建立]**。 如需相關資訊，請參閱 [建立知識庫](../../2014/data-quality-services/create-a-knowledge-base.md) 或 [開啟知識庫](../../2014/data-quality-services/open-a-knowledge-base.md)。  
  
3.  從 **[定義域管理]** 頁面的 **[定義域清單]** 中，選取您想要建立定義域規則的複合定義域，或是建立新的複合定義域。 如果您必須建立新的定義域，請參閱＜ [Create a Composite Domain](../../2014/data-quality-services/create-a-composite-domain.md)＞。  
  
4.  按一下 **[值關聯]** 索引標籤。  
  
5.  檢視針對每一個值組合顯示的頻率。  
  
    > [!NOTE]  
    >  **[值]** 資料表會顯示存在於複合定義域中的每一個值組合。 每一個值都會顯示在它所適用的單一定義域中。 值關聯資料表預設會依據頻率排序，但是您可以按一下另一個資料行，依據該資料行排序。 只會顯示頻率大於或等於 20 的值。  
  
6.  您不能變更資料表中的任何值。 如果您已執行其他作業，請按一下 **[完成]** ，完成定義域管理活動。 否則，請按一下 [**取消**]。  
  
##  <a name="follow-up-after-viewing-value-relations"></a><a name="FollowUp"></a>後續操作：查看值關聯之後  
 在檢視值關聯之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../../2014/data-quality-services/managing-a-domain.md)或[建立比對原則](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
  
