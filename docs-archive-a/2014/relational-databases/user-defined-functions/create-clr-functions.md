---
title: 建立 CLR 函式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
author: rothja
ms.author: jroth
ms.openlocfilehash: 9741646e43d48bc9336b91538c6065c09855c87d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687730"
---
# <a name="create-clr-functions"></a>建立 CLR 函數
  您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體內部建立資料庫物件，這個物件是透過使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 建立的組件來撰寫。 可以利用 Common Language Runtime 所提供的豐富程式設計模型的資料庫物件，包含彙總函式、函數、預存程序、觸發程序以及類型。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立 CLR 函數包含下列步驟：  
  
-   以 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]支援的語言，將函數定義成類別的靜態方法。 如需如何以 Common Language Runtime 設計函數的詳細資訊，請參閱 [CLR 使用者定義函數](../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)。 然後，使用適當的語言編譯器編譯類別，在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中建立組件。  
  
-   使用 CREATE ASSEMBLY 陳述式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中登錄組件。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中之組件的詳細資訊，請參閱[組件 &#40;Database Engine&#41;](../clr-integration/assemblies-database-engine.md)。  
  
-   使用 [CREATE FUNCTION](/sql/t-sql/statements/create-function-transact-sql) 陳述式建立參考已註冊組件的函數。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中部署 SQL Server 專案，便會在已指定給專案的資料庫中註冊組件。 部署專案也會在資料庫中，為所有以 `SqlFunction` 屬性註解的方法建立 CLR 函數。 如需詳細資訊，請參閱 [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 CLR 程式碼的功能預設為關閉。 您可以建立、改變和卸除參考 Managed 程式碼模組的資料庫物件，但是除非使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure (Transact-SQL) [來啟用](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) [CLR 已啟用] 選項 [，否則在](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)中將無法執行這些參考。  
  
## <a name="accessing-external-resources"></a>存取外部資源  
 CLR 函數可用以存取外部資源，例如，檔案、網路資源、Web Service、其他資料庫 (包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的遠端執行個體)。 這可透過使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]中的各種類別來達成，例如 `System.IO`、 `System.WebServices`、 `System.Sql`等等。 包含這類函數的組件應該至少使用 EXTERNAL_ACCESS 權限來設定才能達成此目的。 如需詳細資訊，請參閱 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)支援的語言，將函數定義成類別的靜態方法。 SQL Client Managed Provider 可用以存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的遠端執行個體。 不過，在 CLR 函數中不支援回送連接到原始伺服器。  
  
 **若要建立、修改或卸除 SQL Server 中的組件**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **若要建立 CLR 函數**  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
## <a name="accessing-native-code"></a>存取機器碼  
 CLR 函數可用來透過 Managed 程式碼中的 PInvoke 存取機器碼 (Unmanaged 程式碼)，例如使用 C 或 C++ 撰寫的程式碼 (如需詳細資訊，請參閱 [從 Managed 程式碼呼叫原生函數](https://go.microsoft.com/fwlink/?LinkID=181929) )。 如此可讓您重複使用舊版程式碼 (如 CLR UDF) 或是使用機器碼撰寫關鍵效能 UDF。 這樣的處理方式需要 UNSAFE 組件。 如需了解使用 UNSAFE 組件的注意事項，請參閱 [CLR 整合程式碼存取安全性](../clr-integration/security/clr-integration-code-access-security.md) 。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義函數 &#40;Database Engine&#41;](create-user-defined-functions-database-engine.md)   
 [建立使用者定義彙總](create-user-defined-aggregates.md)   
 [執行使用者定義函數](execute-user-defined-functions.md)   
 [檢視使用者定義函數](view-user-defined-functions.md)   
 [Common Language Runtime &#40;CLR&#41; 整合程式設計概念](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
