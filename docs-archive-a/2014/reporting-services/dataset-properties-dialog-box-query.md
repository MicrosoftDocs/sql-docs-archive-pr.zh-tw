---
title: 資料集屬性對話方塊、查詢 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10160"
- sql12.rtp.rptdesigner.datasetproperties.query.f1
ms.assetid: 1fa34a4b-7de0-4e92-99fa-bc28a206773f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bffb14155d37e67333eb626747e1fcc54e618bbe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87606643"
---
# <a name="dataset-properties-dialog-box-query"></a>資料集屬性對話方塊、查詢
  選取 [**資料集屬性**] 對話方塊上的 [**查詢**]，即可選擇資料來源並建立查詢。  
  
 **[資料集屬性]** 對話方塊包含下列項目：  
  
-   [資料集屬性對話方塊、參數](report-data/dataset-properties-dialog-box-parameters.md)  
  
-   [資料集屬性對話方塊、欄位](../../2014/reporting-services/dataset-properties-dialog-box-fields.md)  
  
-   [資料集屬性對話方塊、選項](../../2014/reporting-services/dataset-properties-dialog-box-options.md)  
  
-   [資料集屬性對話方塊、篩選](report-data/dataset-properties-dialog-box-filters.md)  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入資料集的名稱。 此名稱不可以與報表中任何資料區域或群組的名稱相同。  
  
 **資料來源**  
 選取要做為資料集基礎的資料來源。 若要建立新的資料來源，按一下 **[新增]**。  
  
 **查詢類型**  
 選取資料集使用的命令或查詢類型。 選取 **[文字]** 來執行查詢，以便從資料庫中擷取資料。 選取 **[資料表]** 即可使用 **的** [TableDirect] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能來選取資料表中的所有欄位。 選取 **[預存程序]** 即可依名稱執行預存程序。 依預設，會選取 **[文字]** ，這適用於大多數的查詢。 若要編輯選取的資料來源查詢，按一下 **[查詢設計工具]**。  
  
> [!NOTE]  
>  並非所有的查詢類型都受到所有資料來源的支援。 例如， **[資料表]** 只受到 **[OLE DB]** 和 **[ODBC]** 資料來源類型的支援。  
  
 **查詢**  
 此選項會在選擇 [文字]**** 命令類型選項時出現。 鍵入查詢，或按一下 [匯入]**** 來匯入已存在的查詢。 按一下**運算式** (*Fx*) ] 按鈕，即可編輯運算式。  
  
> [!NOTE]  
>  如果您使用查詢設計工具來建立查詢，則查詢的文字會顯示在此方塊中。  
  
 **資料表名稱**  
 輸入您想要當做資料集使用之資料表的名稱。 此選項會在您選取 **[資料表]** 時出現。  
  
 **選取或輸入預存程序名稱**  
 輸入或選擇您要使用之預存程序的名稱。 按一下**運算式** (*Fx*) ] 按鈕，即可編輯運算式。 此選項會在選擇 [預存程序] 命令類型選項時出現。  
  
 **逾時 (以秒為單位)**  
 輸入查詢超時之前的秒數。預設值是30秒。 **[逾時]** 的值必須是空白或大於零。 如果是空白，則查詢不會逾時。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的資料連線、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [查詢設計工具 &#40;報表產生器&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Reporting Services 查詢設計工具](../../2014/reporting-services/reporting-services-query-designers.md)  
  
  
