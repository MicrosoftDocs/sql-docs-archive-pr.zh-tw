---
title: 將多維度資料庫的相容性層級設定 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 978279e6-a581-4184-af9d-8701b9826a89
author: minewiskan
ms.author: owend
ms.openlocfilehash: eea3d522abc5133e759cf476f3b169fd570b196f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87705657"
---
# <a name="set-the-compatibility-level-of-a-multidimensional-database-analysis-services"></a>設定多維度資料庫的相容性層級 (Analysis Services)
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，資料庫相容性層級屬性會決定資料庫的功能層級。 每個模型類型都有唯一的相容性層級。 例如，的相容性層級 `1100` 根據資料庫是多維度或表格式而有不同的意義。  
  
 本主題描述只適用於多維度資料庫的相容性層級。 如需表格式方案的詳細資訊，請參閱[&#40;SSAS 表格式 SP1&#41;的相容性層級](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
> [!NOTE]  
>  表格式模型具有另外的資料庫相容性層級，並不適用於多維度模型。 多維度模型不存在相容性層級 `1103`。 如需表格式方案的詳細資訊，請參閱[SQL Server 2012 SP1 和相容性層級中的表格式模型的新功能](https://go.microsoft.com/fwlink/?LinkId=301727) `1103` 。  
  
 **多維度資料庫的相容性層級**  
  
 目前唯一會隨功能層級而改變的多維度資料庫行為就是字串儲存體架構。 經由提高資料庫的相容性層級，您可以覆寫量值和維度的 4 GB 字串儲存體上限。  
  
 對於多維度資料庫，`CompatibilityLevel` 屬性的有效值包括：  
  
|設定|描述|  
|-------------|-----------------|  
|`1050`|在指令碼或工具中並不會看見這個值，但它對應至在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中所建立的資料庫。 所有未明確設定 `CompatibilityLevel` 的資料庫都是隱含地在 `1050` 層級執行。|  
|`1100`|這是您在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中建立之新資料庫的預設值。 您也可以針對使用舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立的資料庫指定這個值，以啟用僅在此相容性層級支援的功能 (亦即，維度屬性的增加字串儲存體或包含字串資料的相異計數量值)。<br /><br /> 已 `CompatibilityLevel` 設定為 `1100` 取得額外屬性的資料庫，可 `StringStoresCompatibilityLevel` 讓您選擇資料分割和維度的替代字串儲存體。|  
  
> [!WARNING]  
>  將資料庫相容性設為更高的層級將無法回復。 將相容性層級增加到之後 `1100` ，您必須在較新的伺服器上繼續執行資料庫。 您無法回復至 `1050` 。 您無法 `1100` 在或之前的伺服器版本上附加或還原資料庫 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。  
  
## <a name="prerequisites"></a>Prerequisites  
 資料庫相容性層級是在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引進。 您必須有 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或更新版本，才能檢視或設定資料庫相容性層級。  
  
 資料庫不可為本機 Cube。 本機 Cube 不支援 `CompatibilityLevel` 屬性。  
  
 資料庫必須已經使用舊版 (SQL Server 2008 R2 或更早版本) 建立，然後附加或還原到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或更新版本的伺服器。 部署至 SQL Server 2012 的資料庫已是 `1100`，且無法降級至較低層級執行。  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>判斷多維度資料庫的現有資料庫相容性層級  
 檢視或修改資料庫相容性層級的唯一方式是透過 XMLA。 您可以在 SQL Server Management Studio 中檢視或修改指定資料庫的 XMLA 指令碼。  
  
 如果您在資料庫的 XMLA 定義中搜尋屬性 `CompatibilityLevel` 而此屬性並不存在，很有可能該資料庫是位於 `1050` 層級。  
  
 下一節中會提供檢視及修改 XMLA 指令碼的指示。  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中設定資料庫相容性層級  
  
1.  在提高相容性層級之前，請先備份資料庫，以防您之後想要還原變更。  
  
2.  使用 SQL Server Management Studio 連接至裝載資料庫的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。  
  
3.  以滑鼠右鍵按一下資料庫名稱，依序指向 [編寫資料庫的指令碼為]**** 和 [ALTER 至]****，然後選取 [新增查詢編輯器視窗]****。 資料庫的 XMLA 表示法將會在新視窗中開啟。  
  
4.  複製下面 XML 元素：  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  將它貼到 `</Annotations>` 結束元素的後面和 `<Language>` 元素的前面。 XML 看起來應該類似於下面範例：  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  儲存檔案。  
  
7.  若要執行指令檔，按一下 [查詢] 功能表上的 [執行]****，或按 F5 鍵。  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>支援且需要相同相容性層級的作業  
 以下作業要求來源資料庫共用相同的相容性層級。  
  
1.  只有在兩個資料庫共用相同的相容性層級時，才支援從不同資料庫合併磁碟分割。  
  
2.  從其他資料庫使用連結的維度需要相同的相容性層級。 例如，如果您想要從資料庫中的資料庫使用連結的維度 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ，您必須將 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 資料庫移植至伺服器， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 並將相容性層級設定為 `1100` 。  
  
3.  只有共用相同版本與資料庫相容性層級的伺服器，才支援同步處理伺服器。  
  
## <a name="next-steps"></a>後續步驟  
 在您提高資料庫相容性層級之後，就可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中設定 `StringStoresCompatibilityLevel` 屬性。 這樣做會增加量值和維度的字串儲存體。 如需這項功能的詳細資訊，請參閱 [設定維度及資料分割的字串存放區](configure-string-storage-for-dimensions-and-partitions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [備份、還原和同步處理資料庫 &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
