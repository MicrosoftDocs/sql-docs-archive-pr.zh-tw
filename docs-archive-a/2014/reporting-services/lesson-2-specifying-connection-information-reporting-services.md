---
title: 第 2 課：指定連線資訊 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c187f0abdc4b277a5f1428407b5c42ca4fd6fee6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87699328"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>第 2 課：指定連接資訊 (Reporting Services)
  將報表加入教學課程專案之後，您需要定義「資料來源」**，這是讓報表從關聯式資料庫、多維度資料庫或其他資源存取資料所用的連接資訊。  
  
 在這一課，您將使用 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 範例資料庫做為您的資料來源。 本教學課程假設這個資料庫位於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 安裝在本機電腦上的預設實例中。  
  
### <a name="to-set-up-a-connection"></a>設定連接  
  
1.  在 [**報表資料**] 窗格中，按一下 [**新增**]，然後按一下 [**資料來源**]。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料]**** 窗格，請按一下 [檢視]**** 功能表上的 [報表資料]****。  
  
2.  在 **[名稱]** 中，輸入 [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]。  
  
3.  確認 [內嵌連接]**** 已選取。  
  
4.  在 [類型]**** 中，選取 [Microsoft SQL Server]****。  
  
5.  在 [連接字串]**** 中，鍵入下列字串：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
     這個連接字串假設 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、報表伺服器和 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫都安裝在本機電腦上，且您有登入 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫的權限。  
  
    > [!NOTE]  
    >  如果您使用 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 或具名執行個體，則連接字串必須包括執行個體資訊：  
    >   
    >  `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2012`  
    >   
    >  如需連接字串的詳細資訊，請參閱 Reporting Services 和[資料來源屬性對話方塊](data-source-properties-dialog-box-general.md)[中的資料連線、資料來源和連接字串](data-connections-data-sources-and-connection-strings-in-reporting-services.md)（一般）。  
  
6.  按一下左窗格中的 [認證]****，然後按一下 [使用 Windows 驗證 (整合式安全性)]****。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]資料來源 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 會加入至 [**報表資料**] 窗格。  
  
## <a name="next-task"></a>下一項工作  
 您已順利定義 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 範例資料庫的連接。 下一步，您將建立報表。 請參閱[第 3 課：定義資料表報表的資料集 &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Data Connections, Data Sources, and Connection Strings in Reporting Services](data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
