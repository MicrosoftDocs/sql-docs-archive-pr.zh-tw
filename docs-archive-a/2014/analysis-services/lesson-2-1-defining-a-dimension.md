---
title: 定義維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 112696db-3838-4b50-91bd-d2ce5fa04ee5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2eb7a695ffc2c0588396a4a9ea655983c26cc719
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584778"
---
# <a name="defining-a-dimension"></a>定義維度
  在下列工作中，您將使用「維度精靈」來建立「日期」維度。  
  
> [!NOTE]  
>  您必須先完成第 1 課的所有程序，才能進行這一課。  
  
### <a name="to-define-a-dimension"></a>定義維度  
  
1.  在方案總管中 (於 Microsoft Visual Studio 視窗右側)，以滑鼠右鍵按一下 [維度]****，然後按一下 [新增維度]****。 [維度精靈] 隨即出現。  
  
2.  在 [歡迎使用維度精靈]**** 頁面上，按一下 [下一步]****。  
  
3.  在 [選取建立方法]**** 頁面上，確認已選取 [使用現有的資料表]**** 選項，然後按一下 [下一步]****。  
  
4.  在 [指定來源資訊]**** 頁面上，確認已選取 **Adventure Works DW 2012** 資料來源檢視。  
  
5.  在 [主資料表]**** 清單中，選取 [日期]****。  
  
6.  按 [下一步] 。  
  
7.  在 [選取維度屬性]**** 頁面上，選取下列屬性旁的核取方塊：  
  
    -   **日期索引鍵**  
  
    -   **完整日期替代索引鍵**  
  
    -   **英文月份**  
  
    -   **日曆季**  
  
    -   **行事歷年度**  
  
    -   **Calendar Semester**  
  
8.  將 [完整日期替代索引鍵]**** 屬性之 [屬性類型]**** 資料行的設定，從 [一般]**** 變更為 [日期]****。 若要這樣做，請在 [屬性類型]**** 資料行中按一下 [一般]****。 然後，按一下箭號，以便展開選項。 接下來，按一下 [**日期**行事  >  **曆**  >  **日期**]。 按一下 [確定]  。 重複這些步驟，即可變更屬性的屬性類型，如下所示：  
  
    -   [英文月份名稱]**** 變更為 [月]****  
  
    -   [日曆季]**** 變更為 [季]****  
  
    -   [日曆年度]**** 變更為 [年度]****  
  
    -   [日曆半年度]**** 變更為 [半年]****  
  
9. 按 [下一步] 。  
  
10. 在 [正在完成精靈]**** 頁面上，您可以在 [預覽] 窗格中看見 [日期]**** 維度及其屬性。  
  
11. 按一下 [完成]**** 以完成程序。  
  
     在方案總管的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案中，[日期] 維度會顯示在 [維度]**** 資料夾中。 在開發環境的中心，維度設計師會顯示「日期」維度。  
  
12. 在 [檔案] 功能表上，按一下 [全部儲存]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [定義 Cube](lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)   
 [使用現有的資料表建立維度](multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [使用維度精靈建立維度](multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
