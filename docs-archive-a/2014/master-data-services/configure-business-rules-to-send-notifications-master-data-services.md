---
title: 設定商務規則來傳送通知 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cb1a12167dffe123e55760f031e21499fe22a945
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87607444"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>設定商務規則來傳送通知 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您想要通知使用者屬性值變更時，請設定商務規則來傳送通知。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 [系統管理]**** 和 [使用者及群組的權限]**** 功能區域的權限。 如果您沒有 [使用者及群組的權限]**** 功能區域的權限，就無法檢視傳送通知的目標使用者和群組清單。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   使用驗證動作的商務規則必須已經存在。 如需詳細資訊，請參閱[建立及發行商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)。  
  
-   接收通知的使用者或群組至少必須針對驗證失敗的屬性擁有 [唯讀]**** 權限。 遭明確或隱含拒絕此屬性之權限的使用者或群組將會收到電子郵件，但是無法在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中存取此屬性。  
  
-   如果將郵件傳送給群組，只有可存取 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的群組成員會收到電子郵件。  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>若要設定商務規則來傳送通知  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  從 [實體]**** 清單中選取實體。  
  
5.  從 [**成員類型**] 清單中，選取成員的類型。  
  
6.  從 [屬性]**** 清單中，選取屬性或保留預設值 [全部]****。  
  
7.  在方格中，按兩下商務規則的資料列中的 [**通知**] 欄位。  
  
8.  從子功能表中，按一下要傳送電子郵件通知給哪一個使用者或群組。  
  
## <a name="next-steps"></a>後續步驟  
  
-   遵循下列其中一個程序，將商務規則套用至資料：  
  
    -   [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [根據商務規則驗證版本 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   依照下列方式設定電子郵件通訊協定：  
  
    -   [設定電子郵件通知 &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [通知 &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [設定電子郵件通知 &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
  
