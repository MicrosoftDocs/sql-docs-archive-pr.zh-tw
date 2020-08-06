---
title: 移動或刪除項目 (報表管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a61ad56ea9e20e7fdf38d5acf05529b685ee896
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686768"
---
# <a name="move-or-delete-an-item-report-manager"></a>移動或刪除項目 (報表管理員)
  您發行至報表伺服器的報表和報表相關項目會儲存在資料夾中。 您可以將項目移至不同的資料夾，報表伺服器會自動維護這些項目的參考。 刪除某個項目之前，請考慮是否有其他項目相依於該項目。  
  
## <a name="move-an-item"></a>移動項目  
 您可以將報表伺服器項目移至報表伺服器資料夾階層中不同的資料夾位置。 當您移動項目時，所有屬性 (包括安全性設定) 都會跟著項目移到新位置。 您移動資料夾時，資料夾內的所有項目都會隨著一起移動。  
  
 在報表管理員中，資料夾階層中會指出可以移動的項目。 下表顯示每一個可移動項目的圖示。  
  
|圖示|可移動項目|  
|----------|-------------------|  
|![Report icon](../media/hlp-16doc.gif "報表圖示")|Report|  
|![連結報表圖示](../media/hlp-16linked.gif "連結報表圖示")|連結報表|  
|![資料夾圖示](../media/hlp-16folder.gif "資料夾圖示")|資料夾|  
|![一般資源圖示](../media/hlp-16file.gif "一般資源圖示")|一般資源|  
|![Shared data source icon](../media/hlp-16datasource.png "共用資料來源圖示")|共用資料來源|  
||共用資料集|  
  
 並非所有的項目都可以移動。 您無法移動與報表相關聯的項目，例如訂閱或報表記錄。 那些項目會隨著相關聯的報表移動。 同樣地，您無法移動存在於資料夾階層之外的項目 (例如共用排程)。 如果您沒有權限也無法移動項目。 在您的角色指派中為目標項目選取下列工作時，即涵蓋移動項目的權限：「管理報表」、「管理模型」、「管理資料夾」，以及「管理資料來源」。  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>若要從內容頁面中移動項目  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;].。/report-manager-ssrs-native-mode.md) 。  
  
2.  在報表管理員中，巡覽至 [內容]  頁面，然後找出您要移動的項目。  
  
3.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
4.  在下拉式功能表中，按一下 **[移動]** 。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  針對 [位置]  ，請指定您要移動項目的目標資料夾。 您可以輸入完整資料夾名稱，或使用樹狀目錄控制項導覽至資料夾。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 或者，您可以巡覽至要移動的物件、按一下 [屬性]  ，然後按一下頁面頂端的 [移動]  。  
  
## <a name="delete-an-item"></a>刪除項目  
 刪除某個項目之前，請判斷是否有其他項目使用該項目。 例如，如果您刪除了某個共用資料來源，使用該資料來源的報表和模型將無法再執行。 如果您刪除了某份報表，就會一併刪除與該報表相關聯的訂閱和報表記錄。 若要尋找專案的相依專案，請參閱 [相依專案] 頁面 &#40;報表管理員&#41;]。/dependent-items-page-report-manager.md) 。  
  
#### <a name="to-delete-a-report-or-item"></a>若要刪除報表或項目  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;].。/report-manager-ssrs-native-mode.md) 。  
  
2.  在報表管理員中，巡覽至 [內容]  頁面，然後找出您要刪除的項目。  
  
3.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
4.  在下拉式功能表中，按一下 [刪除]  。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [內容頁 &#40;報表管理員&#41;].。/contents-page-report-manager.md)    
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
