---
title: 使用 ODBC 目的地來載入資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e8bf0b30619c2886df6ddb28858cf98bad858421
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87700096"
---
# <a name="load-data-by-using-the-odbc-destination"></a>使用 ODBC 目的地來載入資料
  此程序說明如何透過使用 ODBC 目的地載入資料。 若要加入及設定 ODBC 目的地，封裝必須已包括至少一個「資料流程」工作與來源。  
  
### <a name="to-load-data-using-an-odbc-destination"></a>使用 ODBC 目的地載入資料  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟所要的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  按一下 **[資料流程]** 索引標籤，然後將 ODBC 目的地從 **[工具箱]** 拖曳到設計介面。  
  
3.  將某個資料流程元件的可用輸出拖曳到 ODBC 目的地的輸入。  
  
4.  按兩下 ODBC 目的地。  
  
5.  在 **[ODBC 目的地編輯器]** 對話方塊中的 **[連接管理員]** 頁面上，選取現有的 ODBC 連接管理員，或按一下 **[新增]** 以建立新的連接管理員。  
  
6.  選取資料存取方法。  
  
    -   **資料表名稱 - 批次**：若要將 ODBC 目的地設定成以批次模式運作，請選取此選項。 當您選取此選項時，可以設定 **[批次大小]** 。  
  
    -   **資料表名稱 - 逐列**：若要將 ODBC 目的地設定成插入每個資料列至目的地資料表 (一次一個)，請選取此選項。 當您選取此選項時，資料會以一次一個資料列的方式載入到資料表。  
  
7.  在 **[資料表或檢視表的名稱]** 欄位中，從清單中選取資料庫中可用的資料表或檢視表，或是輸入可識別資料表的規則運算式。此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。  
  
8.  您可以按一下 **[預覽]** ，最多可檢視從 ODBC 目的地中選取之資料表的 200 個資料列。  
  
9. 按一下 **[對應]** ，然後將資料行從一個清單拖曳至另一個清單，使 **[可用的輸入資料行]** 清單中的資料行對應至 **[可用的目的地資料行]** 清單中的資料行。  
  
10. 若要設定錯誤輸出，請按一下 **[錯誤輸出]** 。  
  
11. 按一下 [確定]  。  
  
12. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 目的地編輯器 &#40;連線管理員頁面&#41;](../odbc-destination-editor-connection-manager-page.md)   
 [ODBC 目的地編輯器 &#40;對應頁面&#41;](../odbc-destination-editor-mappings-page.md)   
 [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../odbc-source-editor-error-output-page.md)  
  
  
