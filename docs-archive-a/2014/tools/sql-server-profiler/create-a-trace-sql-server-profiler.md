---
title: 建立追蹤 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], creating
ms.assetid: 0302fa6d-d2b5-43fe-ad70-7a337575b112
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d73333bbf0ba985ed4952e03584b4e4c130ab6f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87686604"
---
# <a name="create-a-trace-sql-server-profiler"></a>建立追蹤 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來建立追蹤。  
  
### <a name="to-create-a-trace"></a>若要建立追蹤  
  
1.  在 **[檔案]** 功能表上，按一下 **[新增追蹤]** ，並連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
     會出現 [追蹤屬性]  對話方塊。  
  
    > [!NOTE]  
    >  **[追蹤屬性]** 對話方塊無法顯示，但若已選取 **[進行連接後立即啟動追蹤]** ，便會開始追蹤。 於 [工具] 功能表，按一下 [選項]，並清除 [連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
2.  在 **[追蹤名稱]** 方塊中，輸入追蹤的名稱。  
  
3.  在 **[使用範本]** 清單中，選取追蹤使用為基礎的追蹤範本；若不想要使用範本，請選取 **[空白]** 。  
  
4.  若要儲存追蹤結果，請執行下列其中之一：  
  
    -   按一下 [儲存至檔案]****，將追蹤擷取至檔案。 在 **[設定最大檔案大小]** 中指定一個值。 預設值為 5 MB。  
  
         (選擇性) 選取 **[啟用檔案換用]** ，在達到檔案大小上限時自動建立新檔案。 您也可以選取 **[伺服器處理追蹤資料]** ，選取此選項後會由執行追蹤的服務處理追蹤資料，而非由用戶端應用程式來處理。 當伺服器處理追蹤資料時，即使在負擔極重情況下，也不會略過事件，但伺服器效能將受到影響。  
  
    -   按一下 **[儲存至資料表]** 以將追蹤擷取至資料庫的資料表。  
  
         (選擇性) 按一下 **[設定最大資料列數]** ，然後指定一個值。  
  
    > [!CAUTION]  
    >  當您不將追蹤結果儲存至檔案或資料表時，您可以在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 開啟時檢視追蹤。 但是，當您停止追蹤並關閉 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]後會遺失追蹤結果。 若要使用此方式以避免遺失追蹤結果，請在關閉 **之前，按一下** [檔案] **功能表上的** [儲存] [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來儲存結果。  
  
5.  (選擇性) 選取 **[啟用追蹤停止時間]** 核取方塊，然後指定停止日期和時間。  
  
6.  若要加入或移除事件、資料行或篩選，請按一下 [事件選取範圍]**** 索引標籤。 如需詳細資訊，請參閱[指定追蹤檔案的事件及資料行 &#40;SQL Server Profiler&#41;](sql-server-profiler.md)。  
  
7.  按一下 **[執行]** 啟動追蹤。  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL Server Profiler 所需的權限](permissions-required-to-run-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](sql-server-profiler-templates-and-permissions.md)   
 [[SQL Server Profiler]](sql-server-profiler.md)   
 [使追蹤與 Windows 效能記錄資料產生相互關聯 &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
