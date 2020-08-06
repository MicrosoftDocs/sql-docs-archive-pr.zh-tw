---
title: 建立應用程式角色 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.approle.general.f1
helpviewer_keywords:
- application roles [SQL Server], creating
ms.assetid: 6b8da1f5-3d8e-4f88-b111-b915788b06f1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 51272dad57558cdb771f9b98a2f5e5b3da7609cb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87598784"
---
# <a name="create-an-application-role"></a>建立應用程式角色
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中建立應用程式角色。 應用程式角色限制使用者必須經由特定應用程式存取資料庫。 應用程式角色沒有使用者，所以選取 **[應用程式角色]** 時，不會顯示 **[角色成員]** 。  
  
> [!IMPORTANT]  
>  設定應用程式角色時會檢查密碼複雜性。 叫用應用程式角色的應用程式必須儲存其密碼。 應用程式角色密碼應該一律以加密方式儲存。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立應用程式角色：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料庫的 ALTER ANY APPLICATION ROLE 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
##### <a name="to-create-an-application-role"></a>若要建立應用程式角色  
  
1.  在 [物件總管] 中，展開您要建立應用程式角色的資料庫。  
  
2.  展開 **[安全性]** 資料夾。  
  
3.  展開 **[角色]** 資料夾。  
  
4.  以滑鼠右鍵按一下 [應用程式角色] 資料夾，然後選取 [新增應用程式角色]。  
  
5.  在 [應用程式角色 - 新增] 對話方塊，於 [一般] 頁面上的 [角色名稱] 方塊中輸入新應用程式角色的名稱。  
  
6.  在 **[預設結構描述]** 方塊中，透過輸入物件名稱，指定擁有此角色建立的物件之結構描述。 或者，按一下省略符號 **(...)** ，開啟 [尋找結構描述] 對話方塊。  
  
7.  在 **[密碼]** 方塊中，輸入新角色的密碼。 在 [確認密碼]  方塊中再次輸入密碼。  
  
8.  在 **[此角色擁有的結構描述]** 底下，選取或檢視此角色將擁有的結構描述。 結構描述僅能由一個結構描述或角色擁有。  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>其他選項  
 [應用程式角色 - 新增] 對話方塊也在其他兩個頁面上提供選項：[安全性實體] 和 [擴充屬性]。  
  
-   **[安全性實體]** 頁面列出所有可能的安全性實體以及可授與登入的安全性實體權限。  
  
-   **[擴充屬性]** 頁面讓您能夠將自訂屬性加入至資料庫使用者。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-application-role"></a>若要建立應用程式角色  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Creates an application role called "weekly_receipts" that has the password "987Gbv876sPYY5m23" and "Sales" as its default schema.  
  
    CREATE APPLICATION ROLE weekly_receipts   
        WITH PASSWORD = '987G^bv876sPY)Y5m23'   
        , DEFAULT_SCHEMA = Sales;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-application-role-transact-sql)。  
  
  
