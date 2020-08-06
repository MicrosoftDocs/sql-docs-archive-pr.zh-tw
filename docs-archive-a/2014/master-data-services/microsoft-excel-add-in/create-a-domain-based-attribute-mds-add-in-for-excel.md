---
title: 建立網域屬性 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bda0c7f63ad380aaea5d980d2e729822ec9a3d22
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584619"
---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>建立網域屬性 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，當系統管理員想要將資料行中的值限制為一組特定的值時，可以建立網域屬性。  
  
 值可以已經在工作表中，也可以來自現有實體。  
  
> [!NOTE]  
>  如果使用者在受條件約束的資料行中輸入值，而不是從清單中選取，在發行時 **$InputStatus$** 資料行中會顯示錯誤。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 [系統管理]**** 和總管**** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../administrators-master-data-services.md)。  
  
-   模型和實體必須已經存在。  
  
### <a name="to-perform-this-procedure"></a>若要執行此程序：  
  
1.  在 Excel 中，載入包含您想要限制之資料行 (屬性) 的實體。 如需詳細資訊，請參閱將[資料從 MDS 載入 Excel](export-data-to-excel-from-master-data-services.md)中。  
  
2.  在您想要限制的資料行中按一下任何資料格。  
  
3.  在 [建立模型]**** 群組中，按一下 [屬性內容]****。  
  
4.  在 [屬性內容]**** 對話方塊中，從 [屬性類型]**** 清單中選擇 [受條件約束的清單 (網域)]****。  
  
5.  在 [使用下列來源的值擴展屬性]**** 清單中：  
  
    -   若要使用工作表中的值，請選擇 [選取的資料行]****。 將會以選取的資料行中的值建立新的實體和新的暫存資料表。  
  
    -   若要使用現有實體中的值，請選擇實體的名稱。  
  
6.  如果您在上一個步驟中選擇 [選取的資料行]****，請在 [新實體名稱]**** 方塊中輸入新實體的名稱。 此名稱可以與資料行 (屬性) 名稱相同。  
  
7.  按一下 [確定]  。 資料行中的每個資料格現在都有一個可供使用者選擇的值清單。  
  
## <a name="next-steps"></a>後續步驟  
  
-   若要在受條件約束的清單中加入及刪除值，請載入屬性所依據的實體。 如需載入實體的詳細資訊，請參閱將[資料從 MDS 載入 Excel](export-data-to-excel-from-master-data-services.md)中。  
  
## <a name="see-also"></a>另請參閱  
 [以網域為基礎的屬性 &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)   
 [&#40;適用于 Excel 的 MDS 增益集建立實體&#41;](create-an-entity-mds-add-in-for-excel.md)   
 [建立模型 &#40;適用於 Excel 的 MDS 增益集&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
