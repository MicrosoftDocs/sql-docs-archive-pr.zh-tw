---
title: 保護共用資料來源項目的安全 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c4177834a90e2852f4079e3b2bf5a1dd85b9cd51
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87596474"
---
# <a name="secure-shared-data-source-items"></a>保護共用資料來源項目的安全
  您可以在共用資料來源項目上設定安全性，以啟用或停用它的存取權。  
  
 對共用資料來源有最小存取權的使用者 (例如，透過**瀏覽器**角色授與的存取權)，只要也得到檢視報表本身的授權，就可以檢視使用項目的報表清單。  
  
 擁有更多存取權 (例如，透過**內容管理員**角色授與) 的使用者，可以檢視和設定共用資料來源的屬性。  
  
 若要設定安全性，您可以建立角色指派來指定哪些使用者或群組帳戶可以存取共用資料來源。 擁有共用資料項目之存取權的使用者可以變更它的名稱、描述、連接字串或認證資訊。  
  
## <a name="tasks-and-access-to-items"></a>工作與項目的存取  
 建立角色指派時，使用擁有這些工作的角色，以指定適當的權限給使用者和群組。  
  
|選取的工作|授與的權限|  
|----------------------|---------------------------------|  
|檢視資料來源|檢視資料夾階層中的共用資料來源項目。 如果沒有此工作，使用者看不到項目，也許不知道有資料來源可以使用。|  
|管理資料來源|檢視指定名稱、描述和連接資訊的屬性。 此工作也會用來顯示資料夾階層中的共用資料來源項目。 如果您選擇此工作，可以省略「檢視資料來源」工作。|  
|設定項目安全性|建立和修改控制共用資料來源之存取權的角色指派。 此工作必須用於「檢視資料來源」或「管理資料來源」工作。 如果不是，則因為使用者無法選取項目，而沒有作用。|  
  
## <a name="see-also"></a>另請參閱  
 [管理報表資料來源](../report-data/manage-report-data-sources.md)   
 [保護資料夾的安全](secure-folders.md)   
 [保護報表和資源的安全](secure-reports-and-resources.md)   
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)   
 [在 Reporting Services 資料來源中儲存認證](../report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
