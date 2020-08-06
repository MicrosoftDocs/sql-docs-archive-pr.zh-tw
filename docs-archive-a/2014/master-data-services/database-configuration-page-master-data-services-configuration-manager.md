---
title: 資料庫組態頁面 (Master Data Services 組態管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.dbpg.f1
ms.assetid: dd72220e-a599-465d-8b84-9bb6a7433216
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 800eb48d602c799bcc609e283d83c1b1a72c3303
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87703029"
---
# <a name="database-configuration-page-master-data-services-configuration-manager"></a>資料庫組態頁面 (Master Data Services 組態管理員)
  使用 **[資料庫組態]** 頁面，即可編輯 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的系統設定。 系統設定會影響與選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫相關聯的所有 Web 應用程式和 Web 服務。 您必須先選取或建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫，才可啟用及使用系統設定進行組態設定。  
  
## <a name="current-database"></a>目前的資料庫  
 選取現有的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫或建立您要編輯系統設定的新資料庫。 建立新的資料庫之後將會選取它。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**SQL Server 執行個體**|顯示選取的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體名稱。 在您連接到執行個體然後選取或建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫之前，這會是空白的。|  
|**Master Data Services 資料庫**|顯示選取之 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的名稱。 在您連接到執行個體然後選取或建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫之前，這會是空白的。|  
|**Master Data Services 資料庫版本**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫結構描述的版本。|  
|**建立資料庫**|開啟 **[建立資料庫]** 精靈，您可以從此精靈連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，並為該執行個體建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。|  
|**選取資料庫**|開啟 **[連接到資料庫]** 對話方塊，您可以從此對話方塊連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，並選取 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。|  
|**升級資料庫**|開啟精靈，供您用來升級指定的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。 只有當指定的資料庫需要升級時，才會啟用這個按鈕。|  
|**修復資料庫**|按一下此按鈕即可確定 MDS 資料庫是否正確安裝。 如果您備份並還原 MDS 資料庫至從未裝載 MDS 資料庫的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，這樣做可能很有用。|  
  
## <a name="system-settings"></a>系統設定  
 針對與選定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫相關聯的所有 Web 應用程式和 Web 服務編輯系統設定。  
  
 這些設定可在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中使用，並儲存在資料庫的 [系統設定] 資料表 (mdm.tblSystemSetting)。 如需所有設定的清單，請參閱[系統設定 &#40;Master Data Services&#41;](system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Master Data Services 的資料庫和網站](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [資料庫需求 &#40;Master Data Services&#41;](install-windows/database-requirements-master-data-services.md)  
  
  
