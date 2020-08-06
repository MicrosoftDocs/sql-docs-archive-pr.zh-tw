---
title: 檢查使用中的檔案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccd65867-d4c0-43b2-8361-7fd41c6f79ac
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 51505b0dece146b7f6fcdf982e6f88a5715357e1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87595514"
---
# <a name="check-files-in-use"></a>檢查使用中的檔案
  若要避免在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新之後重新啟動 Windows，請使用 [檢查使用中檔案] 頁面來識別正在鎖定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新安裝程式所需之檔案的處理序。  
  
 停止所有連接到正在更新之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的應用程式和服務。 其中包括停止 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
 如果安裝程式判斷在安裝時鎖定了檔案，則在安裝完成之後可能必須重新啟動電腦。 如有必要，安裝程式會提示您重新啟動電腦。 如果安裝程式必須在安裝時結束某項服務，它會在安裝完成之後重新啟動該服務。  
  
 為了排除安裝之後重新啟動電腦的需求，安裝程式會顯示正在鎖定檔案之處理序的清單。 請停止或結束此清單中的處理序和應用程式， 然後按一下 **[重新整理檢查]** 重新執行檢查。 按一下 **[停止檢查]** 可結束正在執行的檢查作業。 如果找不到鎖定的檔案，表格會是空的。 當所有鎖定的處理序都已關閉或停止時，請按 **[下一步]** 繼續。  
  
 安裝程式會將資訊記錄到記錄檔中。 如需有關如何檢視記錄檔的詳細資訊，請參閱 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md) 和 [如何：讀取 SQL Server 安裝程式記錄檔](https://go.microsoft.com/fwlink/?LinkID=134490)。  
  
 記錄檔中將包含下列資訊：  
  
-   處理序的名稱  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的名稱  
  
-   處理序類型  
  
-   執行處理序所使用的帳戶  
  
-   處理序識別碼  
  
-   鎖定的檔案名稱  
  
## <a name="ui-element-list"></a>UI 元素清單  
  
|名稱|描述|  
|----------|-----------------|  
|Process|顯示正在使用要更新之檔案的處理序完整名稱。|  
|類型|顯示處理序的類型。|  
|帳戶|顯示執行處理序所使用的帳戶。|  
|處理序識別碼|顯示處理序識別碼。|  
  
  
