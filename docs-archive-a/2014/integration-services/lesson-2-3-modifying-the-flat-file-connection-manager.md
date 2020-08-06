---
title: 步驟 3：修改一般檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b897f9412a8f2978ebe4137e3e79bf1d28c97844
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87592116"
---
# <a name="step-3-modifying-the-flat-file-connection-manager"></a>步驟 3：修改一般檔案連線管理員
  在這項工作中，您將會修改您在第 1 課建立及設定的一般檔案連接管理員。 一開始建立時，已設定一般檔案連接管理員來以靜態方式載入單一檔案。 若要讓一般檔案連線管理員反覆載入檔案，您必須修改連線管理員的 ConnectionString 屬性來接受使用者定義變數 `User:varFileName`，這個變數包含在執行階段要載入的檔案路徑。  
  
 透過將連線管理員修改為使用該使用者定義變數 `User::varFileName`的值，來擴展連線管理員的 ConnectionString 屬性，使連線管理員能夠連接到不同的一般檔案。 在執行階段，Foreach 迴圈容器的每一個反覆運算將動態更新 `User::varFileName` 變數。 更新這個變數會造成連接管理員連接到不同的一般檔案，並使資料流程工作處理不同的資料集。  
  
### <a name="to-configure-the-flat-file-connection-manager-to-use-a-variable-for-the-connection-string"></a>若要設定一般檔案連接管理員使用連接字串的變數  
  
1.  在 **[連接管理員]** 窗格中，以滑鼠右鍵按一下 **[範例一般檔案來源資料]** ，並選取 **[屬性]** 。  
  
2.  在 [屬性視窗中，針對 [**運算式**] 按一下空白儲存格，然後按一下省略號按鈕 [ ** (] ) **。  
  
3.  在 [**屬性運算式編輯器**] 對話方塊的 [**屬性**] 資料行中，輸入或選取 `ConnectionString` 。  
  
4.  在 [**運算式**] 資料行中，按一下省略號按鈕** ( ...] ) **開啟 [**運算式**產生器] 對話方塊。  
  
5.  在 **[運算式產生器]** 對話方塊中，展開 **[變數]** 節點。  
  
6.  將變數 [ **User：： varfilename 拖曳**] 拖曳到 [**運算式**] 方塊中。  
  
7.  按一下 **[確定]** 來關閉 **[運算式產生器]** 對話方塊。  
  
8.  再按一下 **[確定]** 來關閉 **[屬性運算式編輯器]** 對話方塊。  
  
## <a name="next-lesson-task"></a>下一課的工作  
 [步驟 4：測試第 2 課的教學課程封裝](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
