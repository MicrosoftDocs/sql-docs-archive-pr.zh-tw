---
title: 建立連結的報表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ed5e70c9ff8179ae05186685e21303693fc9aed7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87597570"
---
# <a name="create-a-linked-report"></a>建立連結報表
  連結報表是提供現有報表之存取點的報表伺服器項目。 它在概念上類似於您用來執行程式或開啟檔案的程式捷徑。

 連結報表是從現有的報表衍生，並保留原始的報表定義。 連結報表一律繼承原始報表的報表配置與資料來源屬性。 其他所有屬性與設定可以和原始報表不同，包括安全性、參數、位置、訂閱，以及排程。

 您想要建立現有報表的其他版本時，可以建立連結報表。 例如，您可以使用單一區域銷售報表，來建立您所有銷售地區的區域特定報表。

 雖然連結報表通常是以參數化報表為基礎，但參數化報表並不是必要的。 每當您想要以不同的設定部署現有的報表時，都可以建立連結報表。

### <a name="to-create-a-linked-report"></a>若要建立連結報表

1.  在報表管理員中，導覽至包含您要連結之報表的資料夾，然後開啟選項功能表。您可以按一下 **[建立連結報表]**。

2.  輸入新連結報表的名稱。 選擇性地輸入描述。

3.  若要選取報表的其他資料夾，請按一下 **[變更位置]**。 按一下您要使用的資料夾，或者在 **[位置]** 方塊中輸入資料夾名稱。 [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 如果您未選取其他資料夾，則會在目前的資料夾 (儲存基準報表的位置) 中建立連結報表。

4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] 連結報表隨即開啟。

     連結報表的圖示與報表伺服器所管理的其他項目不同。 下列圖示表示連結報表：

     ![連結報表圖示](../media/hlp-16linked.gif "連結報表圖示")

## <a name="see-also"></a>另請參閱
 [開啟和關閉報表 &#40;報表管理員&#41;](../reports/open-and-close-a-report-report-manager.md) [新的連結報表頁面 &#40;報表管理員](../new-linked-report-page-report-manager.md)&#41;[選擇專案位置] 頁面 &#40;報表管理員](../choose-item-location-page-report-manager.md)&#41;[一般屬性頁面、報表 &#40;報表管理員](../general-properties-page-reports-report-manager.md)&#41;Reporting Services 的 &#40;[概念&#41;ssrs 報表管理員](../reporting-services-concepts-ssrs.md) [&#40;&#41;ssrs 原生模式](../report-manager-ssrs-native-mode.md)


