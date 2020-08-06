---
title: 設定適用於 Excel 之 Master Data Services 增益集的屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cab1c662-5d40-4c16-9f5c-36ff9608810b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fef16f471655ff2f753d2f7234f511c20166ebb0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596752"
---
# <a name="setting-properties-for-master-data-services-add-in-for-excel"></a>設定適用於 Excel 之 Master Data Services 增益集的屬性
  Master Data Services Add-in for Excel 設定會決定如何從 MDS 將資料載入 Excel 增益集，以及如何從 Excel 增益集將資料發行到 MDS。  
  
 若要針對 Excel 增益集進行設定，請開啟 [Excel]****，並按一下 [主要資料]**** 功能表，然後按一下 [設定]****。 可存取 Excel 的任何人都可以變更這些設定。 這些設定適用於開啟 Excel 的電腦。  
  
## <a name="excel-add-in-settings"></a>Excel 增益集設定  
  
||||  
|-|-|-|  
|索引標籤和區段|設定|描述|  
|設定：發行|在發行時顯示 [發行並註解]**** 對話方塊|在您按一下 [發行]**** 之後，選取此選項可顯示 [發行並註解]**** 對話方塊，好讓您輸入所有變更的單一註解，或輸入每一項變更的註解。<br /><br /> 取消選取此選項可指定發行程序已起始，而不必顯示 [發行並註解]**** 對話方塊。 您將沒有機會輸入註解。|  
|設定：版本|版本選取項目|選取將載入 Excel 增益集中之主要資料的版本。 可為以下項目：<br /><br /> [無]**** 表示具有未預設為任何版本的版本<br /><br /> [最舊]**** 表示預設為最舊的版本；[最新]**** 表示預設為最新的版本。|  
|設定：記錄|開啟詳細記錄|針對從 MDS 將主要資料載入至 Excel 增益集的程式啟用記錄功能，以記錄服務中每個命令的結果。|  
|設定：批次大小|要載入的資料格數目|選取一個數字，此數字指示在從 MDS 伺服器載入 Excel 的批次中，將會載入幾千個資料格。 預設值是 50,000 個資料格。|  
|設定：批次大小|要發行的資料格數目|選取一個數字，此數字指示在從 Excel 傳回到伺服器的批次中，將會發行幾千個資料格。 預設值是 50,000 個資料格。|  
|設定：加入至安全清單的伺服器|全部清除|按一下此選項，可清除在開啟關聯的捷徑查詢檔案時，指定為安全的連接清單。|  
|資料：篩選|顯示大型資料集的篩選警告|按一下此選項，當從 MDS 載入至 Excel 的資料集超過最大資料列或資料行數目時，便會顯示警告。|  
|資料：篩選|最大資料列數|選取所載入之資料列數目的臨界值，超出此臨界值將會公佈篩選警告。|  
|資料：篩選|最大資料行數|選取所載入之資料行數目的臨界值，超出此臨界值將會公佈篩選警告。|  
|資料：資料格格式|變更色彩的時機：屬性值變更|按一下此選項可指定資料格的色彩將會在以下情況中變更：如果當您使用 MDS 儲存機制中的新資料重新整理 Excel 增益集資料表，該資料格中的屬性值會變更。|  
|資料：資料格格式|變更色彩的時機：已加入成員|按一下此選項可指定資料列資料格的色彩將會在以下情況中變更：如果當您使用 MDS 存放庫中的新資料來重新整理 Excel 增益集資料表時，新的成員會新增至此資料列。|  
  
  
