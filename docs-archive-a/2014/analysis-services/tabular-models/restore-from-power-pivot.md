---
title: 從 PowerPivot 還原 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4dbb0e7867451e67eaa1503c54d7e3da1c276965
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87706794"
---
# <a name="restore-from-powerpivot"></a>從 PowerPivot 還原
  您可以在 SQL Server Management Studio 中使用 [從 PowerPivot 還原] 功能，於 Analysis Services 執行個體上建立新的表格式模型資料庫 (以表格式模式執行)，或是從 PowerPivot 活頁簿 (.xlsx) 還原到現有的資料庫。  
  
> [!NOTE]  
>  SQL Server Data Tools 中的 [從 PowerPivot 匯入] 專案範本提供了類似的功能。 如需詳細資訊，請參閱[從 PowerPivot 匯入 &#40;SSAS 表格式&#41;](import-from-power-pivot-ssas-tabular.md)。  
  
 使用 [從 PowerPivot 還原] 功能時，請牢記以下事項：  
  
-   若要使用 [從 PowerPivot 還原] 功能，您必須以 Analysis Services 執行個體上伺服器管理員角色的成員身分登入。  
  
-   Analysis Services 執行個體服務帳戶必須對您要從中還原的活頁簿檔案具有讀取權限。  
  
-   依預設，當您從 PowerPivot 還原資料庫時，表格式模型資料庫的 [資料來源模擬資訊] 屬性會設為 [預設值]，而這是指定 Analysis Services 執行個體服務帳戶。 建議您在 [資料庫屬性] 中，將模擬認證變更為 Windows 使用者帳戶。 如需詳細資訊，請參閱[模擬 &#40;SSAS 表格式&#41;](impersonation-ssas-tabular.md)。  
  
-   PowerPivot 資料模型中的資料將會複製到 Analysis Services 執行個體上現有或新的表格式模型資料庫。 如果您的 PowerPivot 活頁簿包含連結資料表，這些資料表將會重新建立成為不具資料來源的資料表，類似於使用 [貼上至新資料表] 所建立的資料表。  
  
### <a name="to-restore-from-powerpivot"></a>從 PowerPivot 還原  
  
1.  在 SSMS 中，于您想要還原的 Active Directory 實例中，以滑鼠右鍵按一下 [**資料庫**]，然後按一下 [**從 PowerPivot 還原**]。  
  
2.  在 [**從 PowerPivot 還原**] 對話方塊的 [**還原來源**] 中，按一下 [**備份檔案**] 中的 **[流覽]**，然後選取要從中還原的 .abf 或 xslx 檔案。  
  
3.  在 [還原目標]**** 的 [還原資料庫]**** 中，輸入新資料庫或現有資料庫的名稱。 如果您沒有指定名稱，就會使用活頁簿的名稱。  
  
4.  按一下 [儲存位置]**** 中的 [瀏覽]****，然後選取要儲存資料庫的位置。  
  
5.  在 [選項]**** 中，保持核取 [包含安全性資訊]****。 從 PowerPivot 活頁簿還原時，這項設定並不適用。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型資料庫 &#40;SSAS 表格式&#41;](tabular-model-databases-ssas-tabular.md)   
 [從 PowerPivot 匯入 &#40;SSAS 表格式&#41;](import-from-power-pivot-ssas-tabular.md)  
  
  
