---
title: 在 [管理中心] 中建立 PowerPivot 網站的信任位置 |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
author: minewiskan
ms.author: owend
ms.openlocfilehash: 70b1317db7ce413f3a593056f3b8a140b3bdc446
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598574"
---
# <a name="create-a-trusted-location-for-powerpivot-sites-in-central-administration"></a>Create a trusted location for PowerPivot sites in Central Administration
  Excel Services 可讓您指定哪些位置對於在 SharePoint 伺服器上開啟的活頁簿而言是有效的儲存機制。 這些位置稱為「信任位置」，而且您可以針對每個建立的信任位置使用不同的組態設定。 對於 PowerPivot for SharePoint 部署，您可以考慮針對包含 PowerPivot 活頁簿的網站建立信任位置，讓您可以套用最適合 PowerPivot 資料存取的設定，同時針對其餘的伺服陣列保留預設值。  
  
  
  
## <a name="prerequisites"></a>必要條件  
 您必須是伺服陣列管理員或服務管理員，才能將 URL 指定為信任位置。  
  
 您必須知道包含 PowerPivot 圖庫或儲存活頁簿之其他文件庫的 SharePoint 網站之 URL 位址。 若要取得位址，請開啟包含文件庫的網站，以滑鼠右鍵按一下 [ **PowerPivot 圖庫**]，選取 [**屬性**]，然後複製包含伺服器名稱和網站路徑之位址 (URL) 的第一個部分。  
  
##  <a name="overview"></a><a name="overview"></a> 概觀  
 一開始安裝 Excel Services 時，會指定 'http://' 做為其信任位置，也就是說，來自伺服陣列之任何網站的活頁簿都可以在伺服器上開啟。 如果您需要更嚴格控制視為值得信任的位置，您可以建立對應到伺服陣列中特定網站的新信任位置，然後針對每個位置變更設定與權限。  
  
 如果您想要針對其餘的伺服陣列保留預設值，同時套用對 PowerPivot 資料存取最有效的不同設定，針對主控 PowerPivot 活頁簿的網站建立新的信任位置將會很實用。 例如，針對 PowerPivot 活頁簿最佳化之信任位置的活頁簿大小上限為 50 MB，而其餘伺服陣列則使用預設值 10MB。  
  
 如果您使用 PowerPivot 圖庫文件庫來預覽發行的活頁簿，而且您遇到資料重新整理警告而不是您所預期的預覽影像，建議您建立信任的位置。 PowerPivot 圖庫使用文件中的資料和簡報資訊，來轉譯報表和活頁簿的縮圖影像。 如果為信任位置啟用資料重新整理時警告，則 PowerPivot 圖庫可能沒有足夠的權限來執行重新整理，這將會造成顯示錯誤，而不是顯示縮圖影像。 加入包含 PowerPivot 圖庫的網站做為新的信任位置可以排除這個問題。  
  
##  <a name="create-a-trusted-location-for-powerpivot-data-access"></a><a name="create"></a>建立 PowerPivot 資料存取的信任位置  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。  
  
2.  按一下 [Excel Services 服務應用程式]。  
  
3.  按一下 [信任的檔案位置]****。  
  
4.  按一下 [新增信任的檔案位置]****。  
  
5.  輸入包含 PowerPivot 圖庫文件庫之網站的 URL。  
  
6.  在 [位置類型] 中，選取 [Microsoft SharePoint Foundation]****。  
  
    > [!IMPORTANT]  
    >  PowerPivot 資料存取不支援 UNC 和 HTTP 位置類型。  
  
7.  接受 [工作階段管理]、[活頁簿內容] 及 [計算方式] 中屬性的所有預設值。  
  
8.  在 [活頁簿內容] 中，將 [最大活頁簿大小]**** 設定為 **50**。 這樣會將活頁簿檔案大小的上限對齊父 Web 應用程式的檔案上傳上限。 如果您的活頁簿大於 50 MB，您必須進一步增加檔案大小的限制。 如需詳細資訊，請參閱[設定最大檔案上傳大小 &#40;PowerPivot for SharePoint&#41;](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。  
  
9. 在 [外部資料] 中，請確認 [允許外部資料] 設定為 [信任的資料連線庫與內嵌連線]****。 活頁簿中的 PowerPivot 資料存取需要這項設定。  
  
10. 此外，請在 [外部資料] 的 [重新整理時警告] 中，清除 [啟用重新整理警告]**** 的核取方塊。 清除此核取方塊可讓 PowerPivot 圖庫略過例行的警告訊息，並改為顯示活頁簿的預覽影像。  
  
11. 按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 圖庫](../../index.yml)  
 [建立和自訂 PowerPivot 圖庫](create-and-customize-power-pivot-gallery.md)   
 [使用 PowerPivot 圖庫](use-power-pivot-gallery.md)  
  
  
