---
title: 反轉交易 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fb5b1b0932b65b1d6f8fe7b1bc842836e21aaca6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87698344"
---
# <a name="reverse-a-transaction-master-data-services"></a>反轉交易 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，系統管理員可以在需要復原動作時，反轉交易。 交易的範例包括屬性值變更、階層移動或成員刪除。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   您必須擁有存取 **[版本管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-reverse-a-transaction"></a>若要反轉交易  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，按一下 [版本管理]****。  
  
2.  在功能表列上，按一下 [交易]****。  
  
3.  在 [交易]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  從 **[版本]** 清單中選取版本。  
  
5.  針對您想要反轉的交易，按一下方格中的資料列。  
  
6.  按一下 [反轉交易]****。  
  
7.  在確認對話方塊中按一下 **[確定]**。 如此就會將另一個交易加入至方格，以便記錄反轉的交易。  
  
## <a name="see-also"></a>另請參閱  
 [交易 &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)   
 [重新啟用成員或集合 &#40;Master Data Services&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
  
  
