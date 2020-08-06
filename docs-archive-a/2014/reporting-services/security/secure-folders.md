---
title: 保護資料夾的安全 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- high-security folders [Reporting Services]
- low-security folders
- folders [Reporting Services], security
- security [Reporting Services], folders
ms.assetid: 0fd91f77-0143-476b-9af0-87293be78e44
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 483b3108713032b3aaf566208f39f6c2f705da1a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87593263"
---
# <a name="secure-folders"></a>保護資料夾的安全
  資料夾安全性是保護報表伺服器中之所有內容的基礎。 因為安全性會在整個資料夾結構繼承，所以您可以指定很多或很少區段的資料夾階層，來允許特定類型的存取。  
  
 高安全性資料夾可以用來儲存機密報表，或當成臨時區域；例如，您可以先使用一個資料夾來測試報表，然後再將報表移至最終位置。 若要控制此區域的存取，您可以定義一個角色指派，只允許報表作者加入和刪除項目，以及第二個角色指派，允許測試者執行報表，但不能加入或移除項目。 因為角色指派是專為測試者與報表作者所定義，所以沒有其他使用者 (除了本機系統管理員以外) 可以存取資料夾。  
  
 低安全性資料夾可以用來儲存您要很容易存取的報表。  
  
 資料夾安全性會形成項目層級安全性的基礎，以報表伺服器資料夾階層的根節點開始，也就是 [主資料夾] 資料夾。 因為安全性是繼承的，建議在 [主資料夾] 資料夾設定較嚴格的安全性原則。 使用 [主資料夾] 角色指派裡的 [瀏覽器]  角色，即可提供只供檢視存取。  
  
## <a name="tasks-and-folder-access"></a>工作和資料夾存取  
 建立資料夾的角色指派時，請考慮下表列出的工作。  
  
|選取的工作|授與的權限|  
|----------------------|---------------------------|  
|檢視資料夾|檢視資料夾階層，以及指出資料夾建立與修改時間的唯讀屬性。<br /><br /> 除非指派給使用者的角色還包含了「檢視報表」、「檢視模型」、「檢視資源」及「檢視資料來源」等工作，否則使用者無法檢視資料夾內的項目。|  
|管理資料夾|檢視資料夾屬性、變更名稱或描述，或者將資料夾移到另一個位置。 此工作允許使用者建立資料夾。|  
|管理報表|從檔案系統將報表加入至資料夾，以及從報表設計師將報表發行至報表伺服器。|  
|管理資料來源|將新的共用資料來源項目加入至資料夾，以及變更現有的共用資料來源。|  
|設定項目安全性|建立和修改控制資料夾之存取的角色指派。 此工作必須用於「檢視資料夾」或「管理資料夾」。 若不這麼做，使用者將無法選取項目，而不會產生任何影響。|  
  
## <a name="see-also"></a>另請參閱  
 [保護報表和資源的安全](secure-reports-and-resources.md)   
 [保護共用資料來源項目的安全](secure-shared-data-source-items.md)   
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)  
  
  
