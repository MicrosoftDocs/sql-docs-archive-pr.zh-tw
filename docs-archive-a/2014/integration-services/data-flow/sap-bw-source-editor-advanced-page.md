---
title: SAP BW 來源編輯器 (進階頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7c78d40555a30031bf39abda18048fda9c648d01
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87707706"
---
# <a name="sap-bw-source-editor-advanced-page"></a>SAP BW 來源編輯器 (進階頁面)
  使用 [SAP BW 來源編輯器] 的 [進階] 頁面可以指定字串轉換規則和逾時期限，也可以重設特定要求識別碼的狀態。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 來源元件，請參閱 [SAP BW 來源](sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
> [!IMPORTANT]  
>  擷取 SAP Netweaver BW 中的資料需要額外的 SAP 授權。 請洽詢 SAP 以確認這些需求。  
  
 **開啟連接管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程]  索引標籤上，按兩下 SAP BW 來源。  
  
3.  在 **[SAP BW 來源編輯器]** 中，按一下 **[進階]** 開啟編輯器的 **[進階]** 頁面。  
  
## <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定來源的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **字串轉換**  
 指定要針對字串轉換套用的規則。  
  
|選項|描述|  
|------------|-----------------|  
|**自動字串轉換**|當 SAP Netweaver BW 系統是 Unicode 系統時，將所有字串轉換為 `nvarchar`。 否則，將所有字串轉換為 `varchar`。|  
|**將字串轉換為 varchar**|將所有字串轉換為 `varchar`。|  
|**將字串轉換為 nvarchar**|將所有字串轉換為 `nvarchar`。|  
  
 **逾時 (秒)**  
 指定來源應該等候的秒數上限。  
  
> [!NOTE]  
>  只有當您已經在編輯器的 [連接管理員] 頁面上，選取 [W - 等候通知] 作為 [執行模式] 的值時，這個選項才有效。 如需詳細資訊，請參閱 [SAP BW 來源編輯器 &#40;連接管理員頁面&#41;](sap-bw-source-editor-connection-manager-page.md)。  
  
 **要求識別碼**  
 指定您想要在按一下 [重設]  時將其狀態重設成「G - 綠色」的要求識別碼。  
  
 **重設**  
 在提示確認之後，讓您將指定之要求識別碼的狀態重設成「G - 綠色」。 在發生問題，而且 SAP Netweaver BW 系統已將要求標幟為黃色或紅色狀態時，這個選項可能很有用。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 來源編輯器 &#40;連線管理員頁面&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 來源編輯器 &#40;資料行頁面&#41;](sap-bw-source-editor-columns-page.md)   
 [SAP BW 來源編輯器 &#40;錯誤輸出頁面&#41;](sap-bw-source-editor-error-output-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 說明](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
