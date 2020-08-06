---
title: 定序對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
author: stevestein
ms.author: sstein
ms.openlocfilehash: d551b2ae7ca27250c144afedf13038efd78ad6ed
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607193"
---
# <a name="collation-dialog-box-visual-database-tools"></a>定序對話方塊 (Visual Database Tools)
  這個對話方塊讓您指定資料行的定序序列 (Collation Sequence)。 在將資料行的值與另一個資料行的值或常數值進行比較的任何作業中，會使用資料行的定序序列。 它也會影響某些字串函數的行為，例如 SUBSTRING 和 CHARINDEX。 如需資料行定序設定作用的完整清單，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 文件。  
  
 下列情況會出現這個對話方塊：  
  
-   在 [資料行屬性]  索引標籤的 [定序]  欄位中輸入無效的定序名稱。  
  
-   在 [資料行屬性] 索引標籤的 [定序] 欄位中按一下，然後按一下欄位右側的省略符號按鈕 ( **...** )。  
  
## <a name="options"></a>選項。  
 **SQL 定序**  
 從下拉式清單中選擇 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所定義的定序序列。  
  
 **Windows 定序**  
 從下拉式清單中選擇 Windows 所定義的定序序列。  
  
 **二進位編碼排序**  
 使用字元值的二進位碼進行比較。 如果選取此選項，某些字母順序比較選項會無法使用。 例如，區分字母大小寫的比較會無法使用，因為大寫字母和小寫字母有不同的二進位編碼方式。 只有在選取 [Windows 定序]  時適用。  
  
 **字典排序**  
 使用字母順序比較選項。 只有在選取 [Windows 定序]  時適用。 The alphabetic comparisons options are:  
  
-   **區分大小寫** ：若要比較作業將大寫和小寫字母視為不相同，請選取此選項。  
  
-   **區分腔調字** (Accent Sensitive)：若要比較作業將腔調字母和非腔調字母視為不相同，請選取此選項。 如果選取此選項，比較作業也會將不同的腔調字母視為不相同。  
  
-   **區分假名** ：若要比較作業將日文音節的片假名和平假名視為不相同，請選取此選項。  
  
-   **全半形需相符** (Width Sensitive)：若要比較作業將半形字元和全形字元視為不相同，請選取此選項。  
  
 **還原預設值按鈕**  
 對此資料行套用預設的資料庫定序序列。  
  
## <a name="see-also"></a>另請參閱  
 [在彙總查詢中使用資料行 &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
