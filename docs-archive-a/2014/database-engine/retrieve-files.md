---
title: 取出檔案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], file retrieval
- file retrieval [SQL Server]
- retrieving files
ms.assetid: 37b74426-e262-43b2-a81f-79b1fd1a36ec
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ebced9ea69f304344893289140687cd6d511e923
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87599159"
---
# <a name="retrieve-files"></a>擷取檔案
  開啟原始檔控制專案之後，您可以利用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，將原始檔控制存放區中的專案檔本機複本擷取到專案所在的本機目錄中。  
  
 您可以依照下列方式，利用整合式原始檔控制來擷取檔案：  
  
-   **取得 (遞迴) 命令的最新版本**  
  
     擷取所選檔案最新的簽入版本。 如果選取某個方案或專案，這個命令會擷取所有方案或專案檔的最新版本。  
  
-   **Get**命令  
  
     顯示 [**取得**] 對話方塊，您可以使用此對話方塊來抓取所選檔案的最新版本，或是抓取所選方案或專案中的檔案子集。  
  
### <a name="to-retrieve-the-latest-version-of-all-the-files-in-a-project"></a>擷取專案中所有檔案的最新版本  
  
1.  在 [方案總管] 中選取專案。  
  
2.  **在 [檔案**] 功能表上，指向 [原始檔**控制**]，然後按一下 [**取得最新的版本 (遞迴) **]。  
  
 專案中檔案的最新版本會擷取到本機磁碟的專案位置中。  
  
#### <a name="to-retrieve-only-certain-files-in-a-project"></a>只擷取專案中的某些檔案  
  
1.  在 [方案總管] 中，選取您要擷取的項目。  
  
2.  **在 [檔案**] 功能表上，指向 [原始檔**控制**]，然後按一下 [**取得**]。  
  
3.  在 [**取得**] 對話方塊中，按一下 **[確定**]。 另外，如果您在 [方案總管] 中選取方案或專案，請清除您不要擷取的項目旁的核取方塊。  
  
## <a name="see-also"></a>另請參閱  
 [[取得] 對話方塊 &#40;原始檔控制&#41;](../../2014/database-engine/get-dialog-box-source-control.md)   
 [設定和抓取版本資訊](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [視圖專案歷程記錄](../../2014/database-engine/view-project-history.md)   
 [檢視檔案狀態](../../2014/database-engine/view-file-status.md)  
  
  
