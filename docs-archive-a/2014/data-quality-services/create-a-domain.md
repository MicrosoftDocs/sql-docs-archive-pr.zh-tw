---
title: 建立定義域 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.createdomain.f1
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fad6abd795aa9412bb71d251623d92d3e13b889c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592270"
---
# <a name="create-a-domain"></a>建立定義域
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中建立定義域。 定義域中的值是欄位中資料的語意表示法。 如需定義域的詳細資訊，請參閱[管理定義域](../../2014/data-quality-services/managing-a-domain.md)。  
  
 建立新的定義域的方式有兩種。 第一種方式是在知識探索活動的對應步驟期間，當您正在分析資料取樣，將知識加入至新的知識庫或現有知識庫時。 第二種方式是在定義域管理活動期間，當您建立新的定義域，而不是變更現有定義域時。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 若要建立定義域，您必須已建立及開啟知識庫。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能建立定義域。  
  
##  <a name="create-a-domain-in-the-knowledge-discovery-activity"></a><a name="Discovery"></a> 在知識探索活動中建立定義域  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟知識庫]** ，然後選取知識庫，或是按一下 **[新增知識庫]** ，並輸入新知識庫的屬性。  
  
3.  選取 **[知識探索]** 當做活動，然後按一下 **[建立]** 建立新的知識庫，或按一下 **[開啟]** 開啟現有的知識庫。  
  
4.  在 **[對應]** 頁面上，指定資料來源的連接。 如需詳細資訊，請參閱＜ [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md)＞。  
  
5.  在 **[對應]** 資料表中，從空白資料列之 **[來源資料行]** 資料行的下拉式清單中選取來源資料行。 如果沒有對應的定義域存在，請按一下 **[建立定義域]** 圖示。  
  
##  <a name="create-a-domain-in-the-domain-management-activity"></a><a name="DomainManagement"></a> 在定義域管理活動中建立定義域  
  
1.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟知識庫]** ，然後選取知識庫，或是按一下 **[新增知識庫]** ，並輸入新知識庫的屬性。  
  
2.  選取 **[定義域管理]** 當做活動，然後按一下 **[建立]** 建立新的知識庫，或按一下 **[開啟]** 開啟現有的知識庫。  
  
3.  在 **[定義域管理]** 頁面上，按一下定義域清單上方的 **[建立定義域]** 圖示。  
  
##  <a name="set-domain-properties"></a><a name="Properties"></a>設定網域屬性  
  
1.  在 **[建立定義域]** 對話方塊中，輸入知識庫特有的名稱以及最多 256 個字元的描述。  
  
    > [!NOTE]  
    >  如需有關定義域屬性的詳細資訊，請參閱＜ [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md)＞。  
  
2.  為定義域中的值，從 **[資料類型]** 清單選取資料類型。 資料類型可以是 **[字串]** (預設值)、 **[日期]**、 **[整數]** 或 **[十進位]**。  
  
3.  選取 **[使用前置值]** 指定一組同義字中的前置值將會是輸出，而不是與其同義的值。 取消選取 **[使用前置值]** ，指定每一個同義字值都是正確或更正形式的輸出，而且不會由其群組的前置值加以取代。  
  
4.  如果資料類型是 **[字串]**，請選取 **[正在將字串標準化]** 來移除定義域值中的特殊字元，這樣可能會提升相符的可能性。  
  
5.  從 **[設定輸出格式為]** 下拉式清單中，選取當定義域中的資料值為輸出時，將套用的格式。 此格式專屬於步驟 2 中選取的資料類型，如下列清單所示：  
  
    -   如果是字串值，您可以指定字串應該輸出為大寫或小寫。  
  
    -   如果是日期值，您可以指定日、月和年的格式。  
  
    -   如果是整數值，您可以指定要套用之格式遮罩的類型。  
  
    -   如果是十進位值，您可以指定要套用之格式遮罩的精確度和類型。  
  
     在 **[設定輸出格式為]** 下拉式清單中選取 **[無]** ，表示不會套用清單中的任何格式。  
  
6.  如果資料類型是 **[字串]**，請在 **[語言]** 下拉式清單中選取您想要套用哪一個語言版本的拼字檢查 (如果您啟用拼字檢查)。  
  
7.  如果資料類型是 **[字串]**，請選取 **[啟用拼字檢查]** ，在擴展定義域時針對所有字串值執行拼字檢查。  
  
8.  如果資料類型是 **[字串]**，請選取 **[停用語法錯誤演算法]** 來擴展定義域，而不檢查字串值的語法錯誤。  
  
9. 按一下 [確定]  。  
  
10. 按一下 **[完成]** ，完成定義域管理活動，如＜ [結束定義域管理活動](../../2014/data-quality-services/end-the-domain-management-activity.md)＞中所述。  
  
##  <a name="follow-up-after-creating-a-domain"></a><a name="FollowUp"></a> 後續操作：建立定義域之後  
 在建立定義域之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../../2014/data-quality-services/managing-a-domain.md)或[建立比對原則](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
  
