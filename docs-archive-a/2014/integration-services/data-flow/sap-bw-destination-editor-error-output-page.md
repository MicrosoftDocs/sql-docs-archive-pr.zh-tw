---
title: SAP BW 目的地編輯器 (錯誤輸出頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a543d811-0bd2-4890-a0d3-f5fdcd4524b8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9ffd58580865a71626252aa2d177530e41156537
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687077"
---
# <a name="sap-bw-destination-editor-error-output-page"></a>SAP BW 目的地編輯器 (錯誤輸出頁面)
  使用 [SAP BW 目的地編輯器] 的 [錯誤輸出] 頁面可以指定錯誤處理選項。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目的地，請參閱 [SAP BW 目的地](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **開啟錯誤輸出頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程]  索引標籤上，按兩下 SAP BW 目的地。  
  
3.  在 [SAP BW 目的地編輯器]  中，按一下 [錯誤輸出]  開啟編輯器的 [錯誤輸出]  頁面。  
  
## <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定目的地的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **輸入或輸出**  
 檢視輸入的名稱。  
  
 **資料行**  
 這個選項不適用。  
  
 **錯誤**  
 指定目的地應該在發生錯誤時採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **截斷**  
 這個選項不適用。  
  
 **說明**  
 檢視作業的描述。  
  
 **將這個值設定到選取的資料格**  
 指定目的地應該在發生錯誤或截斷時對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 目的地編輯器 &#40;連線管理員頁面&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 目的地編輯器 &#40;對應頁面&#41;](sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 目的地編輯器 &#40;進階頁面&#41;](sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 說明](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
