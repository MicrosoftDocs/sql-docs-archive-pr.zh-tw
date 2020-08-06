---
title: 建立跨定義域規則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.testcdrule.f1
- sql12.dqs.dm.cdrules.f1
ms.assetid: 0f3f5ba4-cc47-4d66-866e-371a042d1f21
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cddcd9bbd2fc8d95fe8645781de5fe4e936050a9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687160"
---
# <a name="create-a-cross-domain-rule"></a>建立跨定義域規則
  本主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的知識庫內建立複合定義域的跨定義域規則。 跨定義域規則會在複合定義域所包含的單一定義域中測試值之間的關聯性。 跨定義域規則必須在複合定義域中成立，才能讓定義域值被視為正確且符合商務需求。 跨定義域規則是用來驗證、更正並標準化定義域值。  
  
 跨定義域規則的 If 子句和 Then 子句是分別針對複合定義域的其中一個單一定義域所定義。 您必須針對不同的單一定義域定義每個子句。 跨定義域規則必須與多個單一定義域相關。您無法針對複合定義域定義簡單定義域規則 (僅適用於單一定義域)。 您可以針對單一定義域定義定義域規則，藉以進行此作業。 If 子句和 Then 子句可以分別包含一個或多個條件。  
  
 具有最終條件的跨定義域規則會將規則邏輯套用至條件中值的同義字，以及值本身。 If 和 Then 子句的最終條件包括 [值等於]、[值不等於]、[值在] 或 [值不在]。 例如，假設您擁有複合定義域的下列跨定義域規則：「對於 'City' 而言，如果值等於 'Los Angeles'，則對於 'State' 而言，值等於 'CA'」。 如果 'Los Angeles' 和 'LA' 是同義字，此規則會針對 'Los Angeles CA' 和 'LA CA' 傳回正確，而針對 'Los Angeles WA' 和 'LA WA' 傳回錯誤。  
  
 除了只讓您知道跨定義域規則是否有效之外，跨定義域規則中的最終 *Then* 子句 **[值等於]** 也會在資料清理活動期間更正資料。 如需詳細資訊，請參閱＜ [Data Correction using Definitive Cross-Domain Rules](../../2014/data-quality-services/cleanse-data-in-a-composite-domain.md#CDCorrection) ＞中的 [Cleanse Data in a Composite Domain](../../2014/data-quality-services/cleanse-data-in-a-composite-domain.md)。  
  
 跨定義域規則會在只影響單一定義域的所有簡單規則之後納入考量。 只有當某個值通過單一定義域規則 (如果存在的話) 時，才會套用跨定義域規則。 您必須先定義所有要執行規則的複合定義域和單一定義域，然後才能執行規則。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 若要建立跨定義域規則，您必須已經建立並開啟複合定義域。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_administrator 角色，才能建立跨定義域規則。  
  
##  <a name="create-cross-domain-rules"></a><a name="Create"></a> 建立跨定義域規則  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，開啟或建立知識庫。 選取 **[定義域管理]** 當做活動，然後按一下 **[開啟]** 或 **[建立]**。 如需相關資訊，請參閱 [建立知識庫](../../2014/data-quality-services/create-a-knowledge-base.md) 或 [開啟知識庫](../../2014/data-quality-services/open-a-knowledge-base.md)。  
  
    > [!NOTE]  
    >  定義域管理會在 Data Quality Services 用戶端的頁面上執行，該頁面包含個別定義域管理作業所適用的五個索引標籤。 這不是精靈驅動的程序，任何管理作業都可以個別執行。  
  
3.  從 **[定義域管理]** 頁面的 **[定義域清單]** 中，選取您想要建立定義域規則的複合定義域，或是建立新的複合定義域。 如果您必須建立新的定義域，請參閱＜ [Create a Composite Domain](../../2014/data-quality-services/create-a-composite-domain.md)＞。  
  
4.  按一下 **[CD 規則]** 索引標籤。  
  
5.  按一下 **[加入新的定義域規則]**，然後輸入規則的名稱和描述。  
  
6.  選取 **[使用中]** 指定將要執行此規則 (預設值)，或取消選取以防止執行此規則。  
  
7.  依照下列方式建立 If 子句：  
  
    1.  在 If 子句窗格的定義域清單中，選取複合定義域所包含的其中一個單一定義域，成為 If 子句的主詞。 您可以選取複合定義域中的任何單一定義域。  
  
    2.  從下拉式清單中選取條件，做為子句的第一個條件。  
  
    3.  如果條件需要值，請在與條件相關聯的文字方塊中輸入值。  
  
    4.  如果 If 子句需要另一個條件，請按一下 **[將新條件加入選取的子句]**。 必要時，請選取運算子、選取條件，然後輸入條件的值。  
  
    5.  若要變更條件的順序，請按一下條件的左側加以選取，然後按一下向上或向下箭號。  
  
    6.  若要隱藏條件，請按一下定義域名稱左側的減號。 按一下加號，即可顯示條件。  
  
8.  在 Then 子句窗格的定義域清單中選取單一定義域 (If 子句主詞以外的定義域)，藉以建立 Then 子句。 然後，使用您在建置 If 子句時所進行的相同步驟來建置 Then 子句。  
  
9. 繼續進行下列測試程序。  
  
##  <a name="test-cross-domain-rules"></a><a name="Test"></a> 測試跨定義域規則  
  
1.  依照下列方式測試跨定義域規則：  
  
    1.  按一下複合定義域窗格右上角的 **[在測試資料上執行選取的定義域規則]** 圖示。  
  
    2.  在 **[測試定義域規則]** 對話方塊中，按一下 **[加入定義域規則的新測試詞彙]** 圖示。  
  
    3.  針對與 If 子句相關聯的單一定義域以及與 Then 子句相關聯的單一定義域輸入測試值。 在 If 子句中輸入的測試值必須符合該子句的條件，否則系統將在 **[有效性]** 資料行中輸入問號，表示跨定義域規則不適用於測試資料。  
  
    4.  再次按一下 **[加入定義域規則的新測試詞彙]** 圖示，加入另一組測試值。  
  
    5.  按一下 [**對所有詞彙測試定義域規則**] 圖示。 如果某組測試值有效，DQS 就會在該資料列的 **[有效性]** 資料行中輸入核取記號。 如果某組測試值無效，DQS 就會在該資料列的 [有效性] 資料行中輸入含驚嘆號的三角形。  
  
    6.  測試完成之後，請在 **[測試複合定義域規則]** 對話方塊中按一下 **[關閉]** 。  
  
2.  當您完成跨定義域規則時，請按一下 **[完成]** ，完成定義域管理活動，如＜ [End the Domain Management Activity](../../2014/data-quality-services/end-the-domain-management-activity.md)＞中所述。  
  
##  <a name="follow-up-after-creating-a-cross-domain-rule"></a><a name="FollowUp"></a> 後續操作：建立跨定義域規則之後  
 在建立跨定義域規則之後，您可以針對定義域執行其他定義域管理工作、執行知識探索來將知識加入至定義域，或者將比對原則加入至定義域。 如需詳細資訊，請參閱[執行知識探索](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../../2014/data-quality-services/managing-a-domain.md)或[建立比對原則](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
  
