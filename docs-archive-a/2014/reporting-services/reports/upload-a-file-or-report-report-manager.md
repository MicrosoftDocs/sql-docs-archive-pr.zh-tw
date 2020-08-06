---
title: 上傳檔案或報表 (報表管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 119e2b22976dc227e017b81a59b698cf9eb7457f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593284"
---
# <a name="upload-a-file-or-report-report-manager"></a>上傳檔案或報表 (報表管理員)
  報表管理員會提供一項上傳功能，讓您可以將報表、模型和其他檔案加入至報表伺服器，而不需要從用戶端應用程式發行這些項目。 您從檔案系統上傳的檔案會當做項目儲存在報表伺服器上。 您所上傳的檔案類型會決定其儲存方式：  
  
-   .rdl 檔案會儲存成報表。  
  
-   .smdl 檔案會儲存成報表模型。  
  
-   所有其他檔案 (包括共用資料來源 (.rds) 檔案) 則會當做資源上傳。 雖然報表伺服器不會處理資源，但是如果報表伺服器支援檔案的 MIME 類型，您就可以在報表管理員中檢視資源。  
  
### <a name="to-upload-a-file-or-report"></a>若要上傳檔案或報表  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，導覽至 **[內容]** 頁面。 導覽至您要加入項目的資料夾。  
  
3.  按一下 [上傳檔案]****。  
  
4.  按一下 [瀏覽]**** 選取要上傳的檔案。 您可以上傳報表定義檔案、影像、文件，或要在報表伺服器上提供使用的任何檔案。  
  
5.  輸入新項目的名稱。 項目名稱可以包含空格，但是不能包含保留字元：; ? ： \@ & = +，$/* \< > |。  
  
6.  如果您要以新項目取代現有的項目，請選取 [如果項目存在則覆寫]****。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [[內容] 頁面 &#40;報表管理員&#41;](../contents-page-report-manager.md)   
 [上傳檔案頁面 &#40;報表管理員&#41;](../upload-file-page-report-manager.md)   
 [上傳檔案到資料夾](../report-server/upload-files-to-a-folder.md)  
  
  
